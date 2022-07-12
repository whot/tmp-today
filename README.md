# tmp-today

This repository is a script that creates a date-stamped directory in
`$HOME/tmp/` and symlinks that directory as `$HOME/tmp/today`. The
corresponding systemd unit files create this directory every day.

A `$HOME/tmp/yesterday` symlink is also generated each day.

```
$ ls -l tmp/today
...
drwxr-xr-x. 1 whot whot    0 Jul  6 02:00 2022-07-06-Wed
drwxr-xr-x. 1 whot whot    0 Jul  7 02:00 2022-07-07-Thu
drwxr-xr-x. 1 whot whot    0 Jul  8 19:08 2022-07-08-Fri
drwxr-xr-x. 1 whot whot    0 Jul  9 02:00 2022-07-09-Sat
drwxr-xr-x. 1 whot whot    0 Jul 10 02:00 2022-07-10-Sun
drwxr-xr-x. 1 whot whot   60 Jul 11 19:56 2022-07-11-Mon
drwxr-xr-x. 1 whot whot   42 Jul 12 10:47 2022-07-12-Tue
lrwxrwxrwx. 1 whot whot   14 Jul 12 02:00 today -> 2022-07-12-Tue
lrwxrwxrwx. 1 whot whot   14 Jul 11 02:00 yesterday -> 2022-07-11-Mon
```

## Why a daily tmp directory?

The use for this `tmp/today` directory is a download-and-forget directory.
I have my browser's default directory set to that path, so anything I download
ends up there. Bugzilla attachments, test code, git clones of projects I need
to investigate but won't need for long all go in there.

There is no automatic cleanup of this directory, every so-often I just go
through and delete anything old enough that I won't need it anymore.

My setup pre-dates systemd (I used to have cron jobs for this) so I can
definitely say it is useful :)

## Installation

```
$ cp tmp-today $HOME/.local/bin/
$ cp tmp-today.service tmp-today.timer $HOME/.config/systemd/user/
$ systemctl --user enable tmp-today.service
$ systemctl --user enable --now tmp-today.timer
```

Note that the `tmp-today.service` has the path to the `tmp-today` script
encoded, if installing elsewhere the unit file must be adjusted accordingly.
