# fuzz_stagefright
[SK Nugu] To fuzz stagefright lib using beagleboard xm

## 1. sdcard format
> export DISK=/dev/sdX  # sdX : your sdcard location => ex) /dev/sdb, /dev/sdc, /dev/sdd, ...
> 
> * option 1) delete entire data in sdcard
> 
> sudo dd if=/dev/zero of=${DISK} bs=1M
> 
> * option 2) if you want to delete only sdcard's partion table and label, use this!!
> 
> sudo dd if=/dev/zero of=${DISK} bs=1M count=20

## 2. get prebuilt android ICS img for beagleboard xm 
> wget https://storage.googleapis.com/google-code-archive-downloads/v2/code.google.com/rowboat/beagleboard-xm.tar.gz
> 
> tar xvfs beagleboard-xm.tar.gz
> 
> cd beagleboard-xm/

## 3. run edited mkmmc shell script !!
- partisioning sdcard

- copy compiled android img to sdcard

- file system permision setting

> wget https://raw.githubusercontent.com/Oss9935/fuzz_stagefright/master/mkmmc_android_new.sh
> 
> chmod +x mkmmc_android_new.sh
> 
> sudo ./mkmmc_android_new.sh $DISK    # use your sdcard
> 
> sudo chmod 777 –R /media/\`id | awk '{print $1}' | cut -f 2 -d "(" | cut -f 1 -d ")"\`/rootfs
