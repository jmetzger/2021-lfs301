# LFS 301 - Notes for 16.02. - 20.02.2021

## Agenda 

  1. [Exercises](exercises.md)
  2. [Example-exam](example-exam.md)
  
## Supported platforms for exam 

  * https://docs.linuxfoundation.org/tc-docs/certification/lf-candidate-handbook/exam-preparation-checklist

## Userdata in cloud-init for digitalocean 

```
#cloud-config
users:
  - name: 11trainingdo
    shell: /bin/bash

runcmd:
  - sed -i "s/PasswordAuthentication no/PasswordAuthentication yes/g" /etc/ssh/sshd_config
  - echo " " >> /etc/ssh/sshd_config 
  - echo "AllowUsers 11trainingdo" >> /etc/ssh/sshd_config 
  - echo "AllowUsers root" >> /etc/ssh/sshd_config 
  - systemctl reload sshd 
  - echo "11trainingdo ALL=(ALL) ALL" > /etc/sudoers.d/11trainingdo
  - chmod 0440 /etc/sudoers.d/11trainingdo
```

## Use scheduler 

```
cat /sys/block/vda/queue/scheduler
```

## find with own script.sh 

```
# /usr/loca/bin/script.sh -> do chmod u+x /usr/local/bin/script.sh
#!/bin/bash 

echo "datei gefunden"$1
```

```
find /root -inum 3318 -exec script.sh {} \;
```

## find with regeex 

```
find /proc ! -path '*/[0-9]*/*' -iname 'sched*' 
```

## remount option on error 

```
/dev/sda1  /mnt/platte  ext4    errors=remount-ro  0 0 
```

## KVM - check if Hardware of host supports that 

```
grep -e vmx -e svm /proc/cpuinfo
```

## docker-compose 

  * docker orchestrieren (mehrere Container) 

## ssh - key 

```
# 1. create key 
client1# ssh-keygen (please with password !!) 
# 2. public -> to -> server 2 
client1# ssh-copy-id 
# if wanted use ssh-agent
client1# eval $(ssh-agent)
# adds private-key in default location ~/.ssh/id_rsa 
# and you are forced to enter password once
# then you can connect without private-key-password
# as long as session
client1# ssh-add 
#
ssh 11trainingdo@server2
```

## Samba (smb) und AD-Server 

  * http://www.monoplan.de/samba-als-ads.html

## Parted and gparted 

  * gparted is a gnome frontend for parted.
  * it is not developed by the same developer
  * Developer of parted is Andrew Claussen and .... 
    * Ref: https://en.wikipedia.org/wiki/GNU_Parted
  * gparted used parted under the surface, see also faq's (more specific libparted)
    * https://gparted.org/faq.php
    * https://en.wikipedia.org/wiki/GParted
  
## Benchmarking with bonnie++ 

```
bonnie++ | tail -n 1 | bon_csv2html > $(date +"%Y.%m.%d.%S.%N")_bonnie.html
``` 

## Ansible 

  * https://github.com/jmetzger/ansible-galera-cluster-maxscale
