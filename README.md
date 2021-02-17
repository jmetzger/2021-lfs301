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
