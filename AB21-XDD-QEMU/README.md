# XPU Device Driver for AB21-QEMU/AB21-FPGA

The XPU device driver (XDD) of this project is a SW, running on the Host system, developed by the Supercomputing Technology Research Center to execute the parallel operation kernel operation of the parallel application program written in the OpenCL programming model on the XPU device, which is an emulated operation accelerator based on QEMU. The main functions and features provided by XDD are as follows.
 * XPU device registration/initialization/setting management
 * XPU device context management
 * Parallel operation queue management
 * Execution of parallel operation tasks
 * Event Management
 * XPU device memory allocation and management
## Overview
* This source code directory of XDD includes 
	- XPU Driver Library (XDL)
	- XPU Hig-level Driver (XHD)
	- XPU Platform Driver (XPD)
	- Test program (XDL-test)
* To cross compile for AArch64 (AB21Q)
* Tested on x86_64 host.
* This is not fully debugged.
* XDD can run on the AB21Q virtual machine. So, AB21Q needs to to build and installed before running XDD.

## Directories
```
XDD                                     --> XPU Device Driver (XDD) and XPU Platform Driver (XPD)
    ├── linux-source-5.4.0              --> Ubuntu kernel source
    └── xdlib                           --> XPU Driver Library (XDL) 
        └── test                        --> XDL-test application          
```
<br>
<br>

## Table of Contents
- [Environment & Prerequisites](#environment-and-prerequisites)
- [Installation](#installation)
- [Usage](#usage)
- [Authors](#authors)

<br>

## Environment and Prerequisites

- Development languages:  Gcc 10.0.4 (ARM Cross compile)
- OS:  Ubuntu 20.04 (linux-5.4.0)
- QEMU 6.2.0

<br>


## Installation 

* Build ubuntu kernel

	- before kernel compile and build, you shoud download kernel source code (https://www.kernel.org)
```
$ cd XDD/linux-5.4.0
$ cp ../u20_config .config 
$ make ARCH=arm64 CROSS_COMPILE=aarch64-linux-gnu- -j `nproc`
$ cd ..
```

* Build XDD (in supreme-k-poc/XDD)
```
$ cd XDD
$ make all
$ ls
	xd.ko                             # driver module 
	xdlib/test/test                   # XDL-test program binary
	xdlib/test/axpu_kernel_binary     # OpenCL sample kernel binary which is used by XDL-test
```

## Install and run AB21Q
* Refer to https://git.etri.re.kr/parkym/supreme-k-poc/-/blob/master/ab21sim/ab21tsim/README.md
<br>


## Usage 

## How to run XDD

* run AB21Q virtual machine image (in supreme-k-poc/ab21sim/ab21tsim/QEMU/qemu_test/test_ubuntu/)
	```
	$ cd ab21sim/ab21tsim/QEMU/qemu_test/test_ubuntu/
	$ source env.sh
	$ ./run_ubuntu_20.04_on_ab21q
	```
* in AB21Q virtual machine, copy XDD files from host 
	- use scp or sftp to your host in virtual machine
	- files to copy
		- XDD/xd.ko
		- XDD/xdlib/test/test
		- XDD/xdlib/test/axpu_kernel_binary

* load XDD module and execute XDL-test program
	```
	$ sudo insmod xd.ko
	$ ./test axpu_kernle_binary
	```
<br>
<br>

## Authors

* 김영호 &nbsp;&nbsp;&nbsp;  kyh05@etri.re.kr   
* 임은지 &nbsp;&nbsp;&nbsp;  ejlim@etri.re.kr   
* 안신영 &nbsp;&nbsp;&nbsp;  syahn@etri.re.kr   
<br>
<br>

## Version 
* XDD 2.0.0 / 2022.12.15
<br>
<br>

