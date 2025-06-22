---
title: "Forking dangerous"
datePublished: Sun Jun 22 2025 15:10:00 GMT+0000 (Coordinated Universal Time)
cuid: cmc7t0n0m000902jsfff7a1vp
slug: forking-dangerous
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/Grlq50tXDl8/upload/2ff78ee3533ee4b40c618fd93d5fb542.jpeg
tags: python, process, clone, fork, deadlock

---

### **TL;DR**

* Python *3.14+* now duplicates processes with spawn over fork
    
* spawn duplicates the whole process space
    
* fork clones the process but doesn’t duplicate the thread space
    

The following *deadlock*s (on linux, &lt;py3.14)

```python
import threading
import time
from concurrent.futures import ProcessPoolExecutor

lock = threading.Lock()

def process_items(name):
    lock_id = id(lock)
    print(f"{name}: acquiring lock:{lock_id}")
    with lock:
        print(f"{name}: has lock:{lock_id}")
        time.sleep(1)
    print(f"{name}: released lock:{lock_id}")

if __name__ == "__main__":
    t = threading.Thread(target=process_items, args=("Thread",))
    t.start()

    time.sleep(0.1)

    with ProcessPoolExecutor() as e:
        e.submit(process_items, "Process")

--- output ---
Thread: acquiring lock:281473428672704                                                                         
Thread: has lock:281473428672704                                                                                                                                                            
Process: acquiring lock:281473428672704                                                                        
Thread: released lock:281473428672704
```

> `Process` deadlocks on a duplicated, **locked** `Thread` which isn’t released in it’s memory space

Exercise caution when forking prior to py3.14.

Happy coding!

## References

* [Spawn vs Fork - Tom Rutherford's Lightning Talk](https://www.youtube.com/watch?v=Uuhu-F05A7k&t=2305s)
    
* [The power and danger of os.fork() - Tom Rutherford](https://medium.com/@tmrutherford/the-default-method-of-spawning-processes-on-linux-is-changing-in-python-3-14-heres-why-b9711df0d1b1)
    
* [Claude on Fork vs Process](https://claude.ai/share/dc8a2d94-ab07-48b3-9e2f-23e01dc62b43)