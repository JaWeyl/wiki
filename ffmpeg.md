# FFMPEG Basic Synatx
- Convert ```Fileformat```: ```ffmpeg -i <input-name> <output-name>```

# Specifying Quality
Note that lower values specify a higher *bitrate* therefore the output-file will be larger. 
- For ```*.avi```: ```ffmpeg -i <input-name> -q quality <output-name>```
- For ```*.mp4```: ```ffmpeg -i <input-name> -crf quality <output-name>>```

# To Specify Exact Bitrates
- For ```Video```: ```ffmpeg -i <input-name> -b:a bit-rate <output-name>```
- For ```Audio```: ```ffmpeg -i <input-name> -b:v bit-rate <output-name>```

# Volume Tweak
- Target the ```a := audio``` by specifying a ```volume multiplyer```: ```ffmpeg -i <input-name> -filter:a "volume=2" <output-name>```

# Channel Remapping
- Map the ```audio``` from left to both channels: ```ffmpeg -i <input-name> -filter:a "channelmap=0-0|0-1" <output-name>```
  - the left channel is ```0``` and the right channel is ```1````
  - ```0-0``` map input left to output left
  - ```0-1``` map input left to output right

# Cropping
- Target the ```v := video``` by specifying the area to crop:<br> ```ffmpeg -i <input-name> -filter:v "crop=w=640:h=480:x=100:y=200" <output-name>```
  - ```x,y``` specify the top-left corner

# Scaling
Target the ```v := video``` by specifying the scale factor:<br>
- ```ffmpeg -i <input-name> -filter:v "scale=w=640:h=480" <output-name>```
  - enforce dimensions
- ```ffmpeg -i <input-name> -filter:v "scale=w=640:h=-1" <output-name>```
  - Proportional scaling