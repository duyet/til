---
description: Manage EMR Cluster
---

# EMR

## List all services

{% tabs %}
{% tab title="Bash" %}
```bash
initctl list
```

```text
rc stop/waiting
tty (/dev/tty3) start/running, process 4367
tty (/dev/tty2) start/running, process 4365
tty (/dev/tty1) start/running, process 4361
tty (/dev/tty6) start/running, process 4373
tty (/dev/tty5) start/running, process 4371
tty (/dev/tty4) start/running, process 4369
gmetad start/running, process 8613
update-motd stop/waiting
hive-server2 stop/waiting
hadoop-mapreduce-historyserver stop/waiting
hadoop-yarn-timelineserver stop/waiting
plymouth-shutdown stop/waiting
whisper-server stop/waiting
presto-server stop/waiting
control-alt-delete stop/waiting
hive-hcatalog-server start/running, process 3941
hive-webhcat-server start/running, process 3873
livy-server stop/waiting
rcS-emergency stop/waiting
zookeeper-server start/running, process 30481
kexec-disable stop/waiting
quit-plymouth stop/waiting
hadoop-kms stop/waiting
hadoop-yarn-resourcemanager start/running, process 3582
rcS stop/waiting
prefdm stop/waiting
hadoop-httpfs stop/waiting
init-system-dbus stop/waiting
print-image-id stop/waiting
hadoop-hdfs-zkfc stop/waiting
ganglia-rrdcached start/running, process 8537
elastic-network-interfaces stop/waiting
splash-manager stop/waiting
hadoop-hdfs-journalnode start/running, process 15254
hadoop-yarn-proxyserver stop/waiting
start-ttys stop/waiting
spark-history-server stop/waiting
ranger-kms-server stop/waiting
amazon-ssm-agent start/running, process 3382
hadoop-hdfs-namenode start/running, process 12977
rcS-sulogin stop/waiting
scout-server stop/waiting
serial (ttyS0) start/running, process 4359
gmond start/running, process 8774
```
{% endtab %}
{% endtabs %}

## Status / Restart Service

```text
sudo status hive-hcatalog-server
sudo restart hive-hcatalog-server
```

## Restart Common Services

```text
sudo restart hadoop-mapreduce-historyserver
sudo restart hadoop-yarn-timelineserver
sudo restart hive-hcatalog-server
sudo restart hive-webhcat-server
sudo restart livy-server
sudo restart zookeeper-server
sudo restart hadoop-yarn-resourcemanager
sudo restart hadoop-httpfs
sudo restart hadoop-hdfs-zkfc
sudo restart hadoop-hdfs-journalnode
sudo restart hadoop-yarn-proxyserver
sudo restart spark-history-server
sudo restart hadoop-hdfs-namenode
```

