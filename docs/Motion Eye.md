### Security Camera
There are companies such as SimpliSafe, Ring, Blink, Arlo etc. The problem for me is that one does not know where the videos & images are captured, stored and potentially sold and analyzed. The consumer places these units throughout their home and the amount of data collected could be immense. Because of this  I wanted to see what solutions existed that could provide me the security I wanted + the privacy I needed. 

I have started working with [Raspberry Pi](https://www.raspberrypi.org/) in the past but I wanted to set up a project that was live and my own. I stumbled on two resources: [1](https://www.tomshardware.com/how-to/raspberry-pi-security-camera) & [2](https://greenido.medium.com/raspberry-pi-as-security-camera-with-motion-detection-2f1c2456b963). I hit a snag on both because they relied on CV which appears to be a virtual environment from within the pi. I could not get my `mkvirtualenvw` up and could not debug. 

I did further research and found how to install the [MotionEyeOS](https://github.com/motioneye-project/motioneye/wiki). 

## Steps Taken
You will need the following:
- Raspberry Pi Z W
- Camera (I used [this](https://www.amazon.com/Raspberry-Camera-Vision-IR-Cut-Longruner/dp/B07VSPSNL8/ref=sr_1_3?crid=1E0BEBRV845X4&keywords=raspberry+pi+z+w+night+vision+camera&qid=1649014027&sprefix=raspberry+pi+z+w+night+vision+camera%2Caps%2C55&sr=8-3))
- Power Cable ([Like this](https://www.amazon.com/Raspberry-Power-Supply-Adapter-Charger/dp/B08523DFR4/ref=sr_1_5?crid=1EBBZFXQMUNZY&keywords=raspberry+pi+z+w+power+cable&qid=1649014065&sprefix=raspberry+pi+z+w+power+cable%2Caps%2C48&sr=8-5))
- MicroSD

I pulled the MotioneyeOS [image](https://github.com/motioneye-project/motioneyeos/releases), the latest. Unzip and I placed that file on my desktop.

I then opened Balena Etcher from here [here](https://www.balena.io/etcher/),plugged in my microsd. Balena is easy in the sense that it will automatically detect the correct SD. I selected the image, the SD and then hit Flash.

I needed to get wifi into the OS, I did that via `wpa_supplicant.conf`. Opening a normal text editor I pasted the following into the document and renamed it `wpa_supplicant.conf`

```
country=us
update_config=1
ctrl_interface=/var/run/wpa_supplicant

network={
 scan_ssid=1
 ssid="MyNetworkSSID"
 psk="Pa55w0rd1234"
}
```
The file was then placed into the SD (no specific location). 

Once that was done, I plugged the SD into the Pi, provided power and saw the MotionEye OS loading. My wifi settings loaded and I was able to access the admin console. To do that, be sure to know the IP address of the raspberry Pi. It showed me the IP address in the loading screen, I typed that in and was taken to the login screen.

By default the credentials are username `admin` with no password. I logged in, set a password, changed my IP address and I was able to create my personal preferences on my camera. 

Note: this can only be accessed from within the local network, I do not need an advanced set up as of yet.

I was able to set up alerts to go to my personal email address. So that I would not need to always be logged in within my local network while away.

(This post would benefit from photos, I am working in- WIP)