
# Building Xinu for riscv-64 qemu

## 1. Install risc-v toolchain and qemu  

The build process has been tested with this toolchain: [riscv-collab](https://github.com/riscv-collab/riscv-gnu-toolchain.git)
that contains both.  

``git clone https://github.com/riscv-collab/riscv-gnu-toolchain.git``

### Toolchain

Run these commands from `riscv-gnu-toolchain` directory:  

``./configure --prefix=/opt/riscv``  
``sudo make``

### Qemu

``./configure --enable-qemu-system --prefix=/opt/riscv``  
``sudo make build-sim SIM=qemu``

## 2. Compile Embedded Xinu  

Run this command from Xinu `compile` directory:  

``make PLATFORM=riscv64-qemu COMPILER_ROOT=/opt/riscv/bin/riscv64-unknown-elf-``  

(you may edit `Makefile` variables accordingly in order to only type `make`).  

The build process will produce the `xinu.elf` binary in the same directory.

## 3. Running  

Run this command from Xinu `compile` directory:  

``/opt/riscv/bin/qemu-system-riscv64 -M virt -kernel xinu.elf -bios none -nographic``  

Type `Ctrl-a x` to exit qemu.


## Bugs and Missing Features

The `riscv64-qemu` platform does not yet support networking.
