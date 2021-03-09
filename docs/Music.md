## Music
In the spirit of removing proprietary items to the extent that my knowledge and ability allow, I deiced to switch to the old fashion mp3 player. I chose the Sony Walkman as it had the features I liked:


+ Bluetooth
+ Small in size
+ Expandable Memory (256GB at the moment for my use)
+ Simple Interface 
+ Comes with music library for Windows, but could also use simple drag and drop of files to transfer music 
+ wide array of file types supported


## Problem
I had an old laptop that contained most of the music I've horded since middle school. I simply selected all the files and placed them in my SanDisk memory. About 730 of the files were corrupted, transferring over 0 bytes. 

# Solution 
After sorting the files by size, I then created .opus files to form my play list. I realized that I had several dozen .opus files that my mp3 could not read. I had to batch convert. All over the web I found different types of answers all that were too complex. My friend Txu attempted to help but I got a parse error, still need to debug this. But for now- to convert a directory of *.[m4a,opus,etc] files to another type of file using ffmpeg the following command works:

` for i in *.opus; do ffmpeg -i "$i" -b:a 192k "$i%.*}.mp3"; done`

The above command will take all .opus files and spit out individually named .mp3 files. 

*Please  do this in the directory where your files are*

## Clean up 
I recommend doing a simple `rm *.opus` to remove all excess opus files post convert. 