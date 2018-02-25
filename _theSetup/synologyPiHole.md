---
layout: default
title: Running a Pi-Hole Docker Image on my Synology Nas
hook: Network wide Ad-Blocking
published: true
---
# The Idea

I have a nice two bay Synology NAS and it can run Docker.  Why not run pi-hole as a docker image from my NAS and get network wide Ad Blocking?

[Pi-hole](https://pi-hole.net/) is software originally designed to run on a Rasberry Pi that acts as a DNS server that magically disappers Ads and "web tracking" by failing to resolve the domains of known Ad service / tracking domains.

# Verdict

This is possible, I had it working Just-Fine™, but ultimately decided not to keep it running.

Not to knock that work that [the people that put the pi-hole docker image together](https://hub.docker.com/r/diginc/pi-hole/) are doing, but (for me) the better approach is to just actually get a Raspberry Pi / some compute stick and just run pi-hole on that.

## Issues

### 1) The pi-hole doesn't "containerize" well

The real [pi-hole](https://pi-hole.net/)
* has a nice in-place upgrade path
* has easy/web-based mechanisms to download your config (whitelist/blacklist) and the upload/restore if/when you get a new pi/reinstall the os
* will show you a nice "blocked by pi-hole" message/image/svg when it blocks something
   * so that you/your significant other will know that things are "broken on purpose", instead of just "broken in general"

The most "authentic" way to run pi-hole on a Synology NAS would be to let the docker image use host level neworking.  This means the pi-hole needs port 53 (to actually respond to DNS requests) and port 80 (to host the Admin UI and to show the nice "blocked by pi-hole" images).  

If you let it have port 80, then that means lots of other Synology apps won't work.

If you run it with "bridged" networking (basically the docker image is NATed) then, you don't get
* nice "blocked by pi-hole" message
* to see which deviceds on your network are making DNS calls
   * lookin at you SamsungTV/Ring/Windows boxes, etc

### 2) Docker on Synology is "fiddly"

You find the image you want and "download" it, and get it running.   Now then, how do you upgrade / pull a fresh image?  I couldn't get to a good answer on that.

Here is what I ended up doing
1. Select the Container, and then do Setting -> Export
    * this will make a Json file on your NAS that has all the stuff you typed in to configure the container
2. Delete the container.
    * Wait, why would I delete a known working container, instead of just making a "new" one from the Setting -> Export config file?
    * Because, Synology / Docker won't let you as you would have two containers each trying to bind port 53.
3. Delete the image.
    * Wait, why wouldn't I just "refresh" the image, and then create a new container from the Settings -> Export config file?
    * Well, I couldn't find / figure out how to update / pull the latest image / verify which image I have.   I.e. there is no "refresh button".
    * Also, the Setting -> Export JSON config file has a bunch of GUIDy looking references.   I might be the case that your exported settings actually reference a "particular version" of the image.   
4. Redownload the image.
    * Wait, it won't download now.   Actually, no docker images will download now.  WTF?
    * Yeah so turns out I had a circular dependency of DNS lookup between my wifi-router and the NAS, that only showed up when the NAS stopped being a DNS server / when the docker image was stopped.

## 3) Docker keeps the NAS awake

This was the "straw that broke the camel's back".  Previously, the NAS would spend most of it's life with the hard drives in hibernation, A) being quiet, and B) prolonging life.

I had the bright idea that I could "permanently" plug in a USB stick, and then "run the docker image" off the USB drive, thus allowing the main drives to spin down.

Unfortunatly, that isn't possible as the Synology Docker "package" will only install on a "real" volume, and USB drives do not qualify.

I then configured the Docker image to write it's config and log files to the USB drive, and while that did reduce the number of times the disks were written to, it did not stop it.  There was still something that was forcing writes to the disks every few seconds.

# The Setup

* Make sure your Synolgoy has a static ipaddress OR a static DHCP address from your router.
* Install the Docker Package
* Grab the diginc/pi-hole image
* Create a new container using "bridged" networking

Use these settings when creating the container as "environment variables"    
```
DNS1=9.9.9.9     // the https://quad9.net/ DNS
DNS2=8.8.8.8     // Google's DNS
ServerIP=ip of the Nas
WEBPASSWORD=changeme

Not using host networking
Local -> Container
53       53
8053     80      // access the pi-hole admin by http://ipOfNas:8053/admin
```

And lastly, configure your router to use the NAS as a DNS server.

## References

- [http://tonylawrence.com/post/unix/synology/running-pihole-inside-docker/](http://tonylawrence.com/post/unix/synology/running-pihole-inside-docker/)
    - this guy is running in host networking mode
- [https://discourse.pi-hole.net/t/alternative-synology-installation-method/5454](https://discourse.pi-hole.net/t/alternative-synology-installation-method/5454)
	- overly fancy setup, aka I don't need the lan ips that look stuff up

