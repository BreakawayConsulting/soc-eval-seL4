# i.MX 8M

*Initial publication date:* 2020-6-15

i.MX 8M is a family of *application processors* from NXP.

A general overview of the family is available from the [manufacturer website](https://www.nxp.com/products/processors-and-microcontrollers/arm-processors/i-mx-applications-processors/i-mx-8-processors/i-mx-8m-family-armcortex-a53-cortex-m4-audio-voice-video:i.MX8M).


## High-level Specs

* Quad or dual-core Cortex A-53 + Cortex M0
* GPU / VPU
* PCIe / USB / SDHC / Ethernet
* PWM / GPIO / 4 x UART / 4 x I2C / 3 x SPI
* MIPI-DSI / MIPI-CSI2 / HDMI
* 5 x SAI / SPDIF
* JTAG / Debug


## Documentation Availability

When selecting an SoC for use on seL4 it is very important that documentation is readily available.
It is often desirable in an seL4 based system to be writing device drivers from scratch.
Additionally, the details around various security related hardware is extremely important.

The i.MX series of processor has a reputation for open availability of documentation.

The processor reference manual is freely available after registration from the NXP website.

For reference, this evaluation is based on the manual titled: **i.MX 8M Dual/8M QuadLite/8M Quad Applications Processors Reference Manual**.
It has a documentation number: **IMX8MDQLQRM**.
The documentation release used is: **Rev. 3, 04/2020**.

Due to copyright restrictions the manual is not directly provided in this evaluation.


## Target Use Cases

According to NXP the target use cases for this family of SoCs is *industrial* and *smart home*.

The set of peripherals and compute power make this a relatively good general purpose SoC, which is likely to be suitable for many seL4 applications.


## Product Availability

There are two interesting products where this SoC is in use (or will be):

The first is the [Librem 5](https://puri.sm/products/librem-5/) mobile phone, and the second is the [MNT Reform](https://www.crowdsupply.com/mnt/reform) laptop.

Both the devices are designed with openness, security and privacy in mind (although this report does not attempt to make any evaluations as to the security posture of these products).

The availability of these products makes this SoC an attractive target for seL4 support.


## Evaluation / Development Kit

NXP provides the [MCIMX8M-EVK](https://www.nxp.com/design/development-boards/i-mx-evaluation-and-development-boards/evaluation-kit-for-the-i-mx-8m-applications-processor:MCIMX8M-EVK) as an evaluation kit for development purposes.

The board exposes most of the peripherals allowing development of drivers.


## Security Aspects

The SoC provides a *resource domain controller* (RDC) which, in effect, is an I/O MMU.
Tis allows for limits to be put on the memory and peripherals available to specific bus masters.

The RDC only allows for four individual *resource domains*.
Depending on the application this could limit the extent to which isolation is provided.
However, given the lack of any I/O MMU in many similarly target SoCs this is a welcome addition.

The SoC includes a *high assurance boot* (HAB) implementation in ROM.
This appears suitable for providing a secured boot process.

It should be noted that the implementation of HAB in prior i.MX SoC-s [has a vulnerability](https://blog.quarkslab.com/vulnerabilities-in-high-assurance-boot-of-nxp-imx-microprocessors.html).


## Summary

This SoC is a highly attractive target SoC for an seL4 based project.