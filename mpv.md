# mpv

## View camera input stream

To view the video feed from an attached video device, use:

```sh
mpv av://v4l2:<videodevice> --profile=low-latency --untimed
```

`<videodevice>` corresponds to the video device file, such as `/dev/video0`. Use
of `v4l2` requires that the Video 4 Linux userspace tools are available. (They
probably already are.)

### Stream `motionjpeg` from video device

```sh
mpv --demuxer-lavf-format=video4linux2 --demuxer-lavf-o-set=input_format=mjpeg av://v4l2:<videodevice>
```
