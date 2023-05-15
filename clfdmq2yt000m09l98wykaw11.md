---
title: "502s? 503s? oh my!"
datePublished: Sat Mar 18 2023 07:10:09 GMT+0000 (Coordinated Universal Time)
cuid: clfdmq2yt000m09l98wykaw11
slug: 502s-503s-oh-my
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/cGXdjyP6-NU/upload/9971fde4691a10da20df6422c97177c9.jpeg
tags: cloud, kubernetes, devops, system-architecture, k8s

---

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1679076187736/66cb267f-8ed0-48f6-8236-b12b5d9fe46e.png align="center")

Above (via [excalidraw](https://excalidraw.com/)) is our current architecture in the cloud.

When we built our dashboards to track `http_status` via our rev(erse)Proxies, we saw periodic spikes of [5XX errors](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes#5xx_server_errors), which were predominately 502s with a spattering of 503s.

These have to do with connectivity to and load on the apps running, where

* **502s, the respective revProxy's couldn't connect to any valid (upstream) apps**
    
* 503s, where apps were temporarily overloaded and not available (but connectable)
    

502s shouldn't happen with our current elastic(based on latency thresholds) k8s application setup which is configured for HA (high availability) with a minimum of 1-2 pods per.

503s shouldn't happen because the pods were set up with generously over-provisioned CPU/Memory.

But they were.

### 502s

Diving deeper into the logs we noticed that the respective response would come from different proxies across the system but was consistent within applications. This helped us to group issues based on distance from the app.

1. Closest (apps): Within the pod, there was a few configuration issues with the applications' dependent server.
    
2. Further: Had to do with configurations of k8s
    
    1. Sensitive pod scaling was dampened via `stabilizationWindowSeconds`
        
    2. (2.1) Led to the scaling of k8s cluster nodes which implicitly caused flux in the application pods being moved within nodes. To minimize this, `maxDisruptionBudget` was reduced from the default `50%` and the minimum number of pods per app where set to `4`
        

### 503s

(2.2) ensured that the minimum number of pods at any given time (due to node scaling) would be 2 at the expense of running a slightly under utilized cluster. This along with asymmetric up/down `stabilizationWindowSeconds` , help reduced this types of errors.

The powers at be are appeased, for now.