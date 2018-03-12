# dd

## Track transfer progress

### Option 1: dd status=progress

```
sudo dd if=source of=dest status=progress
```


### Option 2: kill

One-shot
```
sudo kill -USR1 $(pgrep ^dd)
```

Repeat on 5 second interval
```
watch -n5 'sudo kill -USR1 $(pgrap ^dd)'
```
