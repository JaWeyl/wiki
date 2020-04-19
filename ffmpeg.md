# Genereal
- ```Containers```: ```.avi, .mov, .mp4```
  - contains video data, audio data, timecode and codec instructions
- ```Codec``` is software that is used to compress and decompress video and audio data 
  - For example ```h.264, mpeg2```
  - given a container you do not know directly which codec instructions it is using
- ```Formats``` are specifications for video caputre and delivery
  - ```AVCHD``` for example specifies the ```h.264`` codec
  
# FFMPEG Basic Synatx
- Convert ```fileformat```:<br> ```ffmpeg -i <input-name.mov> <output-name.mp4>```

# Specifying Quality
Note that lower values of the *constant rate factor* (CRF) specify a higher *bitrate* therefore the output-file will be larger. 
- For ```*.mp4``` files:<br> ```ffmpeg -i <input-name> -c:v h264 -c:a aac -crf 20 <output-name>```
  - ```-c:v``` compress video with codec *h264*
  - ```-c:a``` compress audio with codec *aac*
  - ```-crf``` sets the CRF (sane values are in between 18 and 28)

# To Specify Exact Bitrates
- For ```Video```:<br> ```ffmpeg -i <input-name> -b:a bit-rate <output-name>```
- For ```Audio```:<br> ```ffmpeg -i <input-name> -b:v bit-rate <output-name>```
  - Compute the target size in bits
  - Get the video length in seconds
  - the desired bit rate is equalt to target-size divided by video-length

# Volume Tweak
- Decrease or increase audio volume:<br>```ffmpeg -i <input-name> -filter:a "volume=2" <output-name>```
  - ```-filter:a``` targets the audio
  - ```"volume=2``` specifies the volume multiplyer

# Channel Remapping
- Map the ```audio``` from left to both channels:<br>```ffmpeg -i <input-name> -filter:a "channelmap=0-0|0-1" <output-name>```
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
