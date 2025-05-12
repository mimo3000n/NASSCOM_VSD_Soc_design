# NASSCOM_VSD_VLSI_Soc_design

![image](https://github.com/user-attachments/assets/4344ac2a-3b55-45de-b0df-c692f1febeb0)

NASSCOM-PD 23Apr-6May_2025

Welcome to documentation for the VSD-IAT workshop on VLSI SoC design! This repository contains my daily learnings, notes, and hands-on work throughout the course.

This workshop focuses on Open-Source ASIC Physical Design Flow, using tools like OpenLane, Magic VLSI, and the Sky130 PDK. Goal is to get skills in chip design using free and open-source tools. My personal goal is NOT to become a chip-designer, i want have a good understanding how process is working, litte bit of physics and good understanding of the tools which are involved in the process.

## it not finished and current work in progress!!!! - i need more time to finish class and document all lab's!!!!!!

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

- ### Chip Floor planing conciderations
  - #### Utilization factor and acpect ratio
 
    Definition and calculation of width and Hight of Core and Dia of a Chip

![11-05-2025_12-47-40](https://github.com/user-attachments/assets/6477c788-2c32-4a4b-abc4-817d038e703a)

    We use a simple netlist of 2 flip-flops and an AND and anOR gate to calulate Utilization factor and aspect Ration.
    Netlist 

![11-05-2025_12-49-10](https://github.com/user-attachments/assets/b458de7f-37e1-4ea2-a4e6-319e983c9af2)

    We replace logicgates by physical logic cells with proper dimension to calculate size of the core

![11-05-2025_12-50-37](https://github.com/user-attachments/assets/51e3391d-0143-470c-bff5-aa69dacb246c)

    assume that a standard cell have size of 1 x 1 until = 1 sq unit in size, same is valid for a flip-flop

![11-05-2025_17-12-45](https://github.com/user-attachments/assets/90dd276b-22bb-4208-842d-651b205b300e)

    remove the wires and place all cells together which rusults in 2 x 2 units = 4 sq. untis

    during production process the core and dia will be replicated multiple time on wafer to increase throuput

![11-05-2025_12-52-09](https://github.com/user-attachments/assets/e39fe0fb-134f-49d0-a984-77a0da0518f1)

    if netlist occupies the complete core we talk about a utilization of 100% or of a utilization factor of 1, which is shown on next 3 slides

![11-05-2025_12-53-02](https://github.com/user-attachments/assets/654ab2a5-7d03-4ff6-be72-5a837d603e1c)

![11-05-2025_12-54-25](https://github.com/user-attachments/assets/243a8be0-8613-4e66-b980-02d83cf37a19)

![11-05-2025_12-55-53](https://github.com/user-attachments/assets/72bcc09e-7f7e-49b4-b5c9-6186b487d9e0)

    The concept of aspect ratio is hight / width. In our example 2 untis / 2 units = 1

![11-05-2025_16-54-56](https://github.com/user-attachments/assets/20e89710-0c8c-4f02-9fff-06763f404311)

![11-05-2025_16-56-06](https://github.com/user-attachments/assets/9b3083ff-44db-4567-bde8-ed547b94e3cd)

    another example with a rectange core of 4 units / 2 units result in a differen Utilisation factor and a different acpcet ration compared to above szenario

![11-05-2025_16-56-44](https://github.com/user-attachments/assets/5b0dd895-bfab-47de-ae08-1ff4221de647)

  - #### Concept of pre-placement

    the idea is to create reusable moduls called IP's. If you have a complex logic you beak it down into reusable parts called module what are seene as black boxes this input an out lines an specific functions.

![11-05-2025_17-36-43](https://github.com/user-attachments/assets/8ba71c2a-fb8f-4edb-b801-06eadb274718)

![11-05-2025_17-38-05](https://github.com/user-attachments/assets/31c22acc-38e0-4ee9-bbe5-8d568df8c579)

![11-05-2025_17-38-50](https://github.com/user-attachments/assets/81b269c9-8a86-432d-ac1d-f0e7147f4a43)

For functions like Mux, Comparator, ALU's, Adder,.... IP's are available and can be used in floorplaning.

![11-05-2025_17-39-44](https://github.com/user-attachments/assets/08823182-8e2d-46c7-b3b6-bb3467024903)


  - #### De-coupling capacitors

    concept of macros which contain reusable cells (IP's) which can be used multiple times and on different hardware.
    Location where cells (A, B, C) in our example depend on desig szenario.

![11-05-2025_17-48-47](https://github.com/user-attachments/assets/897d3d6d-b3c7-4c36-ade2-7c9d21a314d4)

Idea of pre-placed cells are that they are fixed and can't be moved.

![11-05-2025_17-49-27](https://github.com/user-attachments/assets/8767ab10-435c-43cb-b51f-fdcf8cf8c98a)

Concept of de-copupling capacitors: 
Due to phisical resistance of wires on a chip the is a voltage drop, when switching a circuit from 0 to 1, a current flow from power supply to cell.
If the voltage drop is still in noise margin range weare save, otherwise voltage falls into "undifened area" which produce unpredictable result.

![11-05-2025_17-50-40](https://github.com/user-attachments/assets/eb1ac662-24e4-4881-b3ea-dd04a536ff21)

![11-05-2025_17-56-34](https://github.com/user-attachments/assets/9e50e7ca-30f6-4438-a97e-fec1de5bd664)

![11-05-2025_17-51-47](https://github.com/user-attachments/assets/2a71f711-0865-4954-9144-279852610aaa)

![11-05-2025_17-52-39](https://github.com/user-attachments/assets/406e86f0-20b6-4adb-bf94-3a89fee342d4)

To solve this problem we use de-coupling capacitors.
The circuit get its power from de-coupling capacitor in case of switching from 0 to 1, and is so de-coupled from power supply. De-Coupled capacitors are pled very clos to the ciurcit to minimze voltage drops due to wire resistance.


![11-05-2025_17-53-10](https://github.com/user-attachments/assets/4267535f-3f55-4b05-ab1e-8e5d18d9e3f7)

If we look to the physical chip we place in our example de de-coupling capacitors betwee the pre.defined cells.

![11-05-2025_17-53-10](https://github.com/user-attachments/assets/cdc9c09f-1b2f-4775-b1c2-924627d1b629)









  - #### Pin placement and logical cell placement blockage
  - ##### Steps to run floor using OpenLANE
  - ##### Review floorplan files and steps to view floorplan
  - ##### Review floorplan layout in Magic
  
- ### Library Binding and Placement
  - #### Netlist binding and initial place design
  - #### Optimize placement using estimated wite-length and capacitance
  - #### Final plancement optimization
  - #### Need for libraries and characterizatiion
  - #### Congestion aware placement using RePlace
  
- ### Cell design and characterization flows
  - #### Inputs for cell design flow
  - #### Circuit design steps
  - #### Layout design steps
  - #### Typical characterization flow
  
- ### General timing characterization parameter
  - #### Timing threshold definition
  - #### Propagation delay and transition time
  

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

