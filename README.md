# OmarchyOs-DualBoot-Guide
A comprehensive guide for newbie arch users to install or test omarchy os alongside windows



# The only omarchy dual boot setup guide you will ever need

*You need to have a free space partition if you want to dual boot alongside your another os.*

1. First thing first boot your usb drive using rufus 

    Rufus:
 - https://rufus.ie/en/

    Omarchy Os file
 - https://iso.omarchy.org/omarchy-3.0.2.iso

> On rufus select GPT instead of MBR

2. Restart the computer / laptop and get into the usb drive

3. Keep going with the omarchy install by default . You need to stop when it shows your whole nvme ssd. Don't go any further. If you go and do something you might lose your everything.

4. Press `Esc` Then choose > Quit then hit enter . Again choose > Quit then hit enter

5. now you are in the `root@archiso` terminal 

6. type `lsblk` | see your drive name it would be something like `nvme0n1`

7. then type `cfdisk /dev/nvme0n1` to see your free space partition

8. select it choose `New` from below . Resize it to `1G` and make the type `EFI system` from the type option. Now, select the remaining free space i am assuming it has `178G` now just click on the `New`. 

9. You need to see two different thing 
    - 1G EFI system
    - 178G LinuxFileSytem

10. Now select `write` from the below and type `yes` the changes will be made then `quit` to get back into the `root@archiso` terminal

11. The formatting type the command below to format the drives 

- For the `1G` drive we need to format it like this. 
 ---
 `mkfs.fat -F32 /dev/< your 1G drive name>`

> In my case i have used this

 *mkfs.fat -F32 /dev/nvme0n1p5*




- For `178G` drive you need to format it to btrfs file system.
--- 
`mkfs.btrfs /dev/< your 178G drive name >`

> In my case i have used this

*mkfs.btrfs /dev/nvme0n1p6*

---

12. Now we have formatted it now the mounting

Carefully follow the steps


* `178G` drive mounting
    - `mount /dev/ < your drive name > /mnt`

> In my case i have used 

*mount /dev/nvme0n1p6 /mnt*

* `1G` drive mounting
  - `mkdir /mnt/boot`
  - `mount /dev/nvme0n1p5 /mnt/boot`

> In my case i have used 

*mkdir /mnt/boot*

*mount /dev/nvme0n1p6 /mnt/boot*


13. Now the formatting and mounting done now we have to install 

> type archinstall

Give the properties as below and hit the install


1. Select your closet mirror server
2. Disk configuration >> Pre mounted >> type `/mnt` | hit enter then back
3. Change Hostname(optional) if you want to
4. Bootloader >> select `Limine`
5. Authentication >> setup root password and create a user
6. Application >> Audio >> Pipewire 
7. Network >> Copy ISO network config
8. Timezone >> select your time zone

9. Install

> Don't select Profile simply don't touch it. I repeat don't touch it leave as it is.

After clicking on the Install it will start install just simply press yes to make changes to proceed further.

14. Reboot

15. You will see a terminal because we haven't select any profile 

16. now type 
`curl -fsSL https://omarchy.org/install | bash` and give permission wait till the install is finished.

17. Enjoy Omarchy with dual boot  ^-^
