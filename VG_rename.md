`[root@testcent ~]# vgs`  
  VG     #PV #LV #SN Attr   VSize   VFree  
  centos   1   2   0 wz--n- <11,55g    0  
`[root@testcent ~]# vgrename centos OtusVG`  
  Volume group "centos" successfully renamed to "OtusVG"  
`[root@testcent ~]# vi /etc/fstab`  
`[root@testcent ~]# ls /dev/mapper`  
control  OtusVG-root  OtusVG-swap  
`[root@testcent ~]# vi /etc/fstab`  
`[root@testcent ~]# vi /etc/default/grub`   
`[root@testcent ~]# vi /boot/grub2/`  
device.map  fonts/      grub.cfg    grubenv     i386-pc/    locale/       
`[root@testcent ~]# vi /boot/grub2/`  
device.map  fonts/      grub.cfg    grubenv     i386-pc/    locale/       
`[root@testcent ~]# vi /boot/grub2/`  
device.map  fonts/      grub.cfg    grubenv     i386-pc/    locale/  
`[root@testcent ~]# vi /boot/grub2/grub.cfg`  
`[root@testcent ~]# mkinitrd -f -v /boot/initramfs-$(uname -r).img $(uname -r)`  
Executing: /usr/sbin/dracut -f -v /boot/initramfs-3.10.0-957.5.1.el7.x86_64.img 3.10.0-957.5.1.el7.x86_64  
dracut module 'modsign' will not be installed, because command 'keyctl' could not be found!  
dracut module 'busybox' will not be installed, because command 'busybox' could not be found!  
.  
.  
.  
*** Creating image file done ***  
*** Creating initramfs image file '/boot/initramfs-3.10.0-957.5.1.el7.x86_64.img' done ***  
`[root@testcent ~]# reboot`  
`[root@testcent ~]# vgs`  
  VG     #PV #LV #SN Attr   VSize   VFree  
  OtusVG   1   2   0 wz--n- <11,55g    0  
  
