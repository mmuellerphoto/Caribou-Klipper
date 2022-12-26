## Raspberry PI Splashscreen HowTo

###### This HOWTO is highly inspired by [Florian Mueller](https://florianmuller.com/topic/technology)

&nbsp;

First let's get rid of the ugly rainbow screen that appears when the Pi is switched on. Edit the config.txt:

`sudo nano /boot/config.txt`

Add at the end of this file:

`disable_splash=1`

<kbd>STRG</kbd>+<kbd>X</kbd> to save the file and confirm overwriting the file with <kbd>Y</kbd>.

&nbsp;

Next is the cmdline.txt - here we change the output of the console.

**WARNING: Editing cmdline.txt wrong will break your Raspberrys boot up. Always ensure that you have everything in ONE LINE!**
+ All parameters are split by 1 space!
+ Nothing should be split up into two lines

`sudo nano /boot/cmdline.txt`

In this file we find parameters, all in one line. Its important that you add the following exactly at the end of the existing line 1, starting with a space between the exisitng and new. So lets add:

```consoleblank=1 logo.nologo quiet loglevel=0 plymouth.enable=0 vt.global_cursor_default=0 plymouth.ignore-serial-consoles splash fastboot noatime nodiratime noram```

<kbd>STRG</kbd>+<kbd>X</kbd> to save the file and confirm overwriting the file with <kbd>Y</kbd>.

&nbsp;

To be able to use a video or an image as a splash screen, we need to install software. Either you can use **omxplayer** or **vlc**. Installation:

`sudo apt-get update`

For OMXPlayer: `sudo apt-get install omxplayer`

For VLC: `sudo apt-get install vlc`

&nbsp;

Now we have to define what to play on boot. Edit rc.local:

`sudo nano /etc/rc.local`

Upload the image or video you want to use as a splash screen on your Pi.

In rc.local we need to add some lines right before `exit 0`. Replace the path to the image or video with your path to the file(s) ... of course ... ;o)

`dmesg --console-off`

For OMXPlayer: `omxplayer /home/pi/video/splash_video.mov &`

For VLC: `cvlc /home/pi/video/splash_video.mov &`

<kbd>STRG</kbd>+<kbd>X</kbd> to save the file and confirm overwriting the file with <kbd>Y</kbd>.

&nbsp;

That should be all ... Reboot your Pi and your video / image should appear while booting.

`sudo reboot`
