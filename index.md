## Installing Arch Linux

1. Boot from media into installation shell.
![arch_install_boot_menu](https://quixotictendencies.github.com/quix-arch/arch_install_boot_menu.png)
![arch_install_login_shell](https://quixotictendencies.github.com/quix-arch/arch_install_login_shell.png)
2. Update repositories.
```zsh
pacman -Syy
```
3. Install reflector and run it to sort mirrorlist.
```zsh
pacman -S reflector --noconfirm
reflector -c "United States" -f 12 --save /etc/pacman.d/mirrorlist
```
Replace `United States` with your own location if necessary.
4. Set up target drive.
```zsh
cfdisk /PATH/TO/DEVICE
```
Example: /dev/sda
Partition target drive as is appropriate. For new/practicing users on a virtual machine, the following sequence is recommended: `DOS` => `[New]` => `Partition size: Default` => `[primary]` => `[Bootable]` =>  `[Write]` => `yes` => `[Quit]`
```zsh
mkfs.ext4 /dev/sda1
mount /dev/sda1 /mnt
```

5. Install base system.
```zsh
pacstrap /mnt base base-devel linux dhcpcd nano
```
6. Generate fstab.
```zsh
genfstab -U -p /mnt /mnt/etc/fstab
```
7. Chroot into system.
```zsh
arch-chroot /mnt
```
8. Set up locales and clock.
```bash
nano /etc/locale.gen
```
```bash
locale-gen
ln -sf /usr/share/zoneinfo/SUPERZONE/ZONE /etc/localtime
hwclock --systohw --utc
```
Note: Replace `SUPPERZONE` with your geographical region and `ZONE` with a city corresponding to your time zone. Example: `America/Los_Angeles`
9. Set hostname and a basic hosts file.
```bash
echo HOSTNAME > /etc/hostname
nano /etc/hosts
```
![arch_hosts](https://quixotictendencies.github.com/quix-arch/arch_install_hosts.png)
10. Set root password.
11. Intall grub and sudo.
12. Enable dhcpcd.
13. Reboot into system.
14. Add admin user and tweak sudoers.
15. Log out of root and into admin.
16. Install a window manager or desktop environment (optional).
