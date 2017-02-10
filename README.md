# Motion Estimation Processor

Hardware implementation of [Motion Estimation](https://en.wikipedia.org/wiki/Motion_estimation) algorithm written in Verilog-HDL.
It's currently under development.

## About Motion Estimation

Motion Estimation is a process of finding motion vectors from a reference frame to the current frame.
We apply the following process for each of the macro blocks in the current frame.
We first find a block which has the lowest matching error in the search window of the reference frame.
We use sum of absolute errors between corresponding pixels.
Then, the displacement between the current macro block to the best matching macro block is motion vector.

![Figure of Motion Estimation](docs/motion_estimation.png)

## Description

- Breakingoff based motion estimation
- Only integer pixel motion estimation
- Template Block: 16x16 pixels
- Search Range  : ±24 pixels
- Supported devices
  - MU500-RX FPGA board \& MU500-7SEG 7seg LED board
  - DE1-SoC

## Required Tools

- [Icarus Verilog(>=10.0)](http://iverilog.wikia.com/wiki/Installation_Guide)
- [Altera Quartus Prime(>=15.0)](https://www.altera.co.jp/downloads/download-center.html)
- Excel 2013
- [Python 2.7](https://www.python.org/downloads/)

## How to run Simulation

1. Open `memory/memory.xlsx`
1. Click 'Create Memory' button to create `memory/memory_sw.txt` for search range memory and `memory_tb.txt` for template block memory
1. Run `make_tb.sh`
1. You will find the wave file `testbench/***.vcd`

## How to synthesis Motion Estimation Processor

1. Open `memory/memory.xlsx`
1. Click 'Create Memory' button to create `memory/memory_sw.txt` for search range memory and `memory_tb.txt` for template block memory
1. Run `make_mif.sh` to generate mif files
1. Open `fpga/fpga_top.qpf` in Altera Quartus Prime
1. Compile it

## Source Code Organization

The Motion Estimation Processor source code is organized as follows:

```text
docs/       documentation
fpga/       fpga related files
memory/     memory dependencies
rtl/        RTL files for Motion Estimation Processor
testbench/  test suites
tools/      tool for creating mif file
```

## Timing chart

![](docs/timing-chart.png)

## Block diagram

![](docs/block_diagram.png)

## Parameters

### TB\_LENGTH

Size of the template block.
The default value is `16` pixel.

### SW\_LENGTH

Size of the search window.
The default value is `64` pixel.

### PE\_OUT\_WIDTH

Bit width of the Processor Element's output.
The default value is `8` bit.

### MEMORY\_SW\_CONTENT

Path to the search window memory file which contains pixel values.
If you run on iverilog, you should specify text file. If you compile it with Quartus, you should specify mif file.
The default value is `"../memory/memory_sw.txt"`.

### MEMORY\_\TB\_CONTENT

Path to the template block memory file which contains pixel values.
If you run on iverilog, you should specify text file. If you compile it with Quartus, you should specify mif file.
The default value is `"../memory/memory_tb.txt"`.
