# Arch

## AUR package manager

Currently using `yay`.

``` {.bash}
git clone https://aur.archlinux.org/yay.git
```

## MacOS
-----

*sb2nov MacOS Setup Guide*

### Clean Install

[Guide on how to clean
install](http://osxdaily.com/2017/09/27/download-complete-macos-high-sierra-installer/)

## Bluetooth

How to check for bluetooth using `dmesg` and `rfkill`:

``` {.bash org-language="sh"}
dmesg | grep -i Bluetooth
sudo rfkill list
```

If `rfkill` returns block on the devices, run:

``` {.bash org-language="sh"}
sudo rfkill unblock bluetooth
```

Load the `btusb` kernel module:

``` {.bash org-language="sh"}
modprobe -v btusb
```

If it returns something like the following:

> modprobe: FATAL: Module btusb not found in directory
> /lib/modules/4.19.38-1-lts

It means that the kernel has been updated and it is not finding the
module. Should reboot to load the module.

Install `bluez` and (AUR) `bluez-utils` packages:

``` {.bash org-language="sh"}
sudo pacman -S bluez bluez-utils
```

Check if `systemctl` has a bluetooth service running:

``` {.bash org-language="sh"}
sudo systemctl status bluetooth # or
sudo systemctl status bluetooth.target # this was the service running on the archlabs macbook
# if the service is not started:
sudo systemctl start bluetooth
```

[ArchWiki: Bluetooth](https://wiki.archlinux.org/index.php/Bluetooth)
[Linux Hint: Bluetooth](https://linuxhint.com/bluetooth_arch_linux/)

### Using `bluetoothctl`

Running:

``` {.bash org-language="sh"}
bluetoothctl
```

Inside the bluetoothctl interface turn the agent on with `agent on`
command. Set the default agent with `default-agent`.

Example of pairing:

``` {.bluetoothctl}
[NEW] Controller 00:10:20:30:40:50 pi [default]
[bluetooth]# agent KeyboardOnly
Agent registered
[bluetooth]# default-agent
Default agent request successful
[bluetooth]# power on
Changing power on succeeded
[CHG] Controller 00:10:20:30:40:50 Powered: yes
[bluetooth]# scan on
Discovery started
[CHG] Controller 00:10:20:30:40:50 Discovering: yes
[NEW] Device 00:12:34:56:78:90 myLino
[CHG] Device 00:12:34:56:78:90 LegacyPairing: yes
[bluetooth]# pair 00:12:34:56:78:90
Attempting to pair with 00:12:34:56:78:90
[CHG] Device 00:12:34:56:78:90 Connected: yes
[CHG] Device 00:12:34:56:78:90 Connected: no
[CHG] Device 00:12:34:56:78:90 Connected: yes
Request PIN code
[agent] Enter PIN code: 1234
[CHG] Device 00:12:34:56:78:90 Paired: yes
Pairing successful
[CHG] Device 00:12:34:56:78:90 Connected: no
[bluetooth]# connect 00:12:34:56:78:90
Attempting to connect to 00:12:34:56:78:90
[CHG] Device 00:12:34:56:78:90 Connected: yes
Connection successful
```

### Bluetooth-to-serial option

This is a simplified version of the [How to
pair](id:679a3729-807f-405c-9f13-33718d632e3d) section.

Install the utilities the don\'t come with `bluez-utils`:

``` {.bash org-language="sh"}
yay -S bluez-rfcomm bluez-hcitool
```

Discover the MAC address:

``` {.bash org-language="sh"}
hcitool dev
```

Use the MAC address to connect:

``` {.bash org-language="sh"}
rfcomm bind rfcomm0 <MAC address of bluetooth device>
```

### How to pair {#how-to-pair id="679a3729-807f-405c-9f13-33718d632e3d"}

The `hcitool` doesn\'t come with the `bluez-utils` package anymore, but
it can be installed from AUR using `bluez-hcitool`.

Discover the MAC address:

``` {.bash org-language="sh"}
hcitool dev
```

Using the pairing code (0000):

``` {.bash org-language="sh"}
bluetooth-agent 0000 &
```

Set an `rfcomm` connection to bind the device at startup (also needs to
be installed from AUR). Need to edit `/etc/bluetooth/rfcomm.conf`:

    rfcomm0 {
      # Automatically bind the device at startup
      bind no;
      # Bluetooth address of the device
      device 11:22:33:44:55:66;
      # RFCOMM channel for the connection
      channel 3;
      # Description of the connection
      comment "This is Device 1's serial port.";
    }

If `bind no` is used, then it will be needed to manually run the
following command everytime to connect:

``` {.bash org-language="sh"}
sudo rfcomm connect rfcomm0
```

[Heatxsink: How to
pair](http://www.heatxsink.com/entry/how-to-pair-a-bluetooth-device-from-command-line-on-linux)

### Problems connecting to headphone

<https://www.reddit.com/r/linuxmint/comments/5vdly8/bluetooth_headphones_and_linux_mint/>

## Wireless

To enable the module:

``` {.bash}
sudo modprobe -v b43
```

Senha Intelbras: S1EB638354

## Sound

If sound doesn\'t work try:

``` {.bash}
pulseaudio --start
```

If the headphone jack doesn\'t work try:

``` {.bash}
alsamixer
```

Then unmute with `M`.

## Battery life

The battery has improved hugely over the week and after the
modifications listed by Michael Chladek. Namely, installing `powertop`,
`thermald` and `cpupower` just like he described.

When running powertop for the first time, the screen will go black for a
few minutes for a couple of times - don\'t freak out.

``` {.bash}
powertop --calibrate
```

After installing everything and enabling the .service\'s, reboot. I also
installed cpupower-gui so I could easily set the max clock for the CPU
at 2.9 GHz, instead of 3.1. As far as I researched, thermald doesn\'t
need further configurations, you just need to enable it.

## Keyboard light

This fix is really easy to implement and will also get the keyboard
shortcuts automatically if you use the setting my i3 config file - or
just search for the keyword and see how it was implemented. Open the
terminal and type yay -s kbdlight and install it. The commands are
really simple to understand, just read the [git
page](https://github.com/WhyNotHugo/kbdlight).

``` {.bash}
yay -s kbdlight
```

The i3 config file already has the configurations built-in.

## Reinstall and configuration
---------------------------

What is not incorporated in this file can be found in the archlabs
repository.

### yay

### vifm

### Battery life

### mbpfan service

### keyboard light

### i3

### latex

### R

### ledger

### newsboat

### plugins neovim

### nvim-r

### rstudio

### inkscape

### libreoffice

### sync all git repositories

### redo urls file for newsboat

### flameshot

### mailspring

# Parabola

[Installation
guide](https://wiki.parabola.nu/Beginners%27_Guide#Establish_an_internet_connection)

Crucial steps: [parted](https://wiki.parabola.nu/GNU_Parted)
[fstab](https://wiki.parabola.nu/Fstab#Identifying_filesystems) [chroot
- change root](https://wiki.parabola.nu/Change_Root)

# Debian/Mint

## dpkg


[dpkg
cheatsheet](https://www.cyberciti.biz/howto/question/linux/dpkg-cheat-sheet.php)
Syntax Description Example 
- `dpkg -i {.deb package}` Install the package
`dpkg -i zip_2.31-3_i386.deb` 
- `dpkg -i {.deb package}` Upgrade package
if it is installed else install a fresh copy of package
`dpkg -i zip_2.31-3_i386.deb` 
- `dpkg -R {Directory-name}` Install all
packages recursively from directory `dpkg -R /tmp/downloads`
- `dpkg -r {package}` Remove/Delete an installed package except
configuration files `dpkg -r zip` 
- `dpkg -P {package}` Remove/Delete
everything including configuration files `dpkg -P apache-perl` 
- `dpkg -l`
List all installed packages, along with package version and short
description `dpkg -l` `dpkg -l | less` `dpkg -l '*apache*'`
`dpkg -l | grep -i 'sudo'` 
- `dpkg -l {package}` List individual installed
packages, along with package version and short description
`dpkg -l apache-perl` `dpkg -L {package}` Find out files are provided by
the installed package i.e. list where files were installed
`dpkg -L apache-perl` `dpkg -L perl` `dpkg -c {.Deb package}` List files
provided (or owned) by the package i.e. List all files inside debian
.deb package file, very useful to find where files would be installed
`dpkg -c dc_1.06-19_i386.deb`
- `dpkg -S {/path/to/file}` Find what package owns the file i.e. find out
what package does file belong `dpkg -S /bin/netstat`
`dpkg -S /sbin/ippool` 
- `dpkg -p {package}` Display details about package
package group, version, maintainer, Architecture, display depends
packages, description etc `dpkg -p lsof`
- `dpkg -s {package} | grep Status` Find out if Debian package is
installed or not (status) `dpkg -s lsof | grep Status`

## `sudo`

<https://unix.stackexchange.com/questions/354928/bash-sudo-command-not-found>

How to install `sudo`:

``` {.bash}
su - 
apt-get install sudo -y
```

And give sudo right to the user:

``` {.bash}
usermod -aG sudo username
```

Check with `visudo` the lines:

> \%sudo ALL=(ALL:ALL) ALL

## apt-get (just `apt`)

[apt-get
cheatsheet](https://www.cyberciti.biz/howto/question/linux/apt-get-cheat-sheet.php)

## flatpak

<https://wiki.debian.org/FlatpakHowto>

## emacs installation

<https://www.emacswiki.org/emacs/EmacsSnapshotAndDebian>

How to install:

``` {.bash}
# install dependencies
sudo apt-get install autoconf automake libtool texinfo build-essential xorg-dev libgtk2.0-dev libjpeg-dev libncurses5-dev libdbus-1-dev libgif-dev libtiff-dev libm17n-dev libpng-dev librsvg2-dev libotf-dev libgnutls28-dev libxml2-dev

git clone --depth 1 git://git.sv.gnu.org/emacs.git

cd emacs
./autogen.sh
./configure
make bootstrap
sudo make install
```

How to build depencies for emacs on
[ergoemacs](http://ergoemacs.org/emacs/building_emacs_on_linux.html). To
keep the repo up to date:

``` {.bash}
git checkout -t tag-name

git clean -dxf ## cleans up old files
./autogen.sh
./configure
make bootstrap
sudo make install
```

## sources.list

<https://linuxhint.com/how-to-add-a-package-repository-to-debian/>

## vifm

`sudo apt-get install vifm`

## xrandr

Change resolution of dell inspiron 15:

``` {.bash}
xrandr -s 1360x768

```

## cmake

The cmake version on Debian Stable is really old. To download and
install the latest version go to [CMake
page](http://www.cmake.org/download).

``` {.bash}
mkdir temp
cd temp/
wget https://github.com/Kitware/CMake/releases/download/v3.14.4/cmake-3.14.4-Linux-x86_64.sh
sudo mkdir /opt/cmake
sudo sh cmake-$version.$build-Linux-x86_64.sh --prefix=/opt/cmake
sudo ln -s /opt/cmake/bin/cmake /usr/local/bin/cmake
cmake
```

Other options can be found on
[stackoverflow](https://askubuntu.com/questions/355565/how-do-i-install-the-latest-version-of-cmake-from-the-command-line).

## Brightness

In the case the brightness controls are not working, it is possible to
install `brightness-controller` by adding a repository.

``` {.bash}
sudo add-apt-repository ppa:apandada1/brightness-controller
sudo apt update
sudo apt install brightness-controller # multi monitor support

```

## Horizontal touchpad scrolling

Run on terminal:

    synclient HorizTwoFingerScroll=1

<https://askubuntu.com/questions/264091/enable-horizontal-scrolling-in-ubuntu>

## Date and time

<https://www.adminschoice.com/unix-date-format-examples>

Look for timedatectl

# Fedora

There is an option to check the drive of the installation before start
Fedora live.

Teclado para o macintosh: Inglês (EUA, intern. alt.)

Installation time: \>24 min

DE is gnome-shell

While on update:

-   CPU usage is from 0 to 100%.
-   Memory use is 1.7 GB

The installation of the updates needs the system to be rebooted.
Technically, it should be fast since I downloaded the image less than a
week ago. But it is taking a lot of time to install those updates.

After installation of updates:

-   5 to 10 % CPU
-   1,2 GB memory
-   Installation uses 6.2 GB of space

Most resource hungry programs:

-   gnome-shell uses 168 MB of RAM
