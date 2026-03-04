# Custom Standard Cell Design — sky130_vsdinv
> PicoRV32a — OpenLANE Physical Design Flow

![Tool](https://img.shields.io/badge/Tool-Magic%20VLSI-blue)
![Tool](https://img.shields.io/badge/Tool-Ngspice-blue)
![Tool](https://img.shields.io/badge/Tool-OpenSTA-blue)
![PDK](https://img.shields.io/badge/PDK-Sky130-orange)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen)

<h2>🔍 Overview</h2>

- Designed a custom CMOS inverter **sky130_vsdinv** from scratch in **Magic VLSI** following Sky130 DRC rules — extracted SPICE netlist, simulated with **Ngspice**, and characterised timing parameters.
- Aligned layout to Sky130 routing tracks, extracted LEF file, and integrated the custom cell into the OpenLANE flow — verified post-synthesis and post-CTS.

<h2>⚙️ Tasks Covered</h2>

| Task | Description |
|:---|:---|
| Repository Setup | Cloned vsdstdcelldesign — inverter layout and tech files |
| Layer Analysis | PMOS/NMOS identification, Sky130 layer mapping, DRC verification |
| Layout & SPICE Extraction | Input A, Output Y, VDD, GND — extraction to SPICE |
| SPICE Simulation | Sky130 models, pulse input, transient simulation |
| Inverter Characterisation | Rise time, fall time, propagation delay, Vth verification |
| Grid to Track Alignment | Layout aligned to Sky130 routing tracks — pin and boundary verified |
| LEF Extraction | sky130_vsdinv.lef generated — integrated into OpenLANE flow |
| Timing Library Integration | Liberty .lib files loaded — cell delay and capacitance verified |

<h2>📊 Key Observations</h2>

| Metric | Details |
|:---|:---|
| Cell Name | sky130_vsdinv |
| Design Tool | Magic VLSI |
| Simulation Tool | Ngspice |
| Technology | Sky130 130nm — sky130A.tech |
| DRC Status | Clean — 0 violations |
| Output Files | sky130_inv.spice, sky130_vsdinv.lef |
| Library Corner | sky130_fd_sc_hd__tt_025C_1v80.lib — TT 25°C 1.8V |

<h2>📝 Stage Details</h2>

**Task 1 — Cloning Custom Inverter Repository** &nbsp;|&nbsp; `git clone` `Magic` `sky130A`

Cloned `vsdstdcelldesign` repository into OpenLANE working directory. Verified directory structure — `sky130_inv.mag`, `sky130A.tech`, and `libs/` confirmed present. Opened inverter layout in Magic using `magic -T sky130A.tech sky130_inv.mag`.

**Task 2 — Sky130 Layer & Layout Analysis** &nbsp;|&nbsp; `Magic` `DRC` `Sky130 Layers`

Identified PMOS (top — pdiff connected to VDD) and NMOS (bottom — ndiff connected to GND). Polysilicon gate verified as common input crossing both diffusion regions. Metal layers mapped — li1 for local interconnect, mcon/viali for contacts. Substrate taps confirmed for latch-up prevention. DRC status verified clean.

**Task 3 — Layout Creation & SPICE Extraction** &nbsp;|&nbsp; `extract all` `ext2spice` `Magic tkcon`

Input port A, output port Y, VDD and GND rails verified. Extraction file generated using `extract all`. Converted to SPICE using `ext2spice lvs` and `ext2spice` — `sky130_inv.spice` generated with parasitic capacitances included.

**Task 4 — SPICE Deck Creation** &nbsp;|&nbsp; `Ngspice` `sky130 models` `.tran`

Sky130 NMOS and PMOS model files included. VDD supply defined at 1.8V. Pulse input defined with rise/fall times and pulse width. Transient simulation `.tran 0.01n 20n` executed in Ngspice without errors.

**Task 5 — Inverter Characterisation** &nbsp;|&nbsp; `Ngspice` `plot y vs time a`

Input vs output waveforms plotted. Rise time, fall time, and propagation delay measured at 10%, 50%, 90% crossing points. Inverter threshold voltage verified near VDD/2 — confirming balanced PMOS/NMOS sizing.

**Task 6 — Grid to Track Alignment** &nbsp;|&nbsp; `tracks.info` `Magic` `Sky130 Routing Grid`

Examined `tracks.info` from Sky130 PDK — offset and pitch extracted for li1, met1, met2 layers. Layout grid aligned to match routing tracks. Input and output pin centres verified at horizontal and vertical track intersections. Cell width and height confirmed as integer multiples of track pitch. VDD and GND rails centred on tracks for PDN compatibility.

**Task 7 — LEF Extraction** &nbsp;|&nbsp; `lef write` `sky130_vsdinv.lef` `PR Boundary`

Ports named and classified — A as input signal, Y as output signal, VDD and GND as power/ground. PR boundary defined and aligned to routing tracks. LEF extracted — `sky130_vsdinv.lef` generated. LEF file verified — MACRO block, PIN A, PIN Y, and OBS sections confirmed. LEF moved to `designs/picorv32a/src/` and linked in config.tcl.

**Task 8 — Timing Library Integration** &nbsp;|&nbsp; `sky130_fd_sc_hd__tt_025C_1v80.lib` `OpenSTA`

Located Liberty files — TT corner at 25°C and 1.8V verified. Cell area, leakage power, and LUT delay tables inspected. Rise/fall delay tables cross-checked against Ngspice simulation results. Pin capacitances verified. Library files loaded into OpenSTA — picorv32a netlist linked and timing models including sky130_vsdinv confirmed STA-ready.

<h2>🖼️ Implementation Results</h2>

### Cloning Custom Inverter Repository
![Clone 1](1_Lab_steps_to_clone_github_1.png)
![Clone 2](1_Lab_steps_to_clone_github_2.png)
![Clone 3](1_Lab_steps_to_clone_github_3.png)
![Clone 4](1_Lab_steps_to_clone_github_4.png)
![Clone 5](1_Lab_steps_to_clone_github_5.png)

### Sky130 Layer & Layout Analysis
![Layer 1](2_Lab_to_Sky130_basic_layerlayouts_1.png)
![Layer 2](2_Lab_to_Sky130_basic_layerlayouts_2.png)

### Layout Creation & SPICE Extraction
![Layout 1](3_Lab_step_to_creat_std_layout_1.png)
![Layout 2](3_Lab_step_to_creat_std_layout_2.png)
![Layout 3](3_Lab_step_to_creat_std_layout_3.png)
![Layout 4](3_Lab_step_to_creat_std_layout_4.png)
![Layout 5](3_Lab_step_to_creat_std_layout_5.png)
![Layout 6](3_Lab_step_to_creat_std_layout_6.png)
![Layout 7](3_Lab_step_to_creat_std_layout_7.png)
![Layout 8](3_Lab_step_to_creat_std_layout_8.png)

### SPICE Deck Creation
![SPICE 1](4_Create_final_SPICE_deck_using_Sky130_tech_1.png)
![SPICE 2](4_Create_final_SPICE_deck_using_Sky130_tech_2.png)
![SPICE 3](4_Create_final_SPICE_deck_using_Sky130_tech_3.png)
![SPICE 4](4_Create_final_SPICE_deck_using_Sky130_tech_4.png)
![SPICE 5](4_Create_final_SPICE_deck_using_Sky130_tech_5.png)
![SPICE 6](4_Create_final_SPICE_deck_using_Sky130_tech_6.png)
![SPICE 7](4_Create_final_SPICE_deck_using_Sky130_tech_7.png)
![SPICE 8](4_Create_final_SPICE_deck_using_Sky130_tech_8.png)
![SPICE 9](4_Create_final_SPICE_deck_using_Sky130_tech_9.png)

### Inverter Characterisation
![Char 1](5_Characterize_inverter_using_sky130_model_files_1.png)
![Char 2](5_Characterize_inverter_using_sky130_model_files_2.png)
![Char 3](5_Characterize_inverter_using_sky130_model_files_3.png)
![Char 4](5_Characterize_inverter_using_sky130_model_files_4.png)
![Char 5](5_Characterize_inverter_using_sky130_model_files_5.png)
![Char 6](5_Characterize_inverter_using_sky130_model_files_6.png)
![Char 7](5_Characterize_inverter_using_sky130_model_files_7.png)
![Char 8](5_Characterize_inverter_using_sky130_model_files_8.png)
![Char 9](5_Characterize_inverter_using_sky130_model_files_9.png)
![Char 10](5_Characterize_inverter_using_sky130_model_files_10.png)
![Char 11](5_Characterize_inverter_using_sky130_model_files_11.png)
![Char 12](5_Characterize_inverter_using_sky130_model_files_12.png)

### Grid to Track Alignment
![Track 1](6_Convert_grid_info_to_track_info_1.png)
![Track 2](6_Convert_grid_info_to_track_info_2.png)
![Track 3](6_Convert_grid_info_to_track_info_3.png)
![Track 4](6_Convert_grid_info_to_track_info_4.png)
![Track 5](6_Convert_grid_info_to_track_info_5.png)
![Track 6](6_Convert_grid_info_to_track_info_6.png)
![Track 7](6_Convert_grid_info_to_track_info_7.png)
![Track 8](6_Convert_grid_info_to_track_info_8.png)

### LEF Extraction
![LEF 1](7_Convert_magic_layout_to_std_cell_1.png)
![LEF 2](7_Convert_magic_layout_to_std_cell_2.png)
![LEF 3](7_Convert_magic_layout_to_std_cell_3.png)
![LEF 4](7_Convert_magic_layout_to_std_cell_4.png)
![LEF 5](7_Convert_magic_layout_to_std_cell_5.png)
![LEF 6](7_Convert_magic_layout_to_std_cell_6.png)
![LEF 7](7_Convert_magic_layout_to_std_cell_7.png)

### Timing Library Integration
![Lib 1](8_Introduction_to_timing_libs_1.png)
![Lib 2](8_Introduction_to_timing_libs_2.png)
![Lib 3](8_Introduction_to_timing_libs_3.png)
![Lib 4](8_Introduction_to_timing_libs_4.png)
![Lib 5](8_Introduction_to_timing_libs_5.png)
![Lib 6](8_Introduction_to_timing_libs_6.png)
![Lib 7](8_Introduction_to_timing_libs_7.png)
![Lib 8](8_Introduction_to_timing_libs_8.png)
![Lib 9](8_Introduction_to_timing_libs_9.png)
![Lib 10](8_Introduction_to_timing_libs_10.png)
![Lib 11](8_Introduction_to_timing_libs_11.png)
![Lib 12](8_Introduction_to_timing_libs_12.png)
![Lib 13](8_Introduction_to_timing_libs_13.png)
![Lib 14](8_Introduction_to_timing_libs_14.png)
![Lib 15](8_Introduction_to_timing_libs_15.png)
![Lib 16](8_Introduction_to_timing_libs_16.png)
![Lib 17](8_Introduction_to_timing_libs_17.png)
![Lib 18](8_Introduction_to_timing_libs_18.png)

<h2>🔗 Navigation</h2>

[Back to Repository Overview](../README.md) &nbsp;|&nbsp; [Previous : 03 : Placement](../03%20:%20Placement) &nbsp;|&nbsp; [Next : 05 : Timing closure](../05%20:%20Timing%20closure)
