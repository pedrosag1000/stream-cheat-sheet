Stream a test stream with UDP protocol

```gst-launch-1.0 videotestsrc ! openh264enc ! rtph264pay config-interval=10 pt=96 ! udpsink host=127.0.0.1 port=5000```

Play test stream with UDP

```gst-launch-1.0 udpsrc port=5000 ! application/x-rtp,media=video,clock-rate=90000,encoding-name=H264,payload=96 ! rtph264depay ! avdec_h264 ! autovideosink```


stream RSTP by this command:

```gst-launch-1.0 rtspsrc location= rtsp://admin:Admin1401@192.168.1.64:554/streaming/channels/103 latency=10 ! decodebin ! autovideoconvert ! x264enc tune=zerolatency ! rtph264pay ! udpsink host=127.0.0.1 port=8123```

consume and play UDP stream by this command:

```gst-launch-1.0 udpsrc address=127.0.0.1 port=8123 ! application/x-rtp,media=video,clock-rate=90000,payload=96 ! rtph264depay ! avdec_h264 ! autovideosink```


Start stream server from /dev/video*:

```gst-launch-1.0 v4l2src device=/dev/video0 ! decodebin ! autovideoconvert ! x264enc tune=zerolatency ! rtph264pay ! udpsink host=127.0.0.1 port=8123```

Show stream : 
```gst-launch-1.0 -v udpsrc port=8123 caps = "application/x-rtp, media=(string)video, clock-rate=(int)90000, encoding-name=(string)H264, payload=(int)96" ! rtph264depay ! decodebin ! videoconvert ! autovideosink sync=false```
