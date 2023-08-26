---
title: "vim -> neovim"
datePublished: Sat Aug 26 2023 10:07:28 GMT+0000 (Coordinated Universal Time)
cuid: cllruy910000809jr4jgq67pl
slug: vim-neovim
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/EJSaEnVvZcg/upload/8e015f35759659d8bc3edd8bf42f4553.jpeg
tags: vim, neovim, vi, nvim, kentucky

---

I've finally made the move after being introduced to `vim` back in at the [Univeristy of Kentucky](https://www.uky.edu/) (Go Big Blue!) in the last millennium.

Sluggishness is my pet peeve and was the motivation for moving because `vim` loaded with all my plugin's was painfully slow on some of my 10k+ lines of source files that I had to work on and [tabnine](https://www.tabnine.com/) AI completion support was depreciated.

Another reluctance was not knowing the effort involved in supporting my plugins and language servers that I relied on which had become ingrained. I had no clue what updates would I need to make to my current [.vimrc](https://github.com/danwald/config/blob/d929dcf1c78019cb948a12cd375f16dd0758e6d1/.vimrc) to work.

However, I got it mostly running in a little over an hour with minor tweaks to my original [.vimrc](https://github.com/danwald/config/blob/d929dcf1c78019cb948a12cd375f16dd0758e6d1/.vimrc) (still using `vimscript`) and moving to `Plug` manager which was used in the [example](https://unkertmedia.com/how-to-migrate-from-vim-to-neovim/) I followed.

It's night and day faster with no discernible lag for the huge files I was seeing previously with mostly everything working as it was before (the git blame pop script complains with an unknown function error). See the recommendations for some nifty new things.

### Steps involved:

1. cp [init.vim](https://github.com/danwald/config/blob/d929dcf1c78019cb948a12cd375f16dd0758e6d1/init.vim) -&gt;`$HOME/.config/nvim/init.vim` allowing use of your current vimscript `.vimrc`
    
2. Install [Plug](https://github.com/junegunn/vim-plug) Plugin manager
    
3. Inject any lua related config (LS/tabnine) in your `.vimrc` block as
    

```bash
lua << EOF
...
EOF
```

1. Install your plugin's via `nvim +PlugInstall +qall`
    
2. update your aliases `alias vim=nvim` `alias vi=nvim`
    

And that's pretty much it. I hope this helps. Onwards and upwards.

### Recommendations:

* run `:checkhealth` in `nvim` command and fix issues
    
* [mason](https://github.com/williamboman/mason.nvim) to manage `nvim` package which manages language servers
    

### Future improvements:

I plan on porting my [.vimrc](https://github.com/danwald/config/blob/d929dcf1c78019cb948a12cd375f16dd0758e6d1/.vimrc) to `lua`, so keep tabs on it.