# Manual Steps

Taken from [here](https://www.pugetsystems.com/labs/hpc/ubuntu-22-04-server-autoinstall-iso)

- `sudo apt install p7zip`
- `7z -y x ubuntu-24.04.1-desktop-amd64.iso -osource-files`
- Move `source-files/[BOOT]` outside `source-files`
- update `source-files/boot/grub/grub.cfg`
- `touch cmes_utils/cloud-init/meta-data`
- Create `cmes_utils/cloud-init/user-data`
- `xorriso -indev ubuntu-24.04.1-desktop-amd64.iso -report_el_torito as_mkisofs` to get commands
- Replace commands with stuff. Trying this:
    ```bash
    xorriso -as mkisofs -r -V 'CMES_Ubuntu_24.04.1_LTS' \
    -o ../ubuntu-24.04.1-desktop-amd64.cmes.iso \
    --modification-date='2024082716232600' \
    --grub2-mbr ../boot_images/1-Boot-NoEmul.img \
    --protective-msdos-label \
    -partition_cyl_align off \
    -partition_offset 16 \
    --mbr-force-bootable \
    -append_partition 2 28732ac11ff8d211ba4b00a0c93ec93b ../boot_images/2-Boot-NoEmul.img \
    -appended_part_as_gpt \
    -iso_mbr_part_type a2a0d0ebe5b9334487c068b6b72699c7 \
    -c '/boot.catalog' \
    -b '/boot/grub/i386-pc/eltorito.img' \
    -no-emul-boot \
    -boot-load-size 4 \
    -boot-info-table \
    --grub2-boot-info \
    -eltorito-alt-boot \
    -e '--interval:appended_partition_2_start_3026280s_size_10144d:all::' \
    -no-emul-boot \
    .
    ```
It creates but something it broken during the install. Need to edit user-data