---
layout: single
title:  "Linux usage"
date:   2020-09-27 15:20:02 +0700
categories: linux commandline
---

- ### Fix different time when dual boot windows & ubuntu:
{% capture code %}{% raw %}
timedatectl set-local-rtc 1 --adjust-system-clock
#=> To check your current settings, run:
timedatectl
#=> If you ever want to undo this change, run the following command:
timedatectl set-local-rtc 0 --adjust-system-clock
{% endraw %}{% endcapture %}
{% include code.html lang="shell_session" code=code %}
- ### Thunar file manager Sftp client:
{% capture code %}{% raw %}
apt install gvfs-backends
{% endraw %}{% endcapture %}
{% include code.html lang="shell_session" code=code %}
- ### Format a disk partition:
{% capture code %}{% raw %}
fdisk -l
#=> This will give you a list of available drives that are mounted. The flash drive is almost always at the bottom saying something like /dev/sdb1 (with or without a number). That’s your drive.
{% endraw %}{% endcapture %}
{% include code.html lang="shell_session" code=code %}
{% capture code %}{% raw %}
# Unmount disk drive:
umount /dev/sdb1
{% endraw %}{% endcapture %}
{% include code.html lang="shell_session" code=code %}
{% capture code %}{% raw %}
# Now let’s format that sucker! The use of “DEVICENAME” is your name of the drive. Replace it with whatever you want.
# For a DOS/Windows FAT format, type:
mkdosfs -n "DEVICENAME" -I /dev/sdb1
{% endraw %}{% endcapture %}
{% include code.html lang="shell_session" code=code %}
{% capture code %}{% raw %}
# For a Windows FAT32 format, type:
mkfs.vfat -n "DEVICENAME" -I /dev/sdb1
{% endraw %}{% endcapture %}
{% include code.html lang="shell_session" code=code %}
{% capture code %}{% raw %}
# For a GNU/Linux Ext3 format, type:
mkfs.ext3 -L "DEVICENAME" /dev/sdb1
{% endraw %}{% endcapture %}
{% include code.html lang="shell_session" code=code %}
This may take a while. After formatting you will be returned to the prompt. Remove and insert the drive to have it mounted again.
- ### Kill a Linux process:
{% capture code %}{% raw %}
kill -9 `pgrep -f bitbake`
{% endraw %}{% endcapture %}
{% include code.html lang="shell_session" code=code %}
{% capture code %}{% raw %}
ps aux | grep -i firefox | awk {'print $2'} | xargs kill -9
{% endraw %}{% endcapture %}
{% include code.html lang="shell_session" code=code %}
{% capture code %}{% raw %}
kill $(ps aux | grep '[p]ython csp_build.py' | awk '{print $2}')
{% endraw %}{% endcapture %}
{% include code.html lang="shell_session" code=code %}
{% capture code %}{% raw %}
ps aux | grep -i firefox
strace -p PID
{% endraw %}{% endcapture %}
{% include code.html lang="shell_session" code=code %}
- ### Git submodule:

Add:
{% capture code %}{% raw %}
git submodule add <repository> [<path>]
{% endraw %}{% endcapture %}
{% include code.html lang="shell_session" code=code %}
{% capture code %}{% raw %}
git clone <repository> --recurse-submodules
{% endraw %}{% endcapture %}
{% include code.html lang="shell_session" code=code %}
{% capture code %}{% raw %}
git submodule update --init --recursive
{% endraw %}{% endcapture %}
{% include code.html lang="shell_session" code=code %}
{% capture code %}{% raw %}
git submodule update --remote --merge
{% endraw %}{% endcapture %}
{% include code.html lang="shell_session" code=code %}

Remove:
{% capture code %}{% raw %}
git submodule deinit -f -- a/submodule
rm -rf .git/modules/a/submodule
{% endraw %}{% endcapture %}
{% include code.html lang="shell_session" code=code %}
{% capture code %}{% raw %}
git rm -f a/submodule
{% endraw %}{% endcapture %}
{% include code.html lang="shell_session" code=code %}
{% capture code %}{% raw %}
# Note: a/submodule (no trailing slash)
# or, if you want to leave it in your working tree and have done step 0
git rm --cached a/submodule
{% endraw %}{% endcapture %}
{% include code.html lang="shell_session" code=code %}

{% capture code %}{% raw %}
# If you want to see which files will be deleted you can use the -n option before you run the actual command:
git clean -nd
{% endraw %}{% endcapture %}
{% include code.html lang="shell_session" code=code %}
{% capture code %}{% raw %}
# To remove directories
git clean -df
{% endraw %}{% endcapture %}
{% include code.html lang="shell_session" code=code %}
{% capture code %}{% raw %}
# To remove ignored files
git clean -Xf
{% endraw %}{% endcapture %}
{% include code.html lang="shell_session" code=code %}
{% capture code %}{% raw %}
# To remove ignored and non-ignored files
git clean -xf
{% endraw %}{% endcapture %}
{% include code.html lang="shell_session" code=code %}