### Why autoplay playes muted
This video player leverages `videojs` for playback of videos, and facilitate web-optimised, adaptive bitrate streaming.
Following are excerpts from the recommendations videojs has for autoplay. The main article can be found here - https://videojs.com/blog/autoplay-best-practices-with-video-js/
* Never assume autoplay will work.
* It is worth noting the autoplay policies of each browser, as linked here https://videojs.com/blog/autoplay-best-practices-with-video-js/#autoplay-policies-in-the-big-browsers.
* Summarily, **browsers are restrictive of autoplaying videos as "muted"**. They are free (as as per our experiments) mostly have auto played videos as "muted" (even when the option passed was to play the video non muted)