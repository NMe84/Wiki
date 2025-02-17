---
title: Lidarr Appdata Directory
description: 
published: true
date: 2021-08-15T12:50:21.318Z
tags: lidarr, appdata
editor: markdown
dateCreated: 2021-06-09T15:53:13.142Z
---

## Windows

`C:\ProgramData\Lidarr`

## Linux

Unless otherwise specified Lidarr will store it's application data in the home folder of the user Lidarr is running under `/home/$USER/.config/Lidarr` (`~/.config/Lidarr`)

`/var/lib/lidarr`

## OS X

`/Users/$USER/.config/Lidarr (~/.config/Lidarr)`

## Synology

`/usr/local/Lidarr/var/.config/Lidarr`

`/volume1/@appstore/Lidarr/var/.config/Lidarr`

## QNAP

`/share/MD0_DATA/homes/admin/.config/Lidarr`

`/share/CACHEDEV1_DATA/Lidarr_CONFIG`

## Docker

`/config`

- This will vary based on where the user maps `/config` to on their host system

## Argument

The `-data=` argument forces the location of the AppData folder, so your startup command may be forcing a specific location. This is required when trying to run multiple instances. On windows this would be `/data=`

The `-nobrowser` argument refrains from launching/opening the browser on startup. On windows this would be `/nobrowser`
