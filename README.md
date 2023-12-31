# SysCall_HashMap
## Prepare environment
```
sudo apt-get update
sudo apt-get install build-essential linux-headers-$(uname -r)
sudo apt-get install git fakeroot build-essential ncurses-dev xz-utils libssl-dev bc flex libelf-dev bison zstd dwarves
apt source linux-image-unsigned-5.15.0-46-generic

wget https://cdn.kernel.org/pub/linux/kernel/v6.x/linux-6.1.35.tar.xz
tar -xvf linux-6.1.35.tar.xz
cd linux-6.1.35
make menuconfig
make ARCH=$(uname -m) -j$(( $(nproc) * 2 ))

```
If you find error in downloading sources due to `Public key not found`, then find the line which says
```
gpgv: Signature made Friday 16 April 2021 03:19:39 PM IST using RSA key ID XXXXXXX
```
Now downlaod a trusted key with:
```
gpg --keyserver keyserver.ubuntu.com --recv-keys XXXXXXX
```

## Hashmap in Kernel Space and store in `/proc/hashmap`
Add a new system call which can create a hashmap in the kernel space.
1. Define the syscall number: Add the following line to `arch/x86/entry/syscalls/syscall_64.tbl`:
   ```
   <syscall_number>    64    sys_store_hashmap    __x64_sys_store_hashmap
   ```
1. Add a Makefile entry: Modify the Makefile in the kernel source directory and add the following line:
   ```
   obj-y += sys_hashmap.o
   ```
1. Build and install the kernel: Build and install the modified kernel to include your new syscall. After following these steps, you can use your custom syscall in user-space programs to create the hashmap and access its contents through the `/proc/hashmap` file.
