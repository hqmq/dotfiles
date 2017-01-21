# What I learned Setting Up Antergos

## Map Caps-Lock => Esc or Ctrl

* Install `xcape` package.
* Edited `/etc/X11/xinit/xinitrc.d/50-systemd-user.sh`

```
# disable CapsLock, make CapsLock behave like Ctrl + esc
python -c 'from ctypes import *; X11 = cdll.LoadLibrary("libX11.so.6"); display = X11.XOpenDisplay(None); X11.XkbLockModifiers(display, c_uint(0x0100), c_uint(2), c_uint(0)); X11.XCloseDisplay(display)'
setxkbmap -option ctrl:nocaps
xcape -e 'Control_L=Escape'
```

## Apple Touchpad Tweak

The apple touchpad felt very twitchy and overly sensitive.
I followed the directions [from arch wiki](https://wiki.archlinux.org/index.php/MacBookPro10,x#Touchpad).

* Installed `xf86-input-mtrack-git` from AUR
* Edited `/etc/X11/xorg.conf/50-synaptics.conf`

```
Section "InputClass"
	MatchIsTouchpad "on"
	Identifier      "Touchpads"
	Driver          "mtrack"
	Option          "Sensitivity" "0.65"
	Option          "IgnoreThumb" "true"
	Option          "IgnorePalm" "true"
	Option          "TapButton1" "1"  
	Option          "TapButton2" "3"
	Option          "TapButton3" "2"
	Option          "ClickFinger1" "1"
	Option          "ClickFinger2" "2"
	Option          "ClickFinger3" "3"
	Option          "BottomEdge" "25"
	Option          "ScrollDownButton"  "4"
	Option          "ScrollUpButton"    "5"
	Option          "ScrollLeftButton"  "7"
	Option          "ScrollRightButton" "6"
EndSection
```
