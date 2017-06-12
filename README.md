* [1. Setting defaults](#setting-defaults)
* [2. Import video](#import-video)
* [3. Video sequencer & rendering](#video-sequencer-rendering)
* [4. Select, Grab, Cut strips](#select-grab-cut-strips)
* [5. How Channels work](#how-channels-work)
* [6. Mixing multiple video resolutions](#mixing-multiple-video-resolutions)
* [7. Preview Performance Boost - Video Proxy](#preview-performance-boost-video-proxy)

# Setting defaults
Video Editing
```
properties - Dimensions - Render Presets(HDTV 1080p) - Frame Rate
properties - ouput - set location and format Xvid, RGB, mp3(audio)
playback-Audio scubbing, AV-sync, Frame Dropping
view - Show Offsets
File - Save Startup File
File- user preference - memory cache limit 10GB(10000MB)
```

# Import video
current frame set to 1 before import
```
Add-Moive
properties-change Frame rate so that both audio and video have same frames. 
change resoltuion to sync with original : right click video channel. Strip - Set render size
```

# Video sequencer & rendering
move around
```
mouse wheel to move around
'Home' to fit the channel length
```

select portion and render output
```
Frame - set start/end frame
properties - Animation
```

# Select, Grab, Cut strips
```
Box select(B) or use Shift key to select
Strip - soft/hard cut (K/Shift+K)

Select portion and grab using 'G' key
G-x
G-y
```

# How Channels work
```resolution 
The higher channel # has higher priority. Exception is channel 0 which has the highest priority
```

# Mixing multiple video resolutions
1. differing resolutions: resolution set to higher one
  import two videos && click the strip with bigger resolution - Strip - "set render size"
  then the images of the smaller resolution will look distorted
  to resolve it, click the strip, on the right side panel click "Image Offset" in Strip Input and adjust x and y.
  To avoid empty space created by this result, you can use transform script to zoom it.
  Click strip - Add - Effect Strip - Transform
  Right click the original and hide: Strip - Mute Strips(H)
  Select the newly created Transform Strip - look at properties of Transform - Uniform Scale.
  Now It's all set. Lastly you can cut the highest priority strip. e.g. from 6:00 ~ 12:00 out of 12-min video, by selecting
  all three(including the muted) - Left Click time line to be cut - Click Shift +K - Select the cut part - Click x to erase
2. differing frame rates: ffmpeg
[ffmpeg documentation](https://www.ffmpeg.org/ffmpeg.html) check [issue](https://stackoverflow.com/questions/32931685/the-encoder-aac-is-experimental-but-experimental-codecs-are-not-enabled) 
```
ffmpeg -i Shooting\ Stars\ -\ Bridge.mp4 -strict -2 -r 29.97 Shooting\ Stars\ -\ Bridge2.mp4
```

# Preview Performance Boost-Video Proxy
