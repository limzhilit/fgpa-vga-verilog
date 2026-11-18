---
layout: home
title: FPGA VGA Driver Project
tags: fpga vga verilog
categories: demo
---

AIM: Run provided example code and modify it to show understanding

## **Template VGA Design**
### **Project Set-Up**
1. Create new project
2. Add provided files
3. Select board model
4. Set up clock
5. Generate bitstream
6. Program device 

<img src="./docs/assets/images/project.png">### **Template Code**
- `Basys3_Master.xdc` – FPGA pin assignment and timing constraints.
- `Testbench.v` – Provides test inputs for simulating the design.
- `VGAColourStripes.v` – Generates RGB pixel colours and defines the visual pattern.
- `VGASync.v` – Generates VGA synchronisation signals and pixel coordinates.
- `VGATop.v` – Top-level module connecting the clock, VGA timing and colour generation modules.
<img src="./docs/assets/images/sources.png">

## **My VGA Design Edit**
- I attempt a first change to the code with the examples shown by lecturer which include reducing the stripes to 3 and setting the colour.
- I changed the col variable with the row variable to produce horizontal stripe with different colours. 
- I divide row and col by a width and XOR them and AND with 1 so the least significant bit is 0 if both divided row and col are even else 1 [if (((row / 40) ^ (col / 40)) & 1'b1)]
- Added a clock counter and an offset to flip the checker 
- Changed the formula of the offset for a smooth diagonal movement


### **Simulation**
- Set the parameter to a smaller unit to reduce simulation time and make waveforms easier to observe
<img src="./docs/assets/images/simulation.png">


### **RTL Analysis**

RTL Analysis (Register Transfer Level Analysis) is a stage in FPGA design where Vivado examines your Verilog code and translates it into a hardware representation.
Below shows the schematic at the RTL:
<img src="./docs/assets/images/rtl-analysis.png">
<img src="./docs/assets/images/rtl-analysis-close.png">
Closer up we can see the individual gates implementing the logic that is programmed in code for example ADD, DIVIDE, XOR, etc...

### **Synthesis and Implementation Analysis**
In the implementation schematics, each bit in hcount have a look up table (LUT)
<img src="./docs/assets/images/implementation.png">
<img src="./docs/assets/images/implementation-lut.png">

1. Synthesis schematic
Synthesis converts your Verilog RTL into FPGA logic components, such as:
- LUTs (Look-Up Tables)
- Flip-flops
- Multiplexers
- Carry chains
- Other FPGA resources
It determines what hardware needs to exist.
2. Implementation schematic
Implementation takes the synthesised netlist and performs:
- Optimisation: Further optimises the circuit.
- Placement: Assigns logic components to physical locations on the FPGA.
- Routing: Connects the components using physical FPGA routing resources.
It determines where the hardware goes and how the components connect physically.


### **Demonstration**
<img src="./docs/assets/images/first-change.jpg">
<img src="./docs/assets/images/second-change.jpg">
<img src="./docs/assets/images/third-change.jpg">

<video controls width="100%">
  <source src="./docs/assets/videos/fourth-implementation.mp4" type="video/mp4">
  Your browser does not support HTML video.
</video>

<video controls width="100%">
  <source src="./docs/assets/videos/fifth-implementation.mp4" type="video/mp4">
  Your browser does not support HTML video.
</video>

### **Additional**
In a monitor, each row has a wire to activate the row, and each column have 3 datalines for RGB respectively.
