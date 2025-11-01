# Use LiteX on the Acorn CLE 215

# Acorn CLE 101

**The Acorn CLE 101 is a cryptocurrency mining accelerator card from SQRL that can be repurposed as a generic FPGA PCIe development board:**

![Acorn CLE 101](20251025_140851.jpg)

**It features:**

- A Xilinx Artix-7 XC7A100T FPGA (speed grade -2).
- 512 MiB of DDR3 memory with a 16-bit interface.
- 32 MiB QSPI Flash for configuration storage.
- A PCIe Gen2 x4 M.2 connector, providing access to four high-speed GTP transceivers (up to 6.6 Gb/s).
- 4 user LEDs for status or debugging.
- A JTAG connector for programming and debugging.
- 4 general-purpose I/O pins.
- 4 LVDS pair I/Os for high-speed interfacing.

*The Acorn CLE 101 shares much of its design with the NiteFury and CLE215+ boards, offering the same powerful FPGA architecture but with less onboard memory, making it a cost-effective choice for developers. These boards, once used for cryptocurrency mining, can now be found at remarkably low prices — often between 40 € and 80 € on second-hand markets — offering excellent value as FPGA development platforms for hobbyists and researchers alike. :D*

# Prepare your Acorn CLE101 for LiteX

To use the Acorn CLE215+ as a LiteX development board, the following hardware is recommended:

- A PCIe 1X to 16X powered riser adapter card (ex this one)
- A M2 NVME to PCIe Gen2 X4 adapter card (ex this one).
- A JTAG Cable (ex this one).
- A USB to TTL serial cable (ex this one).
- A Molex PICOEZMATE 6 cable (ex this one).
- 2 X 6 pin headers.
An extra PCIe riser + SATA cable will be useful if you want to create SoCs with LiteSATA.

# Prepare the JTAG and Serial adapters
The Acorn exposes the JTAG pins and general purpose IOs to 6-pin Pico-EZmate connectors. We need to create adapters for both connectors. The JTAG will be used to program the FPGA and the second connector for IOs (UART in our case):

enter image description here

You can cut the Pico-EZmate cable in half and solder the pin-headers according to the pin mapping provided:

enter image description here

You can now mount the cable adapters on the board and the board on the PCIe adapters:

enter image description here enter image description here

If not already done, make sure to install LiteX by following the LiteX installation guide and you are ready to use LiteX your board!

# RISC-V Linux in LiteX/Rocket on FPGA Artix-7 XC7A100T
## Installing Ubuntu
You can either install Ubuntu via a Virtual Machine or install it directly on an external hard drive
- For installing Ubuntu on an external hard drive, you can watch the tutorial from this link [External Hard Drive](https://www.youtube.com/watch?v=KFwA1tjZp1w&t=236s)
- For installing Ubuntu on a Virtual Machine, please watch this video [Virtual Machine](https://www.youtube.com/watch?v=Hva8lsV2nTk)
## Installing Litex
1. Install prerequisites
```
$ sudo apt update
$ sudo apt upgrade
$ sudo apt install openocd fakeroot verilator python3 meson gtkterm gawk texinfo git python3-pip bison device-tree-compiler autoconf automake autotools-dev curl python3 libmpc-dev libmpfr-dev libgmp-dev build-essential flex gperf libtool patchutils bc zlib1g-dev libexpat-dev ninja-build
```
2. Install the LiteX development environment
```
$ cd ~
$ mkdir litex
$ cd litex
$ wget https://raw.githubusercontent.com/enjoy-digital/litex/master/litex_setup.py
$ chmod +x litex_setup.py
$ ./litex_setup.py --init --install --user (--user to install to user directory)
$ ./litex_setup.py --update
```
Add to path
```
$ echo 'export PATH=$PATH:~/.local/bin' >> ~/.bashrc
```
3. Installation of cross-compiler toolchain for 64bit RISC-V
```
$ cd ~
$ mkdir riscv
$ cd riscv
$ git clone --recursive https://github.com/riscv/riscv-gnu-toolchain
```
Add to path
```
$ export PATH=$PATH:$HOME/RISCV/bin
$ echo 'export PATH=$PATH:$HOME/RISCV/bin' >> ~/.bashrc
```
## Installing Vivado
Install support packages
```
$ sudo apt install libtinfo-dev libtinfo5
```
Download the .bin installer file
```
$ sudo chmod +x ./filename.bin
$ ./filename.bin
```
Add Vivado to path
```
$ echo 'export PATH=$PATH:/tools/Xilinx/Vivado/2023.1/bin' >> ~/.bashrc
```
## Running the LiteX simulation
```
$ cd ~
$ sudo apt install libevent-dev libjson-c-dev
$ litex_sim --cpu-type=vexriscv
$ ./make.py --board=XXYY --cpu-count=X --build
$ ./make.py --board=XXYY --cpu-count=X --load
$ litex_term --images=images/boot.json /dev/ttyUSBX
```

# Run LiteX-Boards example

