# SVUP

> Upgrade the operating system from a disk image file

Svup is a bash script that performs full root filesystem upgrades by utilizing
btrfs subvolumes.
The name is short for **S**ub**v**olume **Up**grade.
The upgrade is provided in the form of a raw disk image file
whose contents are then transferred onto a snapshot
of the current root filesystem.

Then the boot loader is configured to boot into the filesystem
containing the new upgrades.
Currently only the Raspberry Pi bootloader is supported.

This script was made to facilitate safe and full system upgrades within the
[klippo](https://github.com/D4SK/klippo)
3D-printing software.

## Installing

The script `svup` can be run just by itself,
but some actions require the correct configuration structure
which is best installed through a debian package.

Building the package requires `debhelper` to be installed:

```bash
sudo apt-get install debhelper
```

From inside this repository,
execute the following command to build the package:

```bash
dpkg-buildpackage -us -uc -b
```

Install the package:

```bash
sudo dpkg -i ../svup*.deb
```

In case any dependencies are missing, install them using

```bash
sudo apt-get install -f
```

## Documentation

See `man svup` for details on usage and how _svup_ works.
`svup -h` gives a shorter summary of all available options.
