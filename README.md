#### Swap space/partition is space on a disk created for use by the operating system when memory has been fully utilized. It can be used as virtual memory for the system; it can either be a partition or a file on a disk.

#### we will create a swap file of size 2GB using the dd command as follows. Note that bs=1024 means read and write up to 1024 bytes at a time and count = (1024 x 2048)MB size of the file.

```
[root@ip-172-31-42-41 /]# touch swapfile

We will create a swap file of size 2GB using the dd command as follows. Note that bs=1024 means read and write up to 1024 bytes at a time and count = (1024 x 2048)MB size of the file.

[root@ip-172-31-42-41 /]# dd if=/dev/zero of=/swapfile bs=1024 count=2097152
2097152+0 records in
2097152+0 records out
2147483648 bytes (2.1 GB) copied, 15.1102 s, 142 MB/s

[root@ip-172-31-42-41 /]# du -sch swapfile
2.0G    swapfile
2.0G    total
```

#### Setting appropriate permissions on the file, make it readable only by root user 

```
[root@ip-172-31-42-41 /]# chmod 600 swapfile
```
#### Now setup the file for swap space with the mkwap command.

```
root@ip-172-31-42-41 /]# mkswap swapfile
Setting up swapspace version 1, size = 2 GiB (2147479552 bytes)
no label, UUID=697bc014-160c-463c-ad62-9c9500d29170
```
#### Enable the swap file and add it to the system as a swap file

```
[root@ip-172-31-42-41 /]# swapon swapfile
```
#### Enable the swap file to be mounted at boot time. Edit the /etc/fstab file and add the following line in it.

```
/swapfile swap swap defaults 0 0
```

|Option| Explanation|
|------|------------|
|swapfile| device/file name|
|swap | defines device mount point|
|swap| specifies the file-system type|
|defaults | mdescribes the mount options|
| 0| specifies the option to be used by the dump progra|
|0| specifies the fsck command option|



