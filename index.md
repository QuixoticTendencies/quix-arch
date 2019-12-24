## Installing Arch Linux

1. Boot from media into installation shell.
![arch_install_boot_menu](https://quixotictendencies.github.com/quix-arch/arch_install_boot_menu.png)
![arch_install_login_shell](https://quixotictendencies.github.com/quix-arch/arch_install_login_shell.png)
2. Update repositories.
```bash
pacman -Syy
```
3. Install reflector and run it to sort mirrorlist.
```bash
pacman -S reflector --noconfirm
reflector -c "United States" -f 12 --save /etc/pacman.d/mirrorlist
```
Replace `United States` with your own location if necessary.

4. Set up target drive.
```bash
cfdisk /PATH/TO/DEVICE
...
mkfs.ext4 /PATH/TO/PARTITION
mount /PATH/TO/PARTITION /mnt
```

4.5 If you made a swap partition:
```bash
mkswap /PATH/TO/PARTITION
swapon /PATH/TO/PARTITION
```

5. Install base system.
```bash
pacstrap /mnt base base-devel linux dhcpcd nano
```
6. Generate fstab.
```bash
genfstab -U -p /mnt /mnt/etc/fstab
```
7. Chroot into system.
```bash
arch-chroot /mnt
```
8. Set up locales and clock.
```bash
nano /etc/locale.gen
```
```bash
locale-gen
ln -sf /usr/share/zoneinfo/CONTINENT/ZONE /etc/localtime
hwclock --systohc --utc
```

9. Set hostname and a basic hosts file.
```bash
echo HOSTNAME > /etc/hostname
nano /etc/hosts
```
![arch_hosts](https://quixotictendencies.github.com/quix-arch/arch_hosts.png)

10. Set root password.
```bash
passwd
```

11. Intall grub and sudo.
```bash
pacman -S grub sudo
grub-install /PATH/TO/DEVICE
grub-mkconfig -o /boot/grub/grub.cfg
```

12. Enable dhcpcd.
```bash
systemctl enable dhcpcd
```

13. Reboot into system.
```bash
exit
reboot
```

14. Add admin user and tweak sudoers.
```bash
useradd -m -g users -G wheel -s /bin/bash USERNAME
sed -i '82 s/#//' /etc/sudoers
```

15. Log out of root and into admin.
```bash
exit
```

16. Install a window manager or desktop environment (optional). Example procedure for i3 window manager:
```bash
sudo pacman -S pulseaudio pulseaudio-alsa alsa-utils xorg xorg-xinit i3-wm dmenu i3status chromium xfce4-terminal
echo exec i3 > ~/.xinitrc
alsactl init
startx
```
