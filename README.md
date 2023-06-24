# SysCall_HashMap
Add a new system call which can create a hashmap in the kernel space.
1. Define the syscall number: Add the following line to `arch/x86/entry/syscalls/syscall_64.tbl`:
   ```
   <syscall_number>    64    <syscall_name>    __x64_sys_<syscall_name>
   ```
1. Add a Makefile entry: Modify the Makefile in the kernel source directory and add the following line:
   ```
   obj-y += sys_hashmap.o
   ```
1. Build and install the kernel: Build and install the modified kernel to include your new syscall. After following these steps, you can use your custom syscall in user-space programs to create the hashmap and access its contents through the `/proc/hashmap` file.
