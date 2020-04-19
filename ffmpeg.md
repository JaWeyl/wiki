# Genereal
- **Containers**: ```.avi, .mov, .mp4```
  - contains video data, audio data, timecode and codec instructions
- **Codec** is software that is used to compress and decompress video and audio data 
  - For example ```h.264, mpeg2```
  - it is shortcut for **Co**pressor + **Dec**ompressor
  - given a container you do not know directly which codec instructions it is using
- **Formats** are specifications for video caputre and delivery
  - **AVCHD** for example specifies the ```h.264`` codec
  
# FFMPEG Basic Synatx
- Convert **fileformat**:<br> ```ffmpeg -i <input-name.mov> <output-name.mp4>```

# Specifying Quality
Constant rate factor (CRF) is an encoding mode that adjusts the bitrate up or down to achieve a selected quality level rather than a specific data rate
The Constant Rate Factor (CRF) is the default quality (and rate control) setting for the x264 and x265 encoders. You can set the values between 0 and 51, where lower values would result in better quality, at the expense of higher file sizes. Higher values mean more compression.  A change of ±6 should result in about half/double the file size. Lower CRF values result in a higher bitrate (amount of data encoded per sec). CRF is a “constant quality” encoding mode specified by a quantization parameter which defines how much information to discard from a given block of pixels. This typically leads to a hugely varying bitrate over the entire sequence. The human eye perceives more detail in still objects than when they’re in motion. Because of this, a video encoder can apply more compression (drop more detail) when things are moving, and apply less compression (retain more detail) when things are still. For example, if you set CRF 23, you may end up with 1,500 kBit/s for one source, but only 1,000 kBit/s for the other. They should look the same in terms of quality, though. With CRF, you are saying “use whatever bitrate is necessary to preserve this much detail.” It’s not a 1-to-1 thing. [source](https://slhck.info/video/2017/02/24/crf-guide.html)

- For ```*.mp4``` files:<br> ```ffmpeg -i <input-name> -c:v h264 -c:a aac -crf 20 <output-name>```
  - ```-c:v``` compress video with codec *h264*
  - ```-c:a``` compress audio with codec *aac*
  - ```-crf``` sets the CRF (sane values are in between 18 and 28)

# To Specify Exact Bitrates
- For **Video**:<br> ```ffmpeg -i <input-name> -b:a bit-rate <output-name>```
- For **Audio**:<br> ```ffmpeg -i <input-name> -b:v bit-rate <output-name>```
  - Compute the target size in bits
  - Get the video length in seconds
  - the desired bit rate is equalt to target-size divided by video-length

# Volume Tweak
- Decrease or increase audio volume:<br>```ffmpeg -i <input-name> -filter:a "volume=2" <output-name>```
  - ```-filter:a``` targets the audio
  - ```"volume=2``` specifies the volume multiplyer

# Channel Remapping
- Map the **audio** from left to both channels:<br>```ffmpeg -i <input-name> -filter:a "channelmap=0-0|0-1" <output-name>```
  - the left channel is ```0``` and the right channel is ```1````
  - ```0-0``` map input left to output left
  - ```0-1``` map input left to output right

# Cropping
- Specifying the area to crop:<br> ```ffmpeg -i <input-name> -filter:v "crop=w=640:h=480:x=100:y=200" <output-name>```
  - ```v := video``` targets the video 
  - ```x,y``` specify the top-left corner

# Scaling
- Enforce video dimensions:<br>```ffmpeg -i <input-name> -filter:v "scale=w=640:h=480" <output-name>```
  - ```v := video``` targets the video
- Proportional scaling:<br>```ffmpeg -i <input-name> -filter:v "scale=w=640:h=-1" <output-name>```
  -```h=-1``` sets the hight according to aspect ratio
