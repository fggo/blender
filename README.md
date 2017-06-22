* [0. Installation](#0-installation)
* [1. Setting defaults](#1-setting-defaults)
* [2. Import video](#2-import-video)
* [3. Video sequencer & rendering](#3-video-sequencer-rendering)
* [4. Select, Grab, Cut strips](#4-select-grab-cut-strips)
* [5. How Channels work](#5-how-channels-work)
* [6. Mixing multiple video resolutions](#6-mixing-multiple-video-resolutions)
* [7. Preview Performance Boost - Video Proxy](#7-preview-performance-boost-video-proxy)
* [8. Fast Navigation with Timeline or Markers](#8-fast-navigation-with-timeline-or-markers)
* [9. Playback Misconceptions and Refresh Sequencer](#9-playback-misconceptions-and-refresh-sequencer)
* [10. Precise strip placement or box zoom](#10-precise-strip-placement-or-box-zoom)
* [11. Importing images (overlay resize roate)](#11-importing-images-overlay-resize-roate)
* [12. Video overlay and Transform strip dependency](#12-video-overlay-and-transform-strip-dependency)
* [13. Fade-In Fade-Out & Set End frame fast](#13-fade-in-fade-out-set-end-frame-fast)
* [14. Video and Audio Crossfades & Frame Range Repeat](#14-video-and-audio-crossfades-frame-range-repeat)
* [15. Wipe Video Transitions-Star Wars Style](#15-wipe-video-transitions-star-wars-style)
* [16. Color Balance, Brightness, Contrast, Hue(Strip Modifiers)](#16-color-balance-brightness-contrast-hue-strip-modifiers)
* [17.1 Rendering H.264 video and Testing bitrate](#17-1-rendering-h-264-video-and-testing-bitrate)
* [17.2 Best Render with HandBrake and Lossless Rendering](17-2-best-render-with-handbrake-and-lossless-rendering)
* [18. Intro to Keyframes, Graph Editor, Dope Sheet, Audio Fade](18-intro-to-keyframes-graph-editor-dope-sheet-audio-fade)
* [19. Pan & Scan | Convert Letterbox to HDTV Full Frame | Jump Keyframes](19-pan-scan-convert-letterbox-to-hdtv-full-frame-jump-keyframes)
* [20. Tell a Story with a Photo [Ken Burns Effect]](20-tell-a-story-with-a-photo-ken-burns-effect)
* [21. Face Blurring / Masking with UV-Image Editor / Auto-Keyframe](#21-face-blurring-masking-with-uv-image-editor-auto-keyframe)
* [22. 3D Viewport / Outliner / Subtitles with Scene Strip](#22-3d-viewport-outliner-subtitles-with-scene-strip)
* [23. My Subtitle Template / Image Separate feature](#23-my-subtitle-template-image-separate-feature)
* [New Blender Feature: TEXT Effect Strip in VSE (Available 2.76+)](#new-blender-feature-text-effect-strip-in-vse-available-2.76)
* [24. Speed up & Slow Down Audio/Video | Snap Strips option](#24-speed-up-slow-down-audio-video-snap-strips-option)
* [25. Intro to Meta Strips / Add Effects to Group of Strips](#25-intro-to-meta-strips-add-effects-to-group-of-strips)
* [26. Keyframes can be easy /A Versatile fade in](#26-keyframes-can-be-easy-a-versatile-fade-in)
* [27. Super Fast Video Rendering with Render Script](#27-super-fast-video-rendering-with-render-script)

# 0. Installation
```
sudo add-apt-repository ppa:thomas-schiex/blender
sudo apt-get update
sudo apt-get install blender
```

# 1. Setting defaults
```
properties - dimensions - Render Presets(HDTV) - Frame Rate
properties - ouput/encoding - set location and format Xvid(video), RGB, mp3(audio)
playback - Audio - check Scrubbing, AV-sync, Frame Dropping
view - Show Offsets
file - Save Startup File(save default settings)
file- user preference - memory cache limit 10GB(10000MB)
```

# 2. Import video
```
'shift+left' sets current frame to 1
add - movie (use shift + a)
properties - set frame rate for audio video sync
strip - set render size
```

# 3. Video sequencer & rendering
```
click mouse wheel to move around
'Home' key to fit the channel length
```

```
frame - set start/end frame (cursor on timeline and press S/E)
properties - click Animation - it will render the output as another video file
```

# 4. Select, Grab, Cut strips
```
B box select
'shift+right click' to select multiple audio and video

K/Shift+K (soft/hard cut)

G grab
G-x
G-y
```

# 5. How Channels work
```
strips with higher channel #, has higher priority.
Exception: channel 0 has the highest priority.
```

# 6. Mixing multiple video resolutions
1. differing resolutions: set resolution to higher one
  - higher resolution video - strip - set render size
  - smaller resolution video - property - image offset (fix distorted ratio)
  - smaller resolution video - add - effect strip - transform - uniform scale
  - hide original strip - strip - mute strips(h)
2. differing frame rates: use [ffmpeg](https://www.ffmpeg.org/ffmpeg.html) and check related [issue](https://stackoverflow.com/questions/32931685/the-encoder-aac-is-experimental-but-experimental-codecs-are-not-enabled)
```
ffmpeg -i input.mp4 -strict -2 -r 30 output.mp4
```

# 7. Preview Performance Boost-Video Proxy
```
click the strip - property - set Proxy/Timecode 50%
strip - rebuild proxy and timecode indices
video preview window - view - properties - proxy render size - select proxy size %
do the same for every strip
```

# 8. Fast Navigation with Timeline or Markers
One can check both timeline and video sequencer
```
Marker - add/rename/delete marker
```

# 9. Playback Misconceptions and Refresh Sequencer
Preview playback window fps is not representative of the final render frame rate.
```
Refresh Sequencer: prerendering to sync frame rate
Mpeg preseek set to 50 and click Refresh Sequencer : improved preview playback (more stable fps in preview window)
```

# 10. Precise strip placement or box zoom
```
B G-x press shift to move frames precisely
Shift+B to zoom in and Home to return
```

# 11. Importing images (overlay resize roate)
import image
```
add - image
image properties - image offset
image properties - blend set to 'over drop' (non-transparent image)
image properties - blend set to 'alpha over' (transparent image)
```

change image size
```
add - effect strip - transform - alpha over - adjust position x,y - uniform scale rotation
```

# 12. Video overlay and Transform strip dependency
```
add - movie
select added strip - property - image offset
property - blend - over drop
add - effect strip - transform - uniform scale - adjust position x, y
```

# 13. Fade-In Fade-Out & Set End frame fast
set frame start & end
```
page down - mouse cursor on timeline - S
page up - mouse cursor on timeline - E
```

fade in & out
```
start of the movie
add - effect strip - color - property - adjust length
fade from color strip to video strip(start)
    1st select color strip
    2nd select video strip
    add - effect strip - gamma cross

end of the movie(few seconds away from the end)
add - effect strip - color - property - adjust length
fade from video strip to color strip(end)
    1st select video strip
    2nd select color strip
    add - effect strip - gamma cross
```

# 14. Video and Audio Crossfades & Frame Range Repeat
soft cut allows readjusting strip
```
K soft cut both audio and video
put strips in different channels so that they they intercept
select 1st and 2nd video - add - effect strip- gamma cross
select 1st and 2nd audio - strip - crossfade sounds
```

# 15. Wipe Video Transitions-Star Wars Style
```
K soft cut
put strips in different channels so that they intercept
select 1st and 2nd - add - effect strip - wipe
select wipe strip - property - effect strip - transition - options are double, single, clock - set blur width and angle
```

# 16. Color Balance, Brightness, Contrast, Hue(Strip Modifiers)
change strip 
```
select strip - properties - modifiers - add strip modifier
```

or add adjustment layer
```
select strip - add - effect strip - adjustment layer
select new strip - properties - modifiers - add strip modifier
```

# 17.1 Rendering H.264 video and Testing bitrate
set defaults
```
click render tab && select display as Keep UI
strip - set render size
set frame rate
```

set other options before rendering
```
output path
output video format H.264
output RGB

encoding format - select container (mpeg-4)
encoding codec H.264 (H.264 video inside mpeg-4 extension container)
encoding bitrate <=10000 (higher bitrate higher quality video and bigger file size)
encoding GOP, group of pictures, size. typically fps/2
  higher GOP sizes produce smaller files, but can be harder to playback on lower end pc.
encoding audio codec : AAC(highest quality and compressed), pcm flag(high quality and uncompressed), mp3
encoding audio bitrate for AAC <=384 && >=160
encoding audio bitrate for mp3 <=384

Recording audio khz sample rates differs
scene - audio - format - stereo
scene - audio - rate 48000 (48khz); high quality audio might have higher

select portion of the video using S/E and click Animation to render to see if the bitrate will give enough quality

click Animation to test rendering the chosen frame range and one can change bitrate and test agin
```

# 17.2 Best Render with HandBrake and Lossless Rendering
if you are not be pleased with rendered quality or file size, use advanced encoding by ouputing video with highest quality and encoding with handbrake

output video project as lossless format and use handbrake which can be used to shirnk volume while maintaining quality.

lossless video: there are 3 lossless options
- HuffYUV renders fastest but files are huge
- FFmpeg video codec #1 (FFV1) renders slowest but files are smaller
- H.264(with lossless ouput check marked) renders fast and files are small
- all lossless settings ignore bitrate setting
```
go to render tab
encoding - format - avi
encoding - codec - H.264
encoding - check lossless option marked
```

lossless audio
```
encoding - audio codec - PCM
audio sample rate default 44.1KHZ 
  you can change to a higher one by doing:
  scene - audio - type 'rate' e.g. 48000
  handbrake only supports up to 48KHZ
```

set frame range and click 'Animation' to render
```
S/E to set frame start/end
click Animation
```

install Handbrake in Ubuntu
```
sudo add-apt-repository ppa:stebbins/handbrake-releases
sudo apt-get update
sudo apt install handbrake-gtk handbrake-cli
```

settings in handbrake for encoding
```
file - preference - uncheck "use ipod/itunes friendly .m4a"
```

# 18. Intro to Keyframes, Graph Editor, Dope Sheet, Audio Fade
