# ffmpeg

converting vidoes e.g. for Video Devices for Car with low-qualtiy

hint: http://www.sokesi.com/forum/viewtopic.php?f=13&t=347




```bash
 dnf -y install https://download1.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm
 dnf -y install https://download1.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm
 dnf -y install ffmpeg
```

convert a video for car-tv
```bash
 ffmpeg -i file.mp4 -filter:v scale=720x576 file_720x576.mpg # or ...vob
```

in a loop ...
```
for file in $(ls *mp4)
do 
	echo "ffmpeg -i $file -filter:v scale=720x576 ${file}.mpg" >> status.log
	time ffmpeg -i $file -filter:v scale=720x576 ${file}.mpg > /dev/null 2>&1
done 

```

