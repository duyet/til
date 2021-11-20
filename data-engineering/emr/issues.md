# Issues

## 1/1 local-dirs are bad /mnt/yarn; 1/1 log-dirs are bad /var/log/hadoop-yarn/containers

```
du -sh /mnt/*
du -sh /mnt/yarn/*
...
```

```
sudo su -
rm -rf /mnt/yarn/usercache/livy/*
df -h
```
