# Video config exchange contract
Between iframe loading video and parent HTML containing the iframe.
Parent and child communicate over `window.postMessage` API. It is the child's responsibility to get the video configuration from the parent.
The responsibility lying with the child, takes care of cases when lazy loading of iframe could happen based on UX.

1. Parent registers a listener to receive message from child iframes.
2. Child registers a listener to receive message from parent to get the video configuration.
3. Child on load, shall POST message to parent, and wait for 1ms. Parent handles it in the listener created in (1).
4. Parent on receiving the message POSTs to the source iframe the video configuration. Child handles it in the listener created in (2).
5. Child sets up the videosjs object accordingly.

# Videojs config options supported
https://videojs.com/guides/options
```javascript
var videoConfig = {
    poster: "<image URL>", // (videojs option) this displays and is called for only when auto play is false.
    autoplay: "any", // (videojs option) 
    muted: true, // (videojs option) ensures the video plays muted. false does not guarantee playback with sound
    controlBar: { // (videojs option) controls visibility of options in the control bar
        playToggle: true, // (videojs option) play pause button
        remainingTimeDisplay: true, // (videojs option) 
        progressControl: { // (videojs option) 
            seekBar: true // (videojs option) 
        },
        fullscreenToggle: true // (videojs option) controls full screen button visibility
    },
    currentTime: 3, // (NOT a videojs option, custom built) start playing from 3 seconds mark from the beginning of the video. default behavior is 0 (from the start).
    playsinline: true //  (NOT a videojs option, custom built)https://css-tricks.com/what-does-playsinline-mean-in-web-video/. default behavior is as was false.
}
```

## Example: Code in parent
```javascript
<script>
    var videoConfig = {
        "autoplay": "any"
    };
    window.addEventListener("message", function (event) {
        switch(event.data) {
            case "video-config":
                event.source.window.postMessage(JSON.stringify(videoConfig), '*');
                break;
            default:
                break;
        }
    });
</script>
```
