# NASSCOM_VSD_VLSI_Soc_design

![image](https://github.com/user-attachments/assets/4344ac2a-3b55-45de-b0df-c692f1febeb0)

NASSCOM-PD 23Apr-6May_2025

Welcome to documentation for the VSD-IAT workshop on VLSI SoC design! This repository contains my daily learnings, notes, and hands-on work throughout the course.

This workshop focuses on Open-Source ASIC Physical Design Flow, using tools like OpenLane, Magic VLSI, and the Sky130 PDK. Goal is to get skills in chip design using free and open-source tools. My personal goal is not to become a chip-designer, i want have a good understanding how process is whorking, litte bit of physics and good understaning of the tolls which are involved in the process.

## it not finished and current work in progress!!!!

# Day 1 - Introduction & Synthesis
<details>
<summary> Introduction & Synthesis </summary>

- Introduction to QFN-48 Package, chip, pad,core, die and IP's
- Introduction to RISC-V
- From Spftware Application to Hardware

- Introduction to all componenes of open-source digital asic design
- Simplified RTL2GDS flow
- Introduction to OpenLANE and Strive chipsets
- Introduction to OpenLANE detailed ASIC design flow

- OpenLANE Directory structure in detail
- Design Preparation Steps
- Review files after design prep and run synthesis
- OpenLANE Project Git Link Description
- Steps to characterize synthesis result

### What is OpenLANE

[OpenLANE](https://github.com/efabless/openlane) is an automated RTL to GDSII flow which includes various open-source components such as OpenROAD, Yosys, Magic, Fault, Netgen, SPEF-Extractor. It also facilitates to add custom design exploration and optimization scripts. The detailed diagram of the OpenLANE architecture is shown below:

![image](https://github.com/user-attachments/assets/77ec7746-86c1-4919-a37c-2d5d2bfe50e5)


## Lab - screenshot

[start openlane]![image](https://github.com/user-attachments/assets/dee4eda9-da46-4da9-a694-f0e3668c8960)

[picorv32a]![image](https://github.com/user-attachments/assets/cb9d2afb-a570-49db-b2df-824806b410db)

prep directoryy structure

![image](https://github.com/user-attachments/assets/21a89c72-36aa-4038-9454-25fa45cd556e)

check if run-directory have been created

[run_check]![image](https://github.com/user-attachments/assets/0ea08720-0c01-40c7-adf3-9bf83040558f)

run synthesis

[synthesis]![image](https://github.com/user-attachments/assets/9e8d69bc-7ef3-4211-80e8-4f429aebb9f3)

picorc32a statistics

[statistics]![image](https://github.com/user-attachments/assets/abff69ed-65df-41a9-a16e-5775bbdd5511)

check synthesis result

[synthesis result]![image](https://github.com/user-attachments/assets/1108ed53-a7ca-41c8-8ae8-b2c09ad075b9)

check yosys_4.stat.rpt

![image](https://github.com/user-attachments/assets/da13cec1-00bd-4c22-8606-b4e3055e040d)



additional infos about openlane visit githup repository [openlane](https://github.com/efabless/OpenLane.git)

check youtube for "fossi dial up"

[fossi]![image](https://github.com/user-attachments/assets/47e9dae8-21a0-47ac-ac81-e8e3bc5b43ef)





</details>

# Day 2 - Floorplanning & Placement
<details>
<summary> Interceptiopn of open-source EDA, OpenLANE, Sky130 PDK </summary>

- Chip Floor planing conciderations
  - Utilization factor and acpect ratio
  - Concept of pre-placement
  - De-coupling capacitors
  - Pin placement and logical cell placement blockage
  - Steps to run floor using OpenLANE
  - Review floorplan files and steps to view floorplan
  - Review floorplan layout in Magic
  
- Library Binding and Placement
  - Netlist binding and initial place design
  - Optimize placement using estimated wite-length and capacitance
  - Final plancement optimization
  - Need for libraries and characterizatiion
  - Congestion aware placement using RePlace
  
- Cell design and characterization flows
  - Inputs for cell design flow
  - Circuit design steps
  - Layout design steps
  - Typical characterization flow
  
- General timing characterization parameter
  - Timing threshold definition
  - Propagation delay and transition time
  

</details>

# Day 3 -Standard Cell Design & Characterization
<details>
<summary> Standard Cell Design & Characterization using Magic Layout and ngspice characterizsation</summary>

- Labs for CMOS inverter ngspice simulation
  - IO placer revision
  - SPICE deck creation for CMOS inverter
  - SPICE simulation lab for CMOS inverter
  - Switching Threshold Vm
  - Static and dynamic simulation of CMOS inverter
  - Lab steps to git clone vsdstdcelldesign
  
- Inception of Layout CMOS fabrication process
  - Create Active regions
  - Formation of N-well and P-well
  - Ligthly dopes drain (LDD) formation
  - Source drain formation
  - Local interconnection formatation
  - Higher level formation
  - Lab introduction to Sky130 basic layers layout and LEF using inverter
  - Lab steps to create std cell layout and extraction spice netlist
 
- Sky130 Tech File Labs
  - Lab steps to create final SPICE deck using Sky130 tech
  - Lab steps to characterize inverter using sky130 model files
  - Lab introduction to Magic tool option and DRC rules
  - Lab introduction to ky130 pks's and steps to download labs
  - Lab introduction to Magic and steps to load Sky130 tech-rules
  - Lab exercise to fix poly.9error in Sky130 tech-file
  - Lab exercice to implöement poly resistors spacing to diff and tap
  - Lab challenge excercise to describe DRC error as geometrical construc
  - Lab exercise to find missing or incorrect rules and fix them
 
</details>

# Day 4 - Timing Analysis & Clock Tree Synthesis (CTS)
<details>
<summary> Timing Analysis & Clock Tree Synthesis (CTS) and importance of good clock trees</summary>

- Timing modelling using delay tables
  - Lab steps to convert grid info to track info
  - Lab step to convert magiv layout to std cell LEF
  - Introduction to timing libs and steps to inculde new cell in synthesis
  - Introduction to delay tables
  - Delay table usage Part 1
  - Delay table using Part 2
  - Lab steps to configure systhesis stetting to fix slack and inculde vsdinv
 
   
- Timing analysis with idesl clocks using openSTA
  - Setup timing analysis and introduction to flip-flop setup time
  - Introduction to clock jitter and uncertainty
  - Lab steps to configure OpenmSTA for post-synth timing analysis
  - Lab steps to optimize synthesis to reduce setup violations
  - Lab steps to do basic timing ECO
 
  
- Clock tree synthesis TritonCTS and signal intrgitry
  - Clock tree routing and buffering using H-Tree alogorithm
  - Crosstalk and clock net shielding
  - Lap steps to run CTS using Triton CTS
  - Lab steps to verify CTS runs
 

- Timing analysis with real clocks using open STA
  - Setup timing analysis using real clocks
  - Hold timinng analysis using real clocks
  - Lab steps to analyze timing with real clocks using OpenSTA
  - Lab steps to execute OpenSTA with rigth timing libraries and CTS assignment
  - Lab steps to observe impact of bigger CTS buffers on setup and hold timing
  
</details>

# Day 5 - RTL-to-GDS Flow Completion using tritonRoute and openSTA
<details>
<summary> RTL-to-GDS Flow Completion using tritonRoute and openSTA</summary>

- Routing and design rule checks (DRC)
  - Introduction to Maze Routing and Lee algorithm
  - Lee's Algorithm conclusion
  - Design Rule Check
    
- Power Distribution Network and routing
  - Lab steps to build power distribution network
  - Lab steps from power straps to std cell power
  - Basic of global and drtail routing and configure TritonRoute
    
- TritonRoute Features
  - TritonRoute feature 1 - Honors pre-processing route guide
  - TritonRoute Feature 2 & 3 - Inter-guide connectivity and intra- & inter-layer routing
  - TritoRoute methode to handle connectivity
  - Routing topology algorithm and final files list post-route
  
</details>

