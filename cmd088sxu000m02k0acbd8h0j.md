---
title: "Nested ModuleNotFound"
datePublished: Sat Jul 12 2025 12:33:48 GMT+0000 (Coordinated Universal Time)
cuid: cmd088sxu000m02k0acbd8h0j
slug: nested-modulenotfound
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/eBkEJ9cH5b4/upload/af1b4093d0ce499e388ab416dfcbc942.jpeg
tags: python, virtual-environment, modulenotfounderror, module-not-found

---

`sys.path` is a list of directories (or zip archives) to find imports. “The first entry in the module search path is the directory that contains the input script … Otherwise it’s the current directory”[\*](https://docs.python.org/3/library/sys_path_init.html)

With the following project layout:

```bash
|- main.py #from tools import tools. OK!
|- tools # module
   | __init__.py
   | tools.py
|- scripts
   | __init__.py
   | use_tools.py #from tools import tools **ModuleNotFoundError: No module named 'tools'
|- .venv #virtual env directory
```

`main.py` and `scripts/use_tools.py` both import from `tools/tools.py`

However only `python scripts/use_tools.py` results in a `ModuleNotFoundError`. Below are the search paths when executing the script.

```bash
sys.path = [
    '~/sandbox/courses/langchain/ice_breaker/scripts', #directory of input script
    '~/.asdf/installs/python/3.13.2/lib/python313.zip', #stdlib
    '~/.asdf/installs/python/3.13.2/lib/python3.13', #stdlib
    '~/.asdf/installs/python/3.13.2/lib/python3.13/lib-dynload', #stdlib
    '~/sandbox/courses/langchain/ice_breaker/.venv/lib/python3.13/site-packages' #venv
]
```

Python will search for the `tools` module in

1. current working directory of the source file i.e. `scripts`
    
2. check `PYTHONPATH`
    
3. lastly, it will check python installation specific directories and activated virtualenv paths for standard-libs and site-packages (always use one)
    

To fix the issue you can use [PYTHONPATH](https://docs.python.org/3/using/cmdline.html#envvar-PYTHONPATH) environment variable to add additional directories to `sys.path`.

Here it’s being done in the virtual environment’s `activate` script

```bash
# .venv/bin/activate 

deactivate () {
    # reset old environment variables
    if [ -n "${_OLD_VIRTUAL_PYTHONPATH:-}" ] ; then
        PATH="${_OLD_VIRTUAL_PYTHONPATH:-}"
        export PATH
        unset _OLD_VIRTUAL_PYTHONPATH
    fi
}

_OLD_VIRTUAL_PYTHONPATH="$PYTHONPATH"
export PYTHONPATH="$PWD:$PYTHONPATH"
```

May your modules now be found.

Happy hackin’w

## References

* [The initialization of the sys.path module search path](https://docs.python.org/3/library/sys_path_init.html)
    
* [PYTHONPATH](https://docs.python.org/3/using/cmdline.html#envvar-PYTHONPATH)