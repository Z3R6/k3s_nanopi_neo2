## Overview

The goal of [this project][k3s_nanopi_neo2] is to provide an simple instruction for spin up k3s cluster for home automation

## Requirements 

1. At least two [NanoPi NEO2-LTS](https://www.friendlyarm.com/index.php?route=product/product&product_id=180)
2. For each device need Micro SD SDHC MicroSD Memory Card Class 10
3. Cooling system Heat Sink for NanoPi NEO/NEO2/Air/NEO Plus2 and recommended use funs 20x20x8мм or 20x20x6мм 5v
4. All devices need to be on one flat network desirable in one switch
5. Internet Access (Ethernet or Wifi, required to complete packages installation)


## OS installation

Download DietPi OS [image](https://dietpi.com/downloads/images/DietPi_NanoPiNEO2-ARMv8-Stretch.7z)

## Write to SD card using Windows
1. Extract the Linux image. Insert a TF card into a Windows PC and run the win32diskimager utility as administrator. On the utility's main window select your TF card's drive, the wanted image file and click on "write" to start flashing the TF card.

## Write to SD card using Linux

1. Find the device (eg: /dev/sdb1) you need to write to by using blkid or mount.
2. Double check that you have the correct dev path for your SD card (eg: /dev/sdb1).
3. Unmount the SD card and all its partitions by using umount /dev/sdb?.
4. Write the image using dd if=/path/to/DietPi_vXX.img of=/dev/sdb.


For more detailed information you can navigate on [link](https://dietpi.com/phpbb/viewtopic.php?f=8&t=9#p9)

## Prerequisites

1. Configure static IP for each node [link](https://dietpi.com/phpbb/viewtopic.php?f=8&t=14)
2. Configure hostname. For example for master node, echo master01>/etc/hostname.
3. Conficure hosts file. For example for master node :
        
        127.0.0.1    localhost.localdomain localhost
        127.0.1.1    master01
        192.168.1.200 master01.home.local

## k3s installation
  
### Master node
  
  1. Master node installation, curl -sfL https://get.k3s.io | sh -
  2. Check for Ready node, takes maybe 30 seconds, k3s kubectl get node

### Agent node

  1. For agent installation need token to join in cluster on master node run cat /var/lib/rancher/k3s/server/node-token
  2. Join agent in cluster url -sfL https://get.k3s.io |K3S_URL=https://MASTER_IP:6443 K3S_TOKEN=TOKEN sh -
  3. Check for Ready node, takes maybe 60 seconds, k3s kubectl get node

### Save config 
  
  1. On master node in home directory create .kube directory
  2. Copy config file to .kube directory cp /etc/rancher/k3s/k3s.yaml ~/.kube/config

### Note
  
  More detailed information regarding installation, update or delete cluster you can find [link](https://github.com/rancher/k3s)

## Helm installation (in our case it will install in master node)
  
  1. Download arm helm package curl -O https://get.helm.sh/helm-v2.14.1-linux-arm64.tar.gz
  2. Untar it tar -zxvf helm-v2.14.1-linux-arm64.tar.gz
  3. Move binary mv linux-arm64/helm /usr/local/bin/helm






