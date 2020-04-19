# FFMPEG Basic Synatx
- Convert ```Fileformat```: ffmpeg -i ```input-name``` ```output-name```

# Specifying Quality
- For ```*.avi```: ffmpeg -i ```input-name``` -q ```quality``` ```output-name```
- For ```*.mp4```: ffmpeg -i ```input-name``` -crf ```quality``` ```output-name```

# To Specify Exact Bitrates
- For ```Video```: ffmpeg -i ```input-name``` -b:a ```bit-rate``` ```output-name```
- For ```Audio```: ffmpeg -i ```input-name``` -b:v ```bit-rate``` ```output-name```