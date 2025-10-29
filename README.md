# Use LiteX on the Acorn CLE 215

# Acorn CLE 101

The Acorn CLE 101 is a cryptocurrency mining accelerator card from SQRL that can be repurposed as a generic FPGA PCIe development board:

![Acorn CLE 101](20251025_140851.jpg)

It features:

- A Xilinx Artix-7 XC7A100T FPGA (speed grade -2).
- 512 MiB of DDR3 memory with a 16-bit interface.
- 32 MiB QSPI Flash for configuration storage.
- A PCIe Gen2 x4 M.2 connector, providing access to four high-speed GTP transceivers (up to 6.6 Gb/s).
- 4 user LEDs for status or debugging.
- A JTAG connector for programming and debugging.
- 4 general-purpose I/O pins.
- 4 LVDS pair I/Os for high-speed interfacing.

The Acorn CLE 101 shares much of its design with the NiteFury and CLE215+ boards, offering the same powerful FPGA architecture but with less onboard memory, making it a cost-effective choice for developers. These boards, once used for cryptocurrency mining, can now be found at remarkably low prices — often between 40 € and 80 € on second-hand markets — offering excellent value as FPGA development platforms for hobbyists and researchers alike. :D

# Prepare your Acorn CLE101 for LiteX

To use the Acorn CLE215+ as a LiteX development board, the following hardware is recommended:

- A PCIe 1X to 16X powered riser adapter card (ex this one)
- A M2 NVME to PCIe Gen2 X4 adapter card (ex this one).
- A JTAG Cable (ex this one).
- A USB to TTL serial cable (ex this one).
- A Molex PICOEZMATE 6 cable (ex this one).
- 2 X 6 pin headers.
An extra PCIe riser + SATA cable will be useful if you want to create SoCs with LiteSATA.
