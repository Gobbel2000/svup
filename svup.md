# SVUP (Subvolume Upgrade)

## Download

done externally, in another tool (maybe just as part of kgui)

* List potential images/releases
* Download image, reporting progress
* Validate signature and checksum (maybe in svup tool instead?)


## Install image

* Validate signature and checksum (maybe only in download tool)
* Mount image (using loop device)
* Mount btrfs top level volume
* Snapshot current root subvolume
* rsync root subvolume from image to snapshot
* Copy contents of /boot in image to /boot-save in new snapshot


## List versions

Show a list of all installed alternate versions (essentially, snapshots) that
could be staged, along with some metadata information like:

* Build date
* Install date
* Klippo version
* Disk usage (in terms of COW)


## Stage version

* Copy contents of /boot into /boot-save of current root
* Copy /boot-save of snapshot int /boot/tryboot/
* Copy /boot/config.txt to /boot/tryboot.txt and add `os_prefix=tryboot/`
* Change subvolume in:
  * /boot/tryboot/cmdline.txt
  * SNAPSHOT/etc/fstab


## Boot new version

* Test, if something is staged
* reboot '0 tryboot'


## Verify after boot

If booted successfully:

* Make permanent:
  * Move contents of /boot/tryboot into /boot
  * Unstage version

If didn't boot successfully:

* Notify user
* reboot normally, into previous installation
* Maybe Unstage version


## Unstage version

* Delete /boot/tryboot and /boot/tryboot.txt
