---
layout: post
title:  "Linux usage"
date:   2020-09-27 15:20:02 +0700
categories: jekyll update
---

- ### Fix different time when dual boot windows & ubuntu:
{% highlight shell %}
~$ timedatectl set-local-rtc 1 --adjust-system-clock
#=> To check your current settings, run:
~$ timedatectl
#=> If you ever want to undo this change, run the following command:
~$ timedatectl set-local-rtc 0 --adjust-system-clock
{% endhighlight %}
- ### Thunar file manager Sftp client:
{% highlight shell %}
gvfs-backends
{% endhighlight %}
- ### Format a disk partition:
{% highlight shell %}
~$ fdisk -l
#=> This will give you a list of available drives that are mounted. The flash drive is almost always at the bottom saying something like /dev/sdb1 (with or without a number). That’s your drive.
{% endhighlight %}
# Unmount disk drive:
{% highlight shell %}
~$ umount /dev/sdb1
{% endhighlight %}
# Now let’s format that sucker! The use of “DEVICENAME” is your name of the drive. Replace it with whatever you want.
# For a DOS/Windows FAT format, type:
{% highlight shell %}
~$ mkdosfs -n "DEVICENAME" -I /dev/sdb1
{% endhighlight %}
# For a Windows FAT32 format, type:
{% highlight shell %}
~$ mkfs.vfat -n "DEVICENAME" -I /dev/sdb1
{% endhighlight %}
# For a GNU/Linux Ext3 format, type:
{% highlight shell %}
~$ mkfs.ext3 -L "DEVICENAME" /dev/sdb1
{% endhighlight %}
This may take a while. After formatting you will be returned to the prompt. Remove and insert the drive to have it mounted again.
- ### Kill a Linux process:
{% highlight shell %}
kill -9 `pgrep -f bitbake`
ps aux | grep -i firefox | awk {'print $2'} | xargs kill -9
ps aux | grep -i firefox
strace -p PID
kill $(ps aux | grep '[p]ython csp_build.py' | awk '{print $2}')
{% endhighlight %}
- ### Git submodule:
Add:
{% highlight shell %}
~$ git submodule add <repository> [<path>]
{% endhighlight%}
{% highlight shell %}
~$ git clone <repository> --recurse-submodules
~$ git submodule update --init --recursive
~$ git submodule update --remote --merge
{% endhighlight%}
Remove:
{% highlight shell %}
1. ~$ git submodule deinit -f -- a/submodule    
2. ~$ rm -rf .git/modules/a/submodule
3. ~$ git rm -f a/submodule
# Note: a/submodule (no trailing slash)
# or, if you want to leave it in your working tree and have done step 0
3. ~$ git rm --cached a/submodule
{% endhighlight %}
{% highlight shell %}
# If you want to see which files will be deleted you can use the -n option before you run the actual command:
~$ git clean -nd
# To remove directories
~$ git clean -df
# To remove ignored files
~$ git clean -Xf
# To remove ignored and non-ignored files
~$ git clean -xf
{% endhighlight%}
