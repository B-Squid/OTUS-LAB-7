`[root@testcent ~]# cd /usr/lib/dracut/modules.d/`  
`[root@testcent modules.d]# mkdir 01test`  
`[root@testcent modules.d]# vi module-setup.sh`  
`[root@testcent modules.d]# cd 01test/`  
`[root@testcent 01test]# vi module-setup.sh`  
`[root@testcent 01test]# vi test.sh`  
`[root@testcent 01test]# ls`  
module-setup.sh  test.sh  
`[root@testcent 01test]# mkinitrd -f -v /boot/initramfs-$(uname -r).img $(uname -r)`  
`[root@testcent 01test]# lsinitrd -m /boot/initramfs-$(uname -r).img | grep test`  
test  
`[root@testcent 01test]# vi /boot/grub2/grub.cfg`  
`[root@testcent 01test]# shutdown -r -f -t 4`  
