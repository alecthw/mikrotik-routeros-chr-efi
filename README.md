# mikrotik-routeros-chr-efi

Build MikroTik RouterOS CHR EFI Image!

See [build.yml](.github/workflows/build.yml) for more.

Download form [release](https://github.com/alecthw/mikrotik-routeros-chr-efi/releases).

## Info

RouterOS chr-7.x has contained efi boot files. But it's partition type is `ext2`.

System can be boot from efi after changing the partition type from `ext2` to `fat`.

Other, make `Hybrid MBR`

```bash
(
echo 2 # use GPT
echo t # change partition code
echo 1 # select first partition
echo 8300 # change code to Linux filesystem 8300
echo r # Recovery/transformation
echo h # Hybrid MBR
echo 1 2 # partitions added to the hybrid MBR
echo n # Place EFI GPT (0xEE) partition first in MBR (good for GRUB)? (Y/N)
echo   # Enter an MBR hex code (default 83)
echo y # Set the bootable flag? (Y/N)
echo   # Enter an MBR hex code (default 83)
echo n # Set the bootable flag? (Y/N)
echo n # Unused partition space(s) found. Use one to protect more partitions? (Y/N)
echo w # write changes to disk
echo y # confirm
) | sudo -E gdisk /dev/nbd1
```
