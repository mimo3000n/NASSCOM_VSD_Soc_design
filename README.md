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

To solve this problem we use de-coupling capacitors.
The circuit get its power from de-coupling capacitor in case of switching from 0 to 1, and is so de-coupled from power supply. De-Coupled capacitors are pled very clos to the ciurcit to minimze voltage drops due to wire resistance.

![11-05-2025_17-52-39](https://github.com/user-attachments/assets/406e86f0-20b6-4adb-bf94-3a89fee342d4)

If we look to the physical chip we place in our example de de-coupling capacitors betwee the pre.defined cells.

![11-05-2025_17-53-10](https://github.com/user-attachments/assets/cdc9c09f-1b2f-4775-b1c2-924627d1b629)


  - #### Power planing

    See circuit in prev exercise as an black box, a macro.

![12-05-2025_12-52-09](https://github.com/user-attachments/assets/abe1cc85-aeec-4f3f-8d51-46ea4d5fe941)

    repeat it multible time on a chip.
    Now the goal is if one circut output drives other cicuirs's input in below slide, the shape of the signal sould be the same, that we have to make sure.

![12-05-2025_12-52-50](https://github.com/user-attachments/assets/ced557c9-d11b-42b0-a2a3-6afc2374a9bb)

Where is the problem?
The assumtion is that the orange line is a 16bit bus goning from 0 to 1. we dont have a de-coupling capacitor, so the power supple have to supply power for this complete line.
Its also not possible to place each and everyware a de-coupling capacitor. So the power supply have to supply needed power that there is no voltage drop.

![12-05-2025_12-53-33](https://github.com/user-attachments/assets/69efb053-48a8-4b9b-91fb-dd67cd81483e)

If we visualize the 16bit bus all 1's charge capacitor and all 0's dis-charge capacitor.
If we connect to an inverter all 1's will be dischared and oll 0's will be chard to 1.

![12-05-2025_12-54-11](https://github.com/user-attachments/assets/c054159d-5aab-4bdc-8f4f-9e36b03fa232)

There is only a singe gound line an if all 1's are descarged to 0 there will be a bump in the ground line, call "Ground Bounce". If the size of the grond bounce exit the noise margin level we we enter into undifined state which mean we can have a logic 1 or logic 0.

![12-05-2025_12-55-46](https://github.com/user-attachments/assets/1a141daf-06a0-4fe8-9219-ddf3bd84bfe8)

Same happen if 0's are going to 1's. Due that we have a single power line we will have a voltage droop until capacitor's are charged, if this exit noise margin level we have a risk for an undifined state of the cell.

![12-05-2025_12-56-17](https://github.com/user-attachments/assets/10337385-0929-47b0-aed1-3d4c3877e7ba)

To solve this porblem we use instead of only one power supply multiple power supply's. If a sircut need's power it will get the power from the neares power supply. That's the reason that you multiple Vss & Vdd on chip, this is call a mesh.

![12-05-2025_12-57-13](https://github.com/user-attachments/assets/124a5e9d-fb72-4b13-920f-44c4af73ab41)

If we look to a physical chip we see a power mesh to eliminate the problem with voltatge droop and groud bounce.

![12-05-2025_12-57-48](https://github.com/user-attachments/assets/58900ee4-e4a9-4569-96b5-bf5e762dcda1)

  - #### Pin placement and logical cell placement blockage

    In example implementation the have section 1 & 2, which constists og flip-flops, logic gates and 2 pre-places cells block a and block b.

![12-05-2025_14-37-58](https://github.com/user-attachments/assets/a31fe3b0-ff64-4d0b-8b36-fdc5e098e0c5)

    addition we have section 3 & 4 an pre-placed cell, block c in our design.

![12-05-2025_14-39-35](https://github.com/user-attachments/assets/11ff052f-ba2a-49da-ad05-1f5985d7160c)

    now we have the complete disign with section 1, 2, 3, 4, and pre-placed cell's block a,b,c.
    The connectivity of the gates is described in a "netnist",the coding is done in Verilog or VHDL.

![12-05-2025_14-46-00](https://github.com/user-attachments/assets/434747d0-04ca-43de-b858-a2061bec8cb9)

next is we place input and out port on the chip. The area between core and dia will be filled with pins for input and output. In our example we place input ports in left-hand side and input-port on rigth-hand side, but this depends on design. The ordering of the ports are random it depend's where we place the cell on chip. In our example Clk1 & Clk2 are very important chause they drive the complete chip. We need therefor a least resistance we mean we have to increase the size of the pin.
The area between core and dia are reserved for pin placement and are not used by the routing-tool

![12-05-2025_14-43-13](https://github.com/user-attachments/assets/bfb94b4b-10ce-49ec-a8ad-4ea01176d923)

Now we are ready for placement & routing!!

  - ##### Steps to run floor using OpenLANE

    go into /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/configuration and have a look to Readme.md

    this switches you can stet during synthesis/floorplaning,..

    Floorplaning switches start with FP_ in the Floorplaning section of README.md

``` md
# Variables information

This page describes configuration variables and their default values.

## Required variables

| Variable      | Description                                           |
|---------------|-------------------------------------------------------|
| `DESIGN_NAME`   | The name of the top level module of the design        |
| `VERILOG_FILES` | The path of the design's verilog files |
| `CLOCK_PERIOD`  | The clock period for the design in ns       |
| `CLOCK_NET` | The name of the Net input to root clock buffer used in Clock Tree Synthesis. |
| `CLOCK_PORT`    | The name of the design's clock port used in Static Timing Analysis.   |

## Optional variables

These variables are optional that can be specified in the design configuration file.

### Synthesis

| Variable      | Description                                                   |
|---------------|---------------------------------------------------------------|
| `LIB_SYNTH` | The library used for synthesis by yosys. <br> (Default: `$::env(PDK_ROOT)/$::env(PDK)/libs.ref/$::env(STD_CELL_LIBRARY)/lib/sky130_fd_sc_hd__tt_025C_1v80.lib`)|
| `SYNTH_BIN` | The yosys binary used in the flow. <br> (Default: `yosys`) |
| `SYNTH_DRIVING_CELL`  | The cell to drive the input ports. <br>(Default: `sky130_fd_sc_hd__inv_8`)|
| `SYNTH_DRIVING_CELL_PIN`  | The name of the SYNTH_DRIVING_CELL output pin. <br>(Default: `Y`)|
| `SYNTH_CAP_LOAD` | The capacitive load on the output ports in femtofarads. <br> (Default: `17.65` ff)|
| `SYNTH_MAX_FANOUT`  | The max load that the output ports can drive. <br> (Default: `5` cells) |
| `SYNTH_MAX_TRAN` | The max transition time (slew) from high to low or low to high on cell inputs in ns. Used in synthesis <br> (Default: Calculated at runtime as `10%` of the provided clock period, unless this exceeds a set DEFAULT_MAX_TRAN, in which case it will be used as is). |
| `SYNTH_STRATEGY` | Strategies for abc logic synthesis and technology mapping <br> Possible values are `DELAY/AREA 0-3/0-2`; the first part refers to the optimization target of the synthesis strategy (area vs. delay) and the second one is an index. <br> (Default: `AREA 0`)|
| `SYNTH_BUFFERING` | Enables abc cell buffering <br> Enabled = 1, Disabled = 0 <br> (Default: `1`)|
| `SYNTH_SIZING` | Enables abc cell sizing (instead of buffering) <br> Enabled = 1, Disabled = 0 <br> (Default: `0`)|
| `SYNTH_READ_BLACKBOX_LIB` | A flag that enable reading the full(untrimmed) liberty file as a blackbox for synthesis. Please note that this is not used in technology mapping. This should only be used when trying to preserve gate instances in the rtl of the design.  <br> Enabled = 1, Disabled = 0 <br> (Default: `0`)|
| `SYNTH_NO_FLAT` | A flag that disables flattening the hierarchy during synthesis, only flattening it after synthesis, mapping and optimizations. <br> Enabled = 1, Disabled = 0 <br> (Default: `0`)|
| `SYNTH_SHARE_RESOURCES` | A flag that enables yosys to reduce the number of cells by determining shareable resources and merging them. <br> Enabled = 1, Disabled = 0 <br> (Default: `1`)|
| `SYNTH_ADDER_TYPE` | Adder type to which the $add and $sub operators are mapped to. <br> Possible values are `YOSYS/FA/RCA/CSA`; where `YOSYS` refers to using Yosys internal adder definition, `FA` refers to full-adder structure, `RCA` refers to ripple carry adder structure, and `CSA` refers to carry select adder. <br> (Default: `YOSYS`)|
| `LIB_SLOWEST` | Points to the lib file, corresponding to the slowest corner, for max delay calculation during STA. <br> (Default: `$::env(PDK_ROOT)/$::env(PDK)/libs.ref/$::env(STD_CELL_LIBRARY)/lib/sky130_fd_sc_hd__ff_n40C_1v95.lib`) |
| `LIB_FASTEST` | Points to the lib file, corresponding to the fastest corner, for min delay calculation during STA. <br> (Default: `$::env(PDK_ROOT)/$::env(PDK)/libs.ref/$::env(STD_CELL_LIBRARY)/lib/sky130_fd_sc_hd__ss_100C_1v60.lib`) |
| `LIB_TYPICAL` | Library used for typical delay calculation during STA. <br> (Default`LIB_SYNTH`) |
| `CLOCK_BUFFER_FANOUT` | Fanout of clock tree buffers. <br> (Default: `16`) |
| `ROOT_CLK_BUFFER` | Root clock buffer of the clock tree. <br> (Default: `sky130_fd_sc_hd__clkbuf_16`) |
| `CLK_BUFFER` | Clock buffer used for inner nodes of the clock tree. <br> (Default: `sky130_fd_sc_hd__clkbuf_4`) |
| `CLK_BUFFER_INPUT` | Input pin of the clock tree buffer. <br> (Default: `A`) |
| `CLK_BUFFER_OUTPUT` | Output pin of the clock tree buffer. <br> (Default: `X`) |
| `BASE_SDC_FILE` | Specifies the base sdc file to source before running Static Timing Analysis. <br> (Default: `$::env(OPENLANE_ROOT)/scripts/base.sdc`) |
| `VERILOG_INCLUDE_DIRS` | Specifies the verilog includes directories. <br> Optional. |
| `SYNTH_FLAT_TOP` | Specifies whether or not the top level should be flattened during elaboration. 1 = True, 0= False <br> Default: `0`. |
| `IO_PCT` | Specifies the percentage of the clock period used in the input/output delays. Ranges from 0 to 1.0. <br> (Default: `0.2`) |

### Floorplanning

| Variable      | Description                                                   |
|---------------|---------------------------------------------------------------|
| `FP_CORE_UTIL`  | The core utilization percentage. <br> (Default: `50` percent)|
| `FP_ASPECT_RATIO`  | The core's aspect ratio (height / width). <br> (Default: `1`)|
| `FP_SIZING`  | Whether to use relative sizing by making use of `FP_CORE_UTIL` or absolute one using `DIE_AREA`. <br> (Default: `"relative"` - accepts "absolute" as well)|
| `DIE_AREA`  | Specific die area to be used in floorplanning. Specified as a 4-corner rectangle. Units in mm <br> (Default: unset)|
| `FP_IO_HMETAL`  | The metal layer on which to place the io pins horizontally (top and bottom of the die). <br>(Default: `4`)|
| `FP_IO_VMETAL`  | The metal layer on which to place the io pins vertically (sides of the die) <br> (Default: `3`)|
| `FP_IO_MODE`  | Decides the mode of the random IO placement option. 0=matching mode, 1=random equidistant mode <br> (Default: `1`)|
| `FP_WELLTAP_CELL`  | The name of the welltap cell during welltap insertion. |
| `FP_ENDCAP_CELL`  | The name of the endcap cell during endcap insertion. |
| `FP_PDN_VOFFSET`  | The offset of the vertical power stripes on the metal layer 4 in the power distribution network <br> (Default: `16.32`) |
| `FP_PDN_VPITCH`  | The pitch of the vertical power stripes on the metal layer 4 in the power distribution network <br> (Default: `153.6`) |
| `FP_PDN_HOFFSET`  | The offset of the horizontal power stripes on the metal layer 5 in the power distribution network <br> (Default: `16.65`) |
| `FP_PDN_HPITCH`  | The pitch of the horizontal power stripes on the metal layer 5 in the power distribution network <br> (Default: `153.18`) |
| `FP_PDN_AUTO_ADJUST` | Decides whether or not the flow should attempt to re-adjust the power grid, in order for it to fit inside the core area of the design, if needed. <br> 1=enabled, 0 =disabled (Default: `1`) |
| `FP_TAPCELL_DIST`  | The horizontal distance between two tapcell columns <br> (Default: `14`) |
| `FP_IO_VEXTEND`  |  Extends the vertical io pins outside of the die by the specified units<br> (Default: `-1` Disabled) |
| `FP_IO_HEXTEND`  |  Extends the horizontal io pins outside of the die by the specified units<br> (Default: `-1` Disabled) |
| `FP_IO_VLENGTH`  | The length of the vertical IOs in microns. <br> (Default: `4`) |
| `FP_IO_HLENGTH`  | The length of the horizontal IOs in microns. <br> (Default: `4`) |
| `FP_IO_VTHICKNESS_MULT`  | A multiplier for vertical pin thickness. Base thickness is the pins layer minwidth <br> (Default: `2`) |
| `FP_IO_HTHICKNESS_MULT`  | A multiplier for horizontal pin thickness. Base thickness is the pins layer minwidth <br> (Default: `2`) |
| `BOTTOM_MARGIN_MULT`     | The core margin, in multiples of site heights, from the bottom boundary. <br> (Default: `4`) |
| `TOP_MARGIN_MULT`        | The core margin, in multiples of site heights, from the top boundary. <br> (Default: `4`) |
| `LEFT_MARGIN_MULT`       | The core margin, in multiples of site widths, from the left boundary.  <br> (Default: `12`) |
| `RIGHT_MARGIN_MULT`      | The core margin, in multiples of site widths, from the right boundary.   <br> (Default: `12`) |
| `FP_PDN_CORE_RING` | Enables adding a core ring around the design. More details on the control variables in the pdk configurations documentation. 0=Disable 1=Enable. <br> (Default: `0`) |
| `FP_PDN_ENABLE_RAILS` | Enables the creation of rails in the power grid. 0=Disable 1=Enable. <br> (Default: `1`) |
| `FP_PDN_CHECK_NODES` | Enables checking for unconnected nodes in the power grid. 0=Disable 1=Enable. <br> (Default: `1`) |
| `FP_HORIZONTAL_HALO` | Sets the horizontal halo around the tap and decap cells. The value provided is in microns. <br> Default: `10` |
| `FP_VERTICAL_HALO` | Sets the vertical halo around the tap and decap cells. The value provided is in microns. <br> Default: set to the value of `FP_HORIZONTAL_HALO` |
| `DESIGN_IS_CORE` | Controls the layers used in the power grid. Depending on whether the design is the core of the chip or a macro inside the core. 1=Is a Core, 0=Is a Macro <br> (Default: `1`)|
| `FP_PIN_ORDER_CFG` | Points to the pin order configuration file to set the pins in specific directions (S, W, E, N). Check this [file][0] as an example. If not set, then the IO pins will be placed based on one of the other methods depending on the rest of the configurations. <br> (Default: NONE)|
| `FP_CONTEXT_DEF` | Points to the parent DEF file that includes this macro/design and uses this DEF file to determine the best locations for the pins. It must be used with `FP_CONTEXT_LEF`, otherwise it's considered non-existing. If not set, then the IO pins will be placed based on one of the other methods depending on the rest of the configurations. <br> (Default: NONE)|
| `FP_CONTEXT_LEF` | Points to the parent LEF file that includes this macro/design and uses this LEF file to determine the best locations for the pins. It must be used with `FP_CONTEXT_DEF`, otherwise it's considered non-existing. If not set, then the IO pins will be placed based on one of the other methods depending on the rest of the configurations. <br> (Default: NONE)|
| `FP_DEF_TEMPLATE` | Points to the DEF file to be used as a template when running `apply_def_template`. This will be used to exctract pin names, locations, shapes -excluding power and ground pins- as well as the die area and replicate all this information in the `CURRENT_DEF`. |
| `VDD_NETS` | Specifies the power nets/pins to be used when creating the power grid for the design. |
| `GND_NETS` | Specifies the ground nets/pins to be used when creating the power grid for the design. |
| `SYNTH_USE_PG_PINS_DEFINES` | Specifies the power guard used in the verilog source code to specify the power and ground pins. This is used to automatically extract `VDD_NETS` and `GND_NET` variables from the verilog, with the assumption that they will be order `inout vdd1, inout gnd1, inout vdd2, inout gnd2, ...`. |

### Placement

| Variable      | Description                                                   |
|---------------|---------------------------------------------------------------|
| `PL_TARGET_DENSITY` | The desired placement density of cells. It reflects how spread the cells would be on the core area. 1 = closely dense. 0 = widely spread <br> (Default: `0.55`)|
| `PL_TIME_DRIVEN` | Specifies whether the placer should use time driven placement. 0 = false, 1 = true <br> (Default: `0`)|
| `PL_LIB` | Specifies the library for time driven placement <br> (Default: `LIB_TYPICAL`)|
| `PL_BASIC_PLACEMENT` | Specifies whether the placer should run basic placement or not (by running initial placement, increasing the minimum overflow to 0.9, and limiting the number of iterations to 20). 0 = false, 1 = true <br> (Default: `0`) |
| `PL_SKIP_INITIAL_PLACEMENT` | Specifies whether the placer should run initial placement or not. 0 = false, 1 = true <br> (Default: `0`) |
| `PL_RANDOM_GLB_PLACEMENT` | Specifies whether the placer should run random placement or not. This is useful if the design is tiny (less than 100 cells). 0 = false, 1 = true <br> (Default: `0`) |
| `PL_RANDOM_INITIAL_PLACEMENT` | Specifies whether the placer should run random placement or not followed by replace's initial placement. This is useful if the design is tiny (less than 100 cells). 0 = false, 1 = true <br> (Default: `0`) |
| `PL_ROUTABILITY_DRIVEN` | Specifies whether the placer should use routability driven placement. 0 = false, 1 = true <br> (Default: `0`) |
| `PL_OPENPHYSYN_OPTIMIZATIONS` | Specifies whether OpenPhySyn should be used to perform timing optimizations or not. 0 = false, 1 = true <br> (Default: `0`) |
| `PSN_ENABLE_RESIZING` | Enables driver resizing by OpenPhySyn. 0 = Disabled, 1 = Enabled <br> (Default: `1`)|
| `PSN_ENABLE_PIN_SWAP` | Enables pin swapping for timing optimization by OpenPhySyn. 0 = Disabled, 1 = Enabled <br> (Default: `1`)|
| `PL_RESIZER_DESIGN_OPTIMIZATIONS` | Specifies whether resizer design optimizations should be performed or not. 0 = false, 1 = true <br> (Default: `1`) |
| `PL_RESIZER_TIMING_OPTIMIZATIONS` | Specifies whether resizer timing optimizations should be performed or not. 0 = false, 1 = true <br> (Default: `1`) |
| `PL_RESIZER_MAX_WIRE_LENGTH` | Specifies the maximum wire length cap used by resizer to insert buffers. If set to 0, no buffers will be inserted. Value in microns. <br> (Default: `0`)|
| `LIB_OPT` | Points to the lib file, corresponding to the slowest corner, for max delay calculation during OpenPhySyn optimizations. This is usually a trimmed version of `LIB_SLOWEST`. <br> Default: `$::env(TMP_DIR)/opt.lib` |
| `LIB_RESIZER_OPT` | Points to the lib file, corresponding to the slowest corner, for max delay calculation during resizer optimizations. This is copy of `LIB_SLOWEST`. <br> Default: `$::env(TMP_DIR)/resizer.lib` |
| `DONT_USE_CELLS` | The list of cells to not use during resizer optimizations. <br> Default: the contents of `DRC_EXCLUDE_CELL_LIST`. |
| `PL_ESTIMATE_PARASITICS` | Specifies whether or not to run STA after global placement using OpenROAD's estimate_parasitics -placement and generates reports under `logs/placement`. 1 = Enabled, 0 = Disabled. <br> (Default: `1`) |
| `PL_DIAMOND_SEARCH_HEIGHT` | Specifies the diamond search height used for legalizing the cells during detailed placement. The search width is calculated internally as `heigh*5`. For designs that contain big macros, increasing this value to above 400 will allow for more search space and more potentail for successful legalization. <br> (Default: `100`) |
| `PL_OPTIMIZE_MIRRORING` | Specifies whether or not to run an optimize_mirroring pass whenever detailed placement happens. This pass will mirror the cells whenever possible to optimize the design. 1 = Enabled, 0 = Disabled. <br> (Default: `1`) |
| `PL_RESIZER_BUFFER_INPUT_PORTS` | Specifies whether or not to insert buffers on input ports whenever resizer optimizations are run. For this to be used, `PL_RESIZER_DESIGN_OPTIMIZATIONS` must be set to 1. 1 = Enabled, 0 = Disabled. <br> (Default: `1`) |
| `PL_RESIZER_BUFFER_OUTPUT_PORTS` | Specifies whether or not to insert buffers on output ports whenever resizer optimizations are run. For this to be used, `PL_RESIZER_DESIGN_OPTIMIZATIONS` must be set to 1. 1 = Enabled, 0 = Disabled. <br> (Default: `1`) |

### CTS

| Variable      | Description                                                   |
|---------------|---------------------------------------------------------------|
| `CTS_TARGET_SKEW` | The target clock skew in picoseconds. <br> (Default: `200` ps)|
| `CTS_ROOT_BUFFER`| The name of cell inserted at the root of the clock tree. |
| `CLOCK_TREE_SYNTH` | Enable clock tree synthesis for tirtonCTS. <br> (Default: `1`)|
| `CTS_TOLERANCE` | An integer value that represents a tradeoff of QoR and runtime. Higher values will produce smaller runtime but worse QoR <br> (Default: `100`) |
| `CTS_SINK_CLUSTERING_SIZE` | Specifies the maximum number of sinks per cluster. <br> (Default: `20`) |
| `CTS_SINK_CLUSTERING_MAX_DIAMETER` | Specifies maximum diameter (in micron) of sink cluster. <br> (Default: `50`) |
| `CTS_REPORT_TIMING` | Specifies whether or not to run STA after clock tree synthesis using OpenROAD's estimate_parasitics -placement and generates reports under `logs/cts`. 1 = Enabled, 0 = Disabled. <br> (Default: `1`) |
| `LIB_CTS` | The liberty file used for CTS. By default, this is the `LIB_SYNTH_COMPLETE` minus the cells with drc errors as specified by the drc exclude list. <br> (Default: `$::env(TMP_DIR)/cts.lib`) |

### Routing

| Variable      | Description                                                   |
|---------------|---------------------------------------------------------------|
| `GLB_RT_MINLAYER` | The number of lowest layer to be used in routing. <br> (Default: `1`)|
| `GLB_RT_MAXLAYER` | The number of highest layer to be used in routing. <br> (Default: `6`)|
| `GLB_RT_ADJUSTMENT` | Reduction in the routing capacity of the edges between the cells in the global routing graph. Values range from 0 to 1. <br> 1 = most reduction, 0 = least reduction  <br> (Default: `0`)|
| `GLB_RT_L1_ADJUSTMENT` | Reduction in the routing capacity of the edges between the cells in the global routing graph but specific to li1 layer in sky130A. Values range from 0 to 1 <br> (Default: `0.99`) |
| `GLB_RT_L2_ADJUSTMENT` | Reduction in the routing capacity of the edges between the cells in the global routing graph but specific to met1 in sky130A. Values range from 0 to 1 <br> (Default: `0`) |
| `GLB_RT_L3_ADJUSTMENT` | Reduction in the routing capacity of the edges between the cells in the global routing graph but specific to met2 in sky130A. Values range from 0 to 1 <br> (Default: `0`) |
| `GLB_RT_L4_ADJUSTMENT` | Reduction in the routing capacity of the edges between the cells in the global routing graph but specific to met3 in sky130A. Values range from 0 to 1 <br> (Default: `0`) |
| `GLB_RT_L5_ADJUSTMENT` | Reduction in the routing capacity of the edges between the cells in the global routing graph but specific to met4 in sky130A. Values range from 0 to 1 <br> (Default: `0`) |
| `GLB_RT_L6_ADJUSTMENT` | Reduction in the routing capacity of the edges between the cells in the global routing graph but specific to met5 in sky130A. Values range from 0 to 1 <br> (Default: `0`) |
| `GLB_RT_UNIDIRECTIONAL` | Allow unidirectional routing. 0 = false, 1 = true <br> (Default: `1`) |
| `GLB_RT_ALLOW_CONGESTION` | Allow congestion in the resultign guides. 0 = false, 1 = true <br> (Default: `0`) |
| `GLB_RT_OVERFLOW_ITERS` | The maximum number of iterations waiting for the overflow to reach the desired value. <br> (Default: `50`) |
| `GLB_RT_TILES` | The size of the GCELL used by Fastroute during global routing. <br> (Default: `15`) |
| `GLB_RT_ESTIMATE_PARASITICS` | Specifies whether or not to run STA after global routing using OpenROAD's estimate_parasitics -global_routing and generates reports under `logs/routing`. 1 = Enabled, 0 = Disabled. <br> (Default: `1`) |
| `ROUTING_CORES` | Specifies the number of threads to be used in TritonRoute. <br> (Default: `4`) |
| `GLB_RT_MAX_DIODE_INS_ITERS` | Controls the maximum number of iterations at which re-running Fastroute for diode insertion stops. Each iteration ARC detects the violations and FastRoute fixes them by inserting diodes, then producing the new DEF. The number of antenna violations is compared with the previous iteration and if they are equal or the number is greater the iterations stop and the DEF from the previous iteration is used in the rest of the flow. If the current antenna violations reach zero, the current def will be used and the iterations will not continue. This option is only available in DIODE_INSERTION_STRATEGY = `3`.  <br> (Default: `1`) |
| `GLB_RT_OBS` | Specifies custom obstruction to be added prior to global routing. Comma separated list of layer and coordinates: `layer llx lly urx ury`.<br> (Example: `li1 0 100 1000 300, met5 0 0 1000 500`)  <br> (Default: unset) |
| `ROUTING_OPT_ITERS` | Specifies the maximum number of optimization iterations during Detailed Routing in TritonRoute. <br> (Default: `64`) |
| `GLOBAL_ROUTER` | Specifies which global router to use. Values: `fastroute` or `cugr`. <br> (Default: `fastroute`) |
| `DETAILED_ROUTER` | Specifies which detailed router to use. Values: `tritonroute`, `tritonroute_or`, or `drcu`. <br> (Default: `tritonroute`) |

### Magic

| Variable      | Description                                                   |
|---------------|---------------------------------------------------------------|
| `MAGIC_PAD` |  A flag to pad the views generated by magic (.mag, .lef, .gds) with one site. 1 = Enabled, 0 = Disabled <br> (Default: `0` )|
| `MAGIC_ZEROIZE_ORIGIN` | A flag to move the layout such that it's origin in the lef generated by magic is 0,0. 1 = Enabled, 0 = Disabled  <br> (Default: `1` )|
| `MAGIC_GENERATE_GDS` | A flag to generate gds view via magic . 1 = Enabled, 0 = Disabled  <br> (Default: `1` )|
| `MAGIC_GENERATE_LEF` | A flag to generate lef view via magic . 1 = Enabled, 0 = Disabled  <br> (Default: `1` )|
| `MAGIC_GENERATE_MAGLEF` | A flag to generate maglef view via magic . 1 = Enabled, 0 = Disabled  <br> (Default: `1` )|
| `MAGIC_WRITE_FULL_LEF` | A flag to specify whether or not the output LEF should include all shapes inside the macro or an abstracted view of the macro lef view via magic . 1 = Full View, 0 = Abstracted View  <br> (Default: `0` )|
| `MAGIC_DRC_USE_GDS` | A flag to choose whether to run the magic DRC checks on GDS or not. If not, then the checks will be done on the DEF/LEF. 1 = GDS, 0 = DEF/LEF  <br> (Default: `1` )|
| `MAGIC_EXT_USE_GDS` | A flag to choose whether to run the magic extractions on GDS or DEF/LEF. If GDS was used Device Level LVS will be run. Otherwise, blackbox LVS will be run. 1 = GDS, 0 = DEF/LEF  <br> (Default: `0` )|
| `MAGIC_INCLUDE_GDS_POINTERS` | A flag to choose whether to include GDS pointers in the generated mag files or not. 1 = Enabled, 0 = Disabled  <br> (Default: `0` )|
| `MAGIC_DISABLE_HIER_GDS` | A flag to disable cif hier and array during GDS-II writing.* 1=Enabled `<so this hier gds will be disabled>`, 0=Disabled `<so this hier gds will be enabled>`. <br> (Default: `1` )|

> * Tim Edwards's Explanation on disabling hier gds: The following is an explanation by Tim Edwards, provided in a slack thread, on how this affects the GDS writing process: "Magic can take a very long time writing out GDS while checking hierarchical interactions in a standard cell layout. If your design is all digital, I recommend using "gds *hier write disable" before "gds write" so that it does not try to resolve hierarchical interactions (since by definition, standard cells are designed to just sit next to each other without creating DRC issues).  That can actually make the difference between a 20 hour GDS write and a 2 minute GDS write.  For a standard cell design that takes up the majority of the user space, a > 24 hour write time (without disabling the hierarchy checks) would not surprise me."

### LVS

| Variable      | Description                                                   |
|---------------|---------------------------------------------------------------|
| `LVS_INSERT_POWER_PINS` |  Enables power pins insertion before running lvs. 1 = Enabled, 0 = Disabled <br> (Default: `1` )|
| `LVS_CONNECT_BY_LABEL` | Enables connections by label in LVS by skipping `extract unique` in magic extractions. <br> Default: `0` |
| `YOSYS_REWRITE_VERILOG` | Enables yosys to rewrite the verilog before LVS producing a canonical verilog netlist with verbose wire declarations. This flag will be ignored if `LEC_ENABLE` is 1, and it will be rewritten anyways. 1 = Enabled, 0 = Disabled <br> (Default: `0` ) |

### Misc

| Variable      | Description                                                   |
|---------------|---------------------------------------------------------------|
| `PDK` | Specifies the process design kit (PDK). <br> (Default: `sky130A` )|
| `STD_CELL_LIBRARY` | Specifies the standard cell library to be used under the specified PDK. <br> (Default: `sky130_fd_sc_hd` )|
| `PDK_ROOT` | Specifies the folder path of the PDK. It searches for a `config.tcl` in `$PDK_ROOT/$PDK/libs.tech/openlane/` directory and at least have one standard cell library config defined in `$PDK_ROOT/$PDK/libs.tech/openlane/$STD_CELL_LIBRARY`. |
| `CELL_PAD` | Cell padding; increases the width of cells. <br> (Default: `4` microns -- 4 sites)|
| `DIODE_PADDING` | Diode cell padding; increases the width of diode cells during placement checks. <br> (Default: `2` microns -- 2 sites)|
| `WIRE_RC_LAYER` | The metal layer used in estimate parastics `set_wire_rc`. Should be moved to PDK configurations later.. <br> Default: `met1`.|
| `MERGED_LEF_UNPADDED` | Points to `merged_unpadded.lef` by default. it contains the technology LEF for the used STD_CELL_LIBRARY merged with the LEF file for all the cells. |
| `MERGED_LEF` | points to `merged.lef`, which is `merged_unpadded.lef` but with cell padding. This is controlled by CELL_PAD. |
| `NO_SYNTH_CELL_LIST` | Specifies the file that contains the don't-use-cell-list to be excluded from the liberty file during synthesis. If it's not defined, this path is searched `$::env(PDK_ROOT)/$::env(PDK)/libs.tech/openlane/$::env(STD_CELL_LIBRARY)/no_synth.cells` and if it's not found, then the original liberty will be used as is. |
| `DRC_EXCLUDE_CELL_LIST` | Specifies the file that contains the don't-use-cell-list to be excluded from the liberty file during synthesis and timing optimizations. If it's not defined, this path is searched `$::env(PDK_ROOT)/$::env(PDK)/libs.tech/openlane/$::env(STD_CELL_LIBRARY)/drc_exclude.cells` and if it's not found, then the original liberty will be used as is. In other words, `DRC_EXCLUDE_CELL_LIST` contain the only excluded cell list in timing optimizations. |

### Flow control

| Variable      | Description                                                   |
|---------------|---------------------------------------------------------------|
| `USE_GPIO_PADS` | Decides whether or not to use the gpio pads in routing by merging their LEF file set in `::env(USE_GPIO_ROUTING_LEF)` and blackboxing their verilog modules set in `::env(GPIO_PADS_VERILOG)`. 1=Enabled, 0=Disabled. <br> (Default: `0`) |
| `LEC_ENABLE` | Enables logic verification using yosys, for comparing each netlist at each stage of the flow with the previous netlist and verifying that they are logically equivalent. Warning: this will increase the runtime significantly. 1 = Enabled, 0 = Disabled <br> (Default: `0`)|
| `RUN_ROUTING_DETAILED` | Enables detailed routing. 1 = Enabled, 0 = Disabled <br> (Default: `1`)|
| `RUN_MAGIC` | Enables running magic and GDSII streaming. 1 = Enabled, 0 = Disabled <br> (Default: `1`)|
| `RUN_KLAYOUT` | Enables running Klayout and GDSII streaming. 1 = Enabled, 0 = Disabled <br> (Default: `1`)|
| `RUN_KLAYOUT_DRC` | Enables running Klayout DRC on GDS-II produced by magic. 1 = Enabled, 0 = Disabled <br> (Default: `1`)|
| `KLAYOUT_DRC_KLAYOUT_GDS` | Enables running Klayout DRC on GDS-II produced by Klayout. 1 = Enabled, 0 = Disabled <br> (Default: `0`)|
| `RUN_KLAYOUT_XOR` | Enables running Klayout XOR on 2 GDS-IIs, the defaults are the one produced by magic vs the one produced by klayout. 1 = Enabled, 0 = Disabled <br> (Default: `1`)|
| `KLAYOUT_XOR_GDS` | If `RUN_KLAYOUT_XOR` is enabled, this will enable producing a GDS output from the XOR along with it's PNG export. 1 = Enabled, 0 = Disabled <br> (Default: `1`)|
| `KLAYOUT_XOR_XML` | If `RUN_KLAYOUT_XOR` is enabled, this will enable producing an XML output from the XOR. 1 = Enabled, 0 = Disabled <br> (Default: `1`)|
| `TAKE_LAYOUT_SCROT` | Enables running Klayout to take a PNG screenshot of the produced layout (currently configured to run on the results of each stage).1 = Enabled, 0 = Disabled <br> (Default: `1`)|
| `RUN_SIMPLE_CTS` | Enables inserting simple clock tree after synthesis .1 = Enabled, 0 = Disabled <br> (Default: `0`)|
| `FILL_INSERTION` | Enables fill cells insertion after cts (if enabled) .1 = Enabled, 0 = Disabled <br> (Default: `1`)|
| `TAP_DECAP_INSERTION` | Enables tap and decap cells insertion after floorplanning (if enabled) .1 = Enabled, 0 = Disabled <br> (Default: `1`) |
| `DIODE_INSERTION_STRATEGY` | Specifies the insertion strategy of diodes to be used in the flow. 0 = No diode insertion, 1 = Spray diodes, 2 = insert fake diodes and replace them with real diodes if needed. 3= use FastRoute Antenna Avoidance flow, 4 = Use Sylvian's Custom Script for diode insertion on design pins and smartly inserting needed diodes inside the design, 5 = a mix of strategy 2 and 4. <br> (Default: `3`) |
| `WIDEN_SITE` | Specifies the new virtual width of the site to be used in all stages up to diode insertion, then switched back to the original site width. It can be either a factor or an absolute value controlled by `WIDEN_SITE_IS_FACTOR` <br> (Default: `1`) |
| `WIDEN_SITE_IS_FACTOR` | Specifies whether the given `WIDEN_SITE` should be treated as a factor or an absolute value. 0 = absolute, 1 = factor <br> (Default: `1`) |
| `USE_ARC_ANTENNA_CHECK` | Specifies whether to use the openroad ARC antenna checker or magic antenna checker. 0=magic antenna checker, 1=ARC OR antenna checker <br> (Default: `1`)
| `RUN_SPEF_EXTRACTION` | Specifies whether or not to run SPEF extraction on the routed DEF. 1=enabled 0=disabled <br> Default: `1` |
| `SPEF_WIRE_MODEL` | Specifies the wire model used in SPEF extraction. Options are `L` or `Pi`  <br> Default: `L` |
| `SPEF_EDGE_CAP_FACTOR` | Specifies the edge capacitance factor used in SPEF extraction. Ranges from 0 to 1 <br> Default: `1` |
| `GENERATE_FINAL_SUMMARY_REPORT` | Specifies whether or not to generate a final summary report after the run is completed. Check command `generate_final_summary_report`. 1=enabled 0=disabled <br> Default: `1` |
| `MAGIC_CONVERT_DRC_TO_RDB` | Specifies whether or not generate a Calibre RDB out of the magic.drc report. Result is saved in `<run_path>/results/magic/`. 1=enabled 0=disabled <br> Default: `1`|
| `RUN_CVC` | Runs CVC on the output spice, which is a Circuit Validity Checker. Voltage aware ERC checker for CDL netlists. Thus, it controls the command `run_lef_cvc`. 1=Enabled, 0=Disabled. <br> Default: `1` |

### Checkers

| Variable      | Description                                                   |
|---------------|---------------------------------------------------------------|
| `CHECK_UNMAPPED_CELLS` | Checks if there are unmapped cells after synthesis and aborts if any was found. 1 = Enabled, 0 = Disabled <br> (Default: `1`)|
| `CHECK_ASSIGN_STATEMENTS` | Checks for assign statement in the generated gate level netlist and aborts of any was found.1 = Enabled, 0 = Disabled <br> (Default: `0`)|
| `QUIT_ON_TR_DRC` | Checks for DRC violations after routing and exits the flow if any was found. 1 = Enabled, 0 = Disabled <br> (Default: `1`)|
| `QUIT_ON_MAGIC_DRC` | Checks for DRC violations after magic DRC is executed and exits the flow if any was found. 1 = Enabled, 0 = Disabled <br> (Default: `1`)|
| `QUIT_ON_ILLEGAL_OVERLAPS` | Checks for illegal overlaps during magic extraction. In some cases, these imply existing undetected shorts in the design. It also exits the flow if any was found. 1 = Enabled, 0 = Disabled <br> (Default: `1`)|
| `QUIT_ON_LVS_ERROR` | Checks for LVS errors after netgen LVS is executed and exits the flow if any was found. 1 = Enabled, 0 = Disabled <br> (Default: `1`)|


[0]: ./../designs/spm/pin_order.cfg

```

how to set this parameters for floorplaning:

in file **floorplan.tcl** in folder **/home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/configuration** the default values are set

```tcl
# Copyright 2020 Efabless Corporation
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#      http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

# Floorplan defaults
set ::env(FP_IO_VMETAL) 3
set ::env(FP_IO_HMETAL) 4

set ::env(FP_SIZING) relative
set ::env(FP_CORE_UTIL) 50
set ::env(FP_CORE_MARGIN) 0
set ::env(FP_ASPECT_RATIO) 1

set ::env(FP_PDN_VOFFSET) 16.32
set ::env(FP_PDN_VPITCH) 153.6
set ::env(FP_PDN_HOFFSET) 16.65
set ::env(FP_PDN_HPITCH) 153.18

set ::env(FP_PDN_AUTO_ADJUST) 1

set ::env(FP_PDN_CORE_RING) 0
set ::env(FP_PDN_ENABLE_RAILS) 1

set ::env(FP_PDN_CHECK_NODES) 1

set ::env(FP_IO_MODE) 1; # 0 matching mode - 1 random equidistant mode
set ::env(FP_IO_HLENGTH) 4
set ::env(FP_IO_VLENGTH) 4
set ::env(FP_IO_VEXTEND) -1
set ::env(FP_IO_HEXTEND) -1
set ::env(FP_IO_VTHICKNESS_MULT) 2
set ::env(FP_IO_HTHICKNESS_MULT) 2

set ::env(BOTTOM_MARGIN_MULT) 4
set ::env(TOP_MARGIN_MULT) 4
set ::env(LEFT_MARGIN_MULT) 12
set ::env(RIGHT_MARGIN_MULT) 12

set ::env(FP_HORIZONTAL_HALO) 10
set ::env(FP_VERTICAL_HALO) $::env(FP_HORIZONTAL_HALO)

set ::env(DESIGN_IS_CORE) 1

```

in design folder we have your next config file called **config.tcl**, our design folder **/home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a** and next **sky130A_sky130_fd_sc_hd_config.tcl* in design folder too.

**config.tcl**

``` tcl

# Design
set ::env(DESIGN_NAME) "picorv32a"

set ::env(VERILOG_FILES) "./designs/picorv32a/src/picorv32a.v"
set ::env(SDC_FILE) "./designs/picorv32a/src/picorv32a.sdc"

set ::env(CLOCK_PERIOD) "5.000"
set ::env(CLOCK_PORT) "clk"


set ::env(CLOCK_NET) $::env(CLOCK_PORT)




set filename $::env(OPENLANE_ROOT)/designs/$::env(DESIGN_NAME)/$::env(PDK)_$::env(STD_CELL_LIBRARY)_config.tcl
if { [file exists $filename] == 1} {
	source $filename
}
```

**sky130A_sky130_fd_sc_hd_config.tcl**

``` tcl
# SCL Configs
set ::env(GLB_RT_ADJUSTMENT) 0.1

set ::env(SYNTH_MAX_FANOUT) 6
set ::env(CLOCK_PERIOD) "24.73"
set ::env(FP_CORE_UTIL) 35
set ::env(PL_TARGET_DENSITY) [ expr ($::env(FP_CORE_UTIL)+5) / 100.0 ]

```

the lowest priority is system default file(**floorplan.tcl**), next is **config.tcl** in design folder and next is **sky130A_sky130_fd_sc_hd_config.tcl** in design folder too.

next is to run flooplaning in OpenLANE:

run_floorplan

![12-05-2025_16-40-58](https://github.com/user-attachments/assets/e4df482a-d034-4098-8039-6c6c08e7c28f)

last page of floorplan generation:

![12-05-2025_16-45-55](https://github.com/user-attachments/assets/7eeec25f-301c-421b-81ba-e43dd6f96da5)

  - ##### Review floorplan files and steps to view floorplan

now we go to run's folder: **/home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/12-05_13-55**

![12-05-2025_16-49-38](https://github.com/user-attachments/assets/005ef980-d8db-4e28-b0db-85ad867f8f9e)

we check now that the right switches were used - for that we go in the log folder **/home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/12-05_13-55/logs**

![12-05-2025_16-53-02](https://github.com/user-attachments/assets/2d40d8b0-32ab-4e2a-84ad-034fc893355b)

then in flooplan folder:

![12-05-2025_16-54-28](https://github.com/user-attachments/assets/a7ab678d-2164-4a2a-9ac2-3c9cfb08ad58)

check **picorv32a.floorplan.def** in **/home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/12-05_13-55/results/floorplan** folder.
At begin you can see the coplete dia area of the chip.

**DIEAREA ( 0 0 ) ( 660685 671405 ) ;**

![12-05-2025_21-21-08](https://github.com/user-attachments/assets/e4a667c9-0488-4354-9be0-cee021429347)

now start magic from **/home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/12-05_13-55/results/floorplan** with following cmd-line:

**magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def &**

![12-05-2025_21-41-07](https://github.com/user-attachments/assets/9228cdc6-9775-4575-bff1-8345b525d74d)

  - ##### Review floorplan layout in Magic

in magic you have following commands:

	s - select layout
 	v - center layout on screen

to select a oprtion of the screen you do first a **left mouse click** and then a **rigth mouse click** and

	z - zoom in

 to get info about a object select opject with crosshair and press "s" on keyboard

 	s - object info

	to get the opject info switch to Main window and enter "what" at promt-line %

![12-05-2025_21-57-55](https://github.com/user-attachments/assets/b7a00156-fa93-40ca-b9fd-dc0cda90e80e)

	standard cell's are placed in lower left corner in floorplan.

![12-05-2025_22-14-46](https://github.com/user-attachments/assets/c3ddad2d-23d9-4543-935e-9628e317f6f0)
  
- ### Library Binding and Placement
  - #### Netlist binding and initial place design

	let now transform out netlist to physical cell's. Eack logical component like a flip-flop, inverter, NAND-gate have physical dimension, like a width & higth.
	that's our ecample netlist wich wi translate to phyical cells

![13-05-2025_09-29-03](https://github.com/user-attachments/assets/48c64f56-c385-4c53-a8b1-cb1f91392b8b)

	now we give alle logical gate a phisical property.

 ![13-05-2025_09-30-00](https://github.com/user-attachments/assets/60a98434-c63f-434a-b067-7547069d4017)

	if we remove all wires and focus on phsical components it lokk like below slide and this is called a "Library".
 	A library have not only physical attributs it store also info about delay, timing relevan information and so callen "when" condition. 

 ![13-05-2025_09-33-56](https://github.com/user-attachments/assets/48a2fe45-10cd-4469-a6d5-66846e3eeabc)

	a library storts also differen flavour's of a cell, in our examplel we have cells of bigger size which have a lower delay.

 ![13-05-2025_09-39-52](https://github.com/user-attachments/assets/7862bdf9-af42-4530-b528-ac0bfb079601)

 	next step is placement of the cell on the floorplan.
  	we have a well defines floorplan with input & output pis, we have the netlist and we have a shap of out design of each and evry component.
   
![13-05-2025_09-43-34](https://github.com/user-attachments/assets/07833aaf-62a2-41fe-a9cf-e2d8a598239b)

   	now we place the components of the netlist on the floorplan in a proper way. 
    	The FF1 is connected to Din1, so we place cell close to pin Din1, same for FF2 which is close to Dout1 and so on.
    	
![13-05-2025_09-49-05](https://github.com/user-attachments/assets/9590adb8-45d5-4fb7-8c74-429fa2b4df44)

     	now we placed the complet netlist to out foolplan

  - #### Optimize placement using estimated wite-length and capacitance    
      
![13-05-2025_09-55-20](https://github.com/user-attachments/assets/dc57bc1a-c34b-491a-b644-51598ca60608)

	now we solve the problem of distance between cell's , this is called "optimized placement"
	we have now to solve the problem regarding distance and capacitance shown in example below.
 
![13-05-2025_09-59-37](https://github.com/user-attachments/assets/753fb9d6-857e-46ff-8c22-3385f3ad8b24)

	to maintain signal integrity we insert buffers in our design

 ![13-05-2025_10-03-13](https://github.com/user-attachments/assets/89aaa9c1-c838-49a8-bff7-b4a71f56c03d)

 	the final floorplan look like this taken distance into consideration

  ![13-05-2025_10-06-27](https://github.com/user-attachments/assets/e328e68d-855c-47ca-9e31-dc4616cb411f)

  - #### Final plancement optimization

	setup timing analysis
	library characterisation and modeling.
 	1. part is synthesis of the netlist

![13-05-2025_10-31-10](https://github.com/user-attachments/assets/a7d0de0e-e184-417c-a656-1cfe17430f52)

  	2. part floorplaning & 3. part is placement

![13-05-2025_10-46-45](https://github.com/user-attachments/assets/046f52ca-b9f7-407f-96e2-a8883522b062)

	next is CTS (clock tree synthesis) - goal is that each FF get rising edge of CLK at the same time

 ![13-05-2025_10-51-14](https://github.com/user-attachments/assets/5c1612f6-2901-4903-9304-6c131f3b6862)

 	next stepis routing, i.e. make routing shown in slide below

  ![13-05-2025_10-55-20](https://github.com/user-attachments/assets/991f6ae5-935f-4e19-a2c1-3e7c486e3507)

  	final we come to STA (Static Timing Analysis), here you see the setup time, the hold time, max. frequence of a circuit.
   	Its the last sage of design flow, called often a sign off.

   ![13-05-2025_10-59-52](https://github.com/user-attachments/assets/7c64e981-a593-4f22-9612-ffbaba8e1611)

  - #### Need for libraries and characterizatiion

  - #### Congestion aware placement using RePlace

	we do a global placement and a detailed placement as next step in openLANE tool.
	objective is to reducing wire length.

	run_placement in openLANE

![13-05-2025_11-17-48](https://github.com/user-attachments/assets/ee318dd3-73ce-4b82-9ec0-6b052056ec94)

checking placement after run

![13-05-2025_11-24-18](https://github.com/user-attachments/assets/346e17ed-1646-4ecb-9e38-cb3ba16bb855)

validate now with magic: **magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def &**

![13-05-2025_11-27-02](https://github.com/user-attachments/assets/099d03fe-3c6b-4c59-a73d-859a04c4ab2d)

if you zoom in you can see placement of standard cell's 

![13-05-2025_11-38-25](https://github.com/user-attachments/assets/9974543d-e1e1-45c1-b447-0743bfc098ab)

  
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
 
  Lab:

	Option to do changes on the fly
	check pin config in magic

	set ::env(FP_IO_MODE) 2
	run_floorplan

![13-05-2025_18-05-36](https://github.com/user-attachments/assets/50b2c984-4424-4078-97a0-29bc918ea82f)

	check def file in result/floorplan folder

![13-05-2025_18-09-00](https://github.com/user-attachments/assets/eff68a61-0f7c-48a3-ac3e-15c30b608adc)

validate new pin layout with magic

![2025-05-13_22-02-30](https://github.com/user-attachments/assets/ea9b1479-9182-4f14-87e3-04c8648a8d7a)




  - SPICE deck creation for CMOS inverter
  - SPICE simulation lab for CMOS inverter
  - Switching Threshold Vm
  - Static and dynamic simulation of CMOS inverter
  - Lab steps to git clone vsdstdcelldesign

	clone vsdstdcelldesign repositiry

``` sh
git clone https://github.com/nickson-jose/vsdstdcelldesign.git
```
![2025-05-13_22-15-14](https://github.com/user-attachments/assets/b5149f91-dd00-4437-8b86-07d0d807e91e)

copy tech file to vsdstdcelldesign folder

cd /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic

cp sky130A.tech /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/vsdstdcelldesign/

verify that tech file is in folder

![2025-05-13_22-24-45](https://github.com/user-attachments/assets/f4ab3982-178f-4270-b699-dce93ab206ac)

check inverter with magic tool wit following command: **magic -T sky130A.tech sky130_inv.mag &**, exec this in folder **/home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/vsdstdcelldesign**

![2025-05-13_22-31-00](https://github.com/user-attachments/assets/1287af26-d226-4c7f-90ca-387e944f1fac)

check if nmos or pmos:
select green area and enter "what" in console window.

![2025-05-14_21-40-12](https://github.com/user-attachments/assets/8d9efc19-8e21-4685-9eeb-d9caf6a89516)

same is checking for pmos.

![2025-05-14_21-42-37](https://github.com/user-attachments/assets/ddd6a15c-e380-4b28-8312-7bd6b2e7f762)

to check connectivity of output select it with 2 times "s" so you see connection, in out example output is connected both with nmos & pmos, which is correct.

![2025-05-14_21-45-01](https://github.com/user-attachments/assets/81c0bfed-881e-4110-b79b-1c0298786b60)

![vsdstdcelldesign](https://github.com/nickson-jose/vsdstdcelldesign) show process of stad cell creation.

create an extraction file in **/home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/vsdstdcelldesign** with "extract" command in magic console window

![2025-05-14_22-02-26](https://github.com/user-attachments/assets/e97e4ca0-50bc-4b4d-866e-81fa63ca908b)

check thes ext file is there

![2025-05-14_22-04-15](https://github.com/user-attachments/assets/5c56a165-4134-4555-a720-e977bed21568)

now we creat a spice file

in console window enter:
ext2spice cthresh 0 rthresh 0
ext2spice

![2025-05-14_22-09-33](https://github.com/user-attachments/assets/64d90a5f-3412-413a-9e2c-6522ef8ec210)

spice file is there:

![2025-05-14_22-11-50](https://github.com/user-attachments/assets/840eb9ef-4355-46a5-8a5c-22a4b592c222)

contens of spice file:

![2025-05-14_22-13-57](https://github.com/user-attachments/assets/d011260b-9c0e-49c8-87c5-e0a002143f2d)

modifiy spice file

add .include...., add VDD & VSS line, add Va .... line, add .trans 1n 20n, .contro,.end., .end.

```spice
* SPICE3 file created from sky130_inv.ext - technology: sky130A

.option scale=0.01u
.include ./libs/pshort.lib
.include ./libs/nshort.lib

//.subckt sky130_inv A Y VPWR VGND
M1000 Y A VPWR VPWR pshort_model.0 w=37 l=23
+  ad=1443 pd=152 as=1517 ps=156
M1001 Y A VGND VGND nshort_model.0 w=35 l=23
+  ad=1435 pd=152 as=1365 ps=148
VDD VPWR 0 3.3V
VSS VGND 0 0V
Va A VGND PULSE(0V 3.3V 0 0.1ns 0.1ns 2ns 4ns)
C0 A Y 0.05fF
C1 Y VPWR 0.11fF
C2 A VPWR 0 0.07fF
C3 Y 0 0.24fF
C4 VPWR 0 0.59fF
//.ends
.tran 1n 20n

.control
run
.endc
.end


```
now run modified spice file with ngspice: **ngspice sky130_inv.spice*

![15-05-2025_18-02-31](https://github.com/user-attachments/assets/49d04f97-fb34-4f25-a553-dd4ba859803b)

now we plot output Y over time with command**plot yvs time a**

![15-05-2025_18-03-48](https://github.com/user-attachments/assets/2e703210-6c29-454f-845c-8c33849c5e8b)

![15-05-2025_17-54-33](https://github.com/user-attachments/assets/75139d66-55b1-46ec-b620-6c48229f31e8)




![2025-05-14_22-44-34](https://github.com/user-attachments/assets/f5bf504c-3587-421f-819c-4ab272e795e9)


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
 
check [magic](http://opencircuitdesign.com/magic/index.html) for magic commands

![2025-05-14_23-12-11](https://github.com/user-attachments/assets/173cf4ac-9774-40fe-8637-896f2846efd3)




  - Lab introduction to ky130 pks's and steps to download labs
  - Lab introduction to Magic and steps to load Sky130 tech-rules

![2025-05-15_00-14-20](https://github.com/user-attachments/assets/454a24d0-2e95-49b0-b636-d43cbc25c4c1)



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

