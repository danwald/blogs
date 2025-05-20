---
title: "Publish to pypi via UV & Github workflows"
datePublished: Tue May 20 2025 17:07:45 GMT+0000 (Coordinated Universal Time)
cuid: cmawroyrt001009lbc3ld1pjx
slug: publish-to-pypi-via-uv-and-github-workflows
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/IPx7J1n_xUc/upload/2631dfdbddee96982f885b996c7d0710.jpeg
tags: github, workflow, git, pypi, uv

---

I’ve incorporated [uv](https://github.com/astral-sh/uv) into my development workflow. It’s a swiss army knife that replaces venv, pip, pipx, build, twine and others that i’m yet to discover.

You can even run [standalone scripts](https://gist.github.com/danwald/082d0e87974acd6d378257d0f7a1f3d0): `uv run https://danwald.me/assets/uv_cowsay.py`

I wanted to publish to pypi using a Github workflow triggered by a release. I heavily borrowed from [this article](https://www.andrlik.org/dispatches/til-use-uv-for-build-and-publish-github-actions/) to create [this](https://github.com/danwald/butterfly/blob/main/.github/workflows/python-publish.yml) publishing workflow. The only difference is that uses the recommended authorization of [a trusted publisher](https://docs.pypi.org/trusted-publishers/adding-a-publisher/) rather that a secret. Make sure the pypi’s *project name* and github’s *repository and workflow* names are legit and you’re GTG.

Happy hackin’

## References

* [UV](https://github.com/astral-sh/uv)
    
* [Gist:uv\_cowsay.py](https://gist.github.com/danwald/082d0e87974acd6d378257d0f7a1f3d0)
    
* [Daniel’s Andrlik](https://bsky.app/profile/andrlik.org) [article](https://www.andrlik.org/dispatches/til-use-uv-for-build-and-publish-github-actions/)
    
* [UV to publish packages](https://docs.astral.sh/uv/guides/package/#publishing-your-package)
    
* [Pypi’s trusted publisher](https://docs.pypi.org/trusted-publishers/adding-a-publisher/)