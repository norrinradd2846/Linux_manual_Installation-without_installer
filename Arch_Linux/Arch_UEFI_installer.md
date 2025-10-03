mkfs.fat -F 32 /dev/sda1
mkswap /dev/sda2
mkfs.ext4 /dev/sda3
mount /dev/sda3 /mnt
mkdir -p /mnt/boot/efi
mount /dev/sda1 /mnt/boot/efi
pacstrap /mnt networkmanager base base-devel sudo vim dhclient linux linux-firmware grub efibootmgr efivar xorg-server xfce4 lightdm-gtk-greeter lightdm-gtk-greeter-settings lightdm openvpn net-tools mtools
genfstab -U /mnt > /mnt/etc/fstab
arch-chroot /mnt
echo "root:amunra" | chpasswd
echo ArchwithAPT > /etc/hostname
grub-install --efi-directory /boot/efi/ --target x86_64-efi --recheck
grub-mkconfig -o /boot/grub/grub.cfg
exit
echo "Only reboot is required"
