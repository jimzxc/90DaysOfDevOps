## Day 13 — LVM practice (loopback disk)
### Create a 1GB disk image
```bash
dd if=/dev/zero of=/tmp/disk1.img bs=1M count=1024
Attach the image as a loop device
losetup -fP /tmp/disk1.img
```

### Verify loop devices
```bash
losetup -a
```


### Example output:
```bash
/dev/loop1: [64512]:655421 (/var/lib/snapd/snaps/core22_2293.snap)
/dev/loop6: [64512]:262167 (/tmp/disk1.img)
/dev/loop4: [64512]:655530 (/var/lib/snapd/snaps/snapd_25585.snap)
/dev/loop2: [64512]:655497 (/var/lib/snapd/snaps/lxd_37397.snap)
/dev/loop0: [64512]:657411 (/var/lib/snapd/snaps/core22_2140.snap)
/dev/loop5: [64512]:655420 (/var/lib/snapd/snaps/snapd_25939.snap)
/dev/loop3: [64512]:657421 (/var/lib/snapd/snaps/lxd_37927.snap)
```
# ⚠️ NOTE
```bash
I skipped the remaining challenge tasks for now. I will continue the LVM steps (PV → VG → LV → filesystem → mount) next.
```