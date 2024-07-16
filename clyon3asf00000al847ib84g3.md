---
title: "Upgrade asdf's python"
datePublished: Tue Jul 16 2024 16:40:18 GMT+0000 (Coordinated Universal Time)
cuid: clyon3asf00000al847ib84g3
slug: upgrade-asdfs-python
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/xGtHjC_QNJM/upload/76eb3a3d2a50dd8e2f1328ffec451e66.jpeg
tags: python, upgrade, asdf, pip, pipx

---

It's a fairly straight forward process to upgrade a python version in [asdf](https://asdf-vm.com/guide/getting-started.html).

```bash
asdf update
asdf install python <version>
asdf global python <version>
```

However I kept running into the follow when installing [pipx](https://github.com/pypa/pipx)

```bash
pip install pipx
ERROR: Could not find an activated virtualenv (required).
```

> ensure pip uses the right python via `alias pip='python -mpip'`

After a little digging, I figured out the self inflicted error.

It's always a good idea to avoid install python packages to your global i.e: not in a virtual environment. Do this by adding it to your pip config file via

```bash
pip config set global.require-virtualenv True
```

`pipx` does this for you by default, but it needs to be installed in your "global" (actually `asdf`'s) python. The work around is to temporarily disable it to install `pipx`.

I'm documenting here for anyone else that run's into this and for my future self.

### References

* [https://asdf-vm.com/](https://asdf-vm.com/) - multiple runtime version manager
    
* [https://github.com/pypa/pipx](https://github.com/pypa/pipx) - manager for isolated python applications