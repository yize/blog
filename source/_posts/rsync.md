---
title: rsync 如何同步到 root 的目录下？
date: 2017-03-30 18:18:34
tags:
---

# rsync 如何同步到 root 账户下？

```bash
rsync -chavzP --rsync-path="sudo rsync" --stats user@192.168.1.2:/ .
```
使用 `--rsync-path="sudo rsync"`

links： [http://unix.stackexchange.com/questions/92123/rsync-all-files-of-remote-machine-over-ssh-without-root-user/92125#92125](http://unix.stackexchange.com/questions/92123/rsync-all-files-of-remote-machine-over-ssh-without-root-user/92125#92125)