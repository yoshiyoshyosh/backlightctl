# backlightctl
A simple script to change the backlight brightness value on laptops. Mostly made as a workaround for [this bug](https://bugzilla.kernel.org/show_bug.cgi?id=203905).

## Configuration
The only configurable variable is the backlight path. It defaults to `/sys/class/backlight/amdgpu_bl0/brightness`. You can change `BACKLIGHT_PATH` to point to the file path.

## Usage
```
Usage: backlightctl [-h] [-s VALUE] [-c VALUE]
No arguments: Print current brightness and exit
If -s and -c are specified, -c takes priority

 -h         show this help
 -q         print current brightness to stdout and exit
 -s <VALUE> set brightness to VALUE
 -c <VALUE> change brightness by VALUE
```

## Recommendations
- Move this script to `/usr/local/bin`
- If your backlight isn't saved on reboot, add the following to `/etc/rc.local`:
```
/usr/local/bin/backlightctl -s <your_preferred_brightness>
```
- (doas) add the following to `/etc/doas.conf`:
```
permit nopass :wheel as root cmd backlightctl
```
- (sudo) add the following to `/etc/sudoers` (using `visudo`):
```
%wheel ALL=(ALL:ALL) NOPASSWD: /usr/local/bin/backlightctl
```
