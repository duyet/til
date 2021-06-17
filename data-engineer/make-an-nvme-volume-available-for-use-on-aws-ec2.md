# Make an NVMe volume available for use on AWS EC2

The root device is `/dev/xvda`. The attached volume is `/dev/xvdb`, which is not yet mounted.

```bash
[ec2-user ~]$ lsblk
NAME    MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
xvda    202:0    0    8G  0 disk
-xvda1  202:1    0    8G  0 part /
xvdb    202:80   0   10G  0 disk
```

TL;DR

```bash
sudo mkfs -t xfs /dev/xvdb
sudo mkdir /data
sudo mount /dev/xvdb /data

ls -la /data
```

[https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ebs-using-volumes.html](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ebs-using-volumes.html)

