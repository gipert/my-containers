# gerda-tgsend

With Singularity:
```
alias gerda-notify='singularity exec \
    --hostname `hostname`
    -b telegram-send.conf:/etc/telegram-send.conf
    /path/to/gerda-tgsend.simg gerda-notifier'

gerda-notify -l error "the task has failed."
```
