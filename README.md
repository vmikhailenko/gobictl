Simple script to manage Qualcomm Gobi 2000 GPS device in Linux

# How to set up Gobi 2000 GPS in Linux

+ `sudo apt-get install gobi_loader`

+ Copy firmware to `/lib/firmware/gobi`

+ Modify /lib/udev/rules.d/60-gobi_loader.rules

	# ACTION=="add", SUBSYSTEM=="tty" KERNEL=="ttyUSB*" GOTO="gobi_rules" GROUP="gpsd" MODE="0664"
	ACTION=="add", SUBSYSTEM=="tty" KERNEL=="ttyUSB*" GOTO="gobi_rules" GROUP="gpsd" MODE="0664" SYMLINK+="gobi%n"

This will create symlinks gobi1, gobi2 and gobi3 for each of the Gobi 2000 devices and make GPS device writable by members of group *gpsd*.

+ Disable _gpsd_ and _gpsd.socket_ in systemd. 

+ Use script `gobictl start [device]` to start GPS tracking and start gpsd for device. `gobictl stop` will stop GPS tracking and kill gpsd.

+ Check status via `gpsmon` or `xgps`. 