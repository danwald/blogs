---
title: "Record your work"
datePublished: Sun Feb 18 2024 17:45:06 GMT+0000 (Coordinated Universal Time)
cuid: clsrssplm000i08ic5qz17vbs
slug: record-your-work
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/xzPMUMDDsfk/upload/c4a637182dcea1ff82d2e735f0af20ee.jpeg
tags: zsh, logging, career, oh-my-zsh

---

I saw the pertinent video by [Chris Albon](https://twitter.com/chrisalbon) on [Don't do invisible work](https://www.youtube.com/watch?v=HiF83i1OLOM) at '22's [normconf](https://twitter.com/normconf). He evangelizes broadcasting your work to know what value one provides which helps with career progression. Given we are forgetful animals, we need to physically log work so that we know what to broadcast.

The following snip via [this](https://github.com/danwald/omz-utils/blob/3494028e838455c67f20a631c1c5664b695439dd/omz-utils.plugin.zsh#L173) is a command-line (zsh) utility that lets you record work items:

```bash
rw() {
    WORK_FILE="${WORK_FILE:-$HOME/.work.log}"
    BACKUP_FILE="$WORK_FILE.bck"
    # head insert into backupfile
    echo "`date +'%Y-%m-%d'` $@" | cat - $WORK_FILE > $BACKUP_FILE
    # preserve simlink
    cat $BACKUP_FILE > $WORK_FILE
}
```

> `~/.work.log -> ~/Google Drive/.work.log` symlinked off machine

Improvements:

* have **sections** to log multiple work streams
    
* sqllite instead of POT
    
* optionally specify time spent in fractional hours from time of insertion