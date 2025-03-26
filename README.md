# Things to do

Read this! https://canonical-subiquity.readthedocs-hosted.com/en/latest/explanation/cloudinit-autoinstall-interaction.html

- Figure out if we can reasonably do user input
- Configure cloud-init ansible play
- Configure cloud-init Networkmanager
- Create ARM version
  
  Having trouble trying to emulate Raspi4b. This is the best I can do but there are memory errors and it doesn't boot completely. You must have Qemu 9.2. You must extract the vmlinuz kernel file and uncompress. You also need the dtb file associated with the 4b. Both can be found on the img file.
  
  ```bash
  ./qemu-system-aarch64 -M raspi4b -serial mon:stdio -display gtk -kernel /home/odtebja/Desktop/twb/playground/test/cmes_ubuntu_iso_create/24.04/vmlinuz -dtb /home/odtebja/Desktop/twb/playground/test/cmes_ubuntu_iso_create/24.04/bcm2711-rpi-4-b.dtb -append "earlycon=pl011,mmio32,0xfe201000 console=ttyAMA1,115200 root=LABEL=writable rootfstype=ext4 rootwait" --initrd /home/odtebja/Desktop/twb/playground/test/cmes_ubuntu_iso_create/24.04/initrd.img -sd /home/odtebja/Desktop/twb/playground/test/cmes_ubuntu_iso_create/24.04/ubuntu-24.04.2-preinstalled-desktop-arm64+raspi.cmes.img -netdev user,id=mynet,hostfwd=tcp::2222-:22 -vnc :5
  ```