---
layout: post
title: Homelab Part 2 - Wireguard VPN on OpenWRT Router
---

This is the second post in a series documenting my first serious look into home-labbing. My first post was about using Pihole and Unbound in Docker on a Raspberry Pi. If you are interested please see it [here](https://jsparkes.com/Homelab-Part-1-PiHole/).

I'm very excited to write this second post as it is something I have been trying, in one way or another to achieve for months. I first heard about Wireguard on one of the many Linux podcasts I consume (Shout out [Linux Unplugged](https://linuxunplugged.com/), [Linux Action News](https://linuxactionnews.com/) and [Late Night Linux](https://latenightlinux.com/) to name a few). As a PiVPN dabbler it seemed like a huge improvement over the OpenVPN software. Almost instant connectivity, a simple code base and a way to filter SSID's to make it automatically switch off on certain networks.

Despite this excitement I never managed to get it working. I had a lot to learn. As I wrote in my first post my network is a strange one. Running off a 4g unlimited phone contract in a Huawei dongle plugged into the back of an Archer C7 OpenWRT router. However I will be doing another post in the future about the wonders of [double NAT](https://kb.netgear.com/30186/What-is-Double-NAT) and how I managed to get through it. For now I am going to focus on getting Wireguard set up on an OpenWRT router and some devices. I am going to try and walkthrough as simple as possible so even the newest user can follow along, however I will be providing many links for further reading throughout the post so you can get as deep as you want into everything.

Warning: As this will be opening your home network to the internet, I strongly suggest reading all extra information, please also read outside of what I provide as I am in no way an expert and may have security holes in what I write below. If you do not feel comfortable doing this please consider creating a Wireguard VPN on a server such as [Digital Ocean](https://www.digitalocean.com/community/tutorials/how-to-create-a-point-to-point-vpn-with-wireguard-on-ubuntu-16-04). Please be smart and understand how much you do/don't stand to lose and the risks you take.

With that, on with the guide!

# [SHH](https://en.wikipedia.org/wiki/Secure_Shell) into your [OpenWRT](https://en.wikipedia.org/wiki/OpenWrt) Router(This is done different depending on your operating system, please use Google to find out how to do it on your particular system)

# Update your packages using the following command
```
opkg update
```

#  
