# Zephyr-OS-and-QEMU-on-ARM-M33
Steps to setup Zephyr OS on QEMU for ARM M33 controller. MPS2-AN521 is a ARMv8 based microcontroller that supports Trustzone. This project shows the steps to emulate Zephyr OS on MPS2-AN521 on QEMU emulator.

Run these on Linux terminal

$ sudo apt install --no-install-recommends git cmake ninja-build gperf \
ccache dfu-util device-tree-compiler wget \
python3-dev python3-pip python3-setuptools python3-tk python3-wheel xz-utils file \

$ make gcc gcc-multilib g++-multilib libsdl2-dev

$ pip3 install --user -U west

$ echo 'export PATH=~/.local/bin:"$PATH"' >> ~/.bashrc

$ source ~/.bashrc

$ west init ~/zephyrproject

$ cd ~/zephyrproject

$ west update

$ west zephyr-export

$ pip3 install --user -r ~/zephyrproject/zephyr/scripts/requirements.txt

$ wget https://github.com/zephyrproject-rtos/sdk-ng/releases/download/v0.12.3/zephyr-sdk-0.12.3-x86_64-linux-setup.run

$ chmod +x zephyr-sdk-0.12.3-x86_64-linux-setup.run

$ ./zephyr-sdk-0.12.3-x86_64-linux-setup.run -- -d ~/zephyr-sdk-0.12.3

$ cd $ZEPHYR_ROOT/samples/hello_world/

$ mkdir build

$ cd build

$ west build -p -b mps2_an521 zephyr/samples/hello_world

$ qemu-system-arm -M mps2-an521 -device loader,file=<path_to_zephyr.elf file> -serial stdio

 
