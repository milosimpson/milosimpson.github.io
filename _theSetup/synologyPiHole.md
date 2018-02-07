---
layout: default
title: Pi Hole Docker Image on the Nas
hook: Network wide Ad-Blocking
published: true
---

* Docker
* Synology Gotchas
* USB parition so that the hard drives can sleep


Grab the diginc/pi-hole image.   Currently uses debian as the x86 compatible image.


References
- [http://tonylawrence.com/post/unix/synology/running-pihole-inside-docker/](http://tonylawrence.com/post/unix/synology/running-pihole-inside-docker/)
    - docs no making the "landing page" better
- [https://discourse.pi-hole.net/t/alternative-synology-installation-method/5454](https://discourse.pi-hole.net/t/alternative-synology-installation-method/5454)
	- overly fancy setup, aka I don't need the lan ips that look stuff up
    
    
```
DNS1=9.9.9.9
DNS2=8.8.8.8
ServerIP=ip of the Nas
WEBPASSWORD=changeme

Not using host networking
Local -> Container
53       53
8053     80      // access the pi-hole admin by http://ipOfNas:8053/admin
```