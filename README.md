# linux-modules

Studying about modules

# Building your kernel

Create your file system:

```
truncate -s 4G my_disk.raw
mkfs.ext4 my_disk.raw
```

Mount the file system:

```
mkdir mnt_partition
sudo mount my_disk.raw mnt_partition
```

Install debian on file system:

```
sudo debootstrap stable mnt_partition http://deb.debian.org/debian/
sudo chroot mnt_partition /bin/bash
passwd
//type your password
```


# Compile kernel

Clone [Linux repo](https://github.com/Every2/linux)

And run:

```
make defconfig
make -j$(nproc)
```

# QEMU
```
qemu-system-x86_64 \
    -drive file=my_disk.raw,format=raw,index=0,media=disk \
    -m 4G \
    -nographic \
    -kernel .linux/arch/x86_64/boot/bzImage \
    -append "root=/dev/sda rw console=ttyS0 loglevel=6" \
    --enable-kvm
``` 

# Ref

[Lkcamp tutorial](https://docs.lkcamp.dev/intro_tutorials/boot/)
