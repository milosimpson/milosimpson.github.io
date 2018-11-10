---
layout: default
published: true
hook: Java Development Environment on Windows 10 cira 2018
---
# Java Development Environment on Windows 10 in 2018

## Context

Recently, Macs have become thier own special kind of ["bag of hurt"](https://www.youtube.com/watch?v=-XSC_UG5_kU).  So, for the first time in 15 years, I purchased a Dell laptop in instead of a MacBook Pro: Dell XPS 9560 (1TB SSD 32gigs ram, Costco special).

My professional history of developing Java has been :
1. Windows - on the MicroSoft JVM with Visual Studio
2. Linux - on Redhat with Netbeans / Intellij
3. Windows - on Cygwin with Intellij
4. Mac - on Brew with Intellij

So I know I can develop on windows, I would just prefer it to on be on cygwin again.   I also plan to dual boot into Ubuntu and setup an environment there, but that is a different doc.

## Goals 

- Use the Windows version of Intellij, so that it will work well with HiDpi monitors and be fast.
- Use the Windows Subsystem for Linux (WSL) to do everything else.
- Have a resonable terminal experience with proper copy and paste support.

Things I know I am going to miss

- brew
- pbcopy and pbpaste

## The High Level Plan

After a bunch of trial and error there is where I landed.

 - Install and setup WSL
     - change my WSL user's home directory to be a symlink to a windows side directory
     - then install apt versions of jdk, maven, git, etc
     - setup ssh keys
 - On the windows side install
     - Java
     - Intellij (note don't need Windows Side maven)
     - Cygwin ... specifically to get "git.exe" for Intellij
     - [cmder](http://cmder.net/) as the tty front end to WSL Bash
 
Admittedly this is a bit janky.   There will be two different JVMs and two different verions of Git touching the same files, but it works, at least for the simple things I am doing.

### WSL and home directory setup

Linux can read and write "windows" files, but not the other way around.   Because maven and git write to the "home" directory by default, and Intellij wants to be able to read and write to those files, they need to "live" in Windows.

Reference
 - [https://askubuntu.com/questions/772050/reset-the-password-in-linux-bash-in-windows](https://askubuntu.com/questions/772050/reset-the-password-in-linux-bash-in-windows)
 - [https://superuser.com/questions/1132626/changing-home-directory-of-user-on-windows-subsystem-for-linux](https://superuser.com/questions/1132626/changing-home-directory-of-user-on-windows-subsystem-for-linux)

The idea is to use the same mechanism as resetting the linux user's password by logging in as "root", but then editing the /etc/passwd file to change the home directory.

**Gotcha 1** :  Linux needs to have created the directory on windows.   Aka I want to use "c:\winux\msimpson" as my home dir.   So in only create "C:\winux" in windows, and create the "msimpson" sub dir from linux.

```
# In PowerShell run as Administrator
ubuntu config --default-user root

# In new WSL now logged in as root
mkdir -p /mnt/c/winux/msimpson
vi /etc/passwd   # change to /mnt/c/winux/msimpson"

# Quit WSL and back in Admin PowerShell
ubuntu config --default-user msimpson

# Move existing dot files
# In new WSL session now logged in as msimpson
pwd  # should say /mnt/c/winux/msimpson

cp -r /home/msimpson/.* .
```

**Gotcha 2** :  Ssh will be grumpy with the new "windows" compatible "home" dir in that the new dir  has super open permissions.   Thus the trick is to leave the .ssh dir in the linux FS but make it available as a sym or hardlink from the windows dir.

```
ln -s /home/msimpson/.ssh /mnt/c/winux/msimpson/.ssh
```

### Windows Setup

I preffer to make a c:\java directory and then have the jdks and Intellij be installed there.

I install cmder and cywin under c:\winux.

This is how to get cmder to boot WSL by default.   
- [https://gist.github.com/nickautomatic/02ccb76292f7f8d9767e](https://gist.github.com/nickautomatic/02ccb76292f7f8d9767e)
