---
title: Uptime-Kuma
date: 2023-01-27 00:00:00 +0100
categories: [Homelab, Software]
tag: [docker, synology]        #TAG names should always be lowercase
---

# Setup Uptime-Kuma on Synology Docker

Based on: https://mariushosting.com/how-to-install-uptime-kuma-on-your-synology-nas/

Docker Hosts configuration failed. 

Remove:
-e PUID=1026 \
-e PGID=100 \

Also added DNS because with Pi-Hole running as DNS the monitoring failed.

docker run -d --name=uptime_kuma \
-p 3444:3001 \
-e TZ=Europe/Amsterdam \
-v /volume1/docker/uptimekuma:/app/data \
-v /var/run/docker.sock:/var/run/docker.sock \
--restart always \
--dns 1.1.1.1 \
--dns 1.0.0.1 \
louislam/uptime-kuma
