# EXP-4 4Bit-Up-Down-Asynchronous-Reset-Counter-Synthesis

## Aim:

Synthesize 4Bit-Up-Down-Asynchronous-Reset-Counter design using Constraints and analyse reports, Timing, area and Power.

## Tool Required:

Functional Simulation: Incisive Simulator (ncvlog, ncelab, ncsim)

Synthesis: Genus

### Step 1: Getting Started

Synthesis requires three files as follows,

◦ Liberty Files (.lib)

◦ Verilog/VHDL Files (.v or .vhdl or .vhd)

◦ SDC (Synopsis Design Constraint) File (.sdc)

 ### Step 2 : Creating an SDC File

•	In your terminal type “gedit input_constraints.sdc” to create an SDC File if you do not have one.

•	The SDC File must contain the following commands;

create_clock -name clk -period 2 -waveform {0 1} [get_ports "clk"]

set_clock_transition -rise 0.1 [get_clocks "clk"]

set_clock_transition -fall 0.1 [get_clocks "clk"]

set_clock_uncertainty 0.01 [get_ports "clk"]

set_input_delay -max 0.8 [get_ports "rst"] -clock [get_clocks "clk"]

set_output_delay -max 0.8 [get_ports "count"] -clock [get_clocks "clk"]

i→ Creates a Clock named “clk” with Time Period 2ns and On Time from t=0 to t=1.

ii, iii → Sets Clock Rise and Fall time to 100ps.

iv → Sets Clock Uncertainty to 10ps.

v, vi → Sets the maximum limit for I/O port delay to 1ps.

### Step 3 : Performing Synthesis

The Liberty files are present in the library path,

• The Available technology nodes are 180nm ,90nm and 45nm.

• In the terminal, initialise the tools with the following commands if a new terminal is being
used.

◦ csh

◦ source /cadence/install/cshrc

• The tool used for Synthesis is “Genus”. Hence, type “genus -gui” to open the tool.

• Genus Script file with .tcl file Extension commands are executed one by one to synthesize the netlist.

#### Synthesis RTL Schematic :

![Screenshot 2024-11-11 113909](https://github.com/user-attachments/assets/52aebc42-f5ca-4529-997f-a23b08d645d9)

#### Area report:
============================================================
  Generated by:           Genus(TM) Synthesis Solution 21.14-s082_1
  Generated on:           Nov 11 2024  01:07:20 am
  Module:                 counter
  Operating conditions:   slow (balanced_tree)
  Wireload mode:          enclosed
  Area mode:              timing library

============================================================

Instance Module  Cell Count  Cell Area  Net Area   Total Area   Wireload  

--------------------------------------------------------------------------
counter                  20    139.270     0.000      139.270 <none> (D)  
  (D) = wireload is default in technology library

#### Power Report:

Instance: /counter
Power Unit: W
PDB Frames: /stim#0/frame#0

  -------------------------------------------------------------------------
    Category         Leakage     Internal    Switching        Total    Row%
  -------------------------------------------------------------------------
      memory     0.00000e+00  0.00000e+00  0.00000e+00  0.00000e+00   0.00%
    register     4.32910e-07  3.64579e-05  1.19525e-06  3.80861e-05  71.51%
       latch     0.00000e+00  0.00000e+00  0.00000e+00  0.00000e+00   0.00%
       logic     3.44255e-07  8.22664e-06  3.84810e-06  1.24190e-05  23.32%
        bbox     0.00000e+00  0.00000e+00  0.00000e+00  0.00000e+00   0.00%
       clock     0.00000e+00  0.00000e+00  2.75400e-06  2.75400e-06   5.17%
         pad     0.00000e+00  0.00000e+00  0.00000e+00  0.00000e+00   0.00%
          pm     0.00000e+00  0.00000e+00  0.00000e+00  0.00000e+00   0.00%
  -------------------------------------------------------------------------
    Subtotal     7.77165e-07  4.46846e-05  7.79735e-06  5.32591e-05 100.00%
  Percentage           1.46%       83.90%       14.64%      100.00% 100.00%
  
#### Timing Report: 
====================================================================
  Generated by:           Genus(TM) Synthesis Solution 21.14-s082_1
  Generated on:           Nov 11 2024  01:07:14 am
  Module:                 counter
  Operating conditions:   slow (balanced_tree)
  Wireload mode:          enclosed
  Area mode:              timing library

====================================================================

Path 1: MET (718 ps) Setup Check with Pin count_reg[2]/CK->D
          Group: clk
     Startpoint: (F) rst
          Clock: (R) clk
       Endpoint: (R) count_reg[2]/D
          Clock: (R) clk

                     Capture       Launch     
        Clock Edge:+    2000            0     
        Drv Adjust:+       0            0     
       Src Latency:+       0            0     
       Net Latency:+       0 (I)        0 (I) 
           Arrival:=    2000            0     
                                              
             Setup:-     166                  
       Uncertainty:-      10                  
     Required Time:=    1824                  
      Launch Clock:-       0                  
       Input Delay:-     800                  
         Data Path:-     306                  
             Slack:=     718                  

Exceptions/Constraints:
  input_delay             800             input_constraints.sd_line_5 

---------------------------------------------------------------------------------------
Timing Point   Flags   Arc   Edge   Cell     Fanout Load Trans Delay Arrival Instance 
                                                     (fF)  (ps)  (ps)   (ps)  Location 
                                                    
--------------------------------------------------------------------------------------
  rst            -       -     F     (arrival)      3  6.2     0     0     800    (-,-) 
  g310__8246/Y   -       B->Y  R     NOR2XL         3  4.9   170   126     926    (-,-) 
  g297__5107/Y   -       A0->Y R     AO22X1         1  1.6    55   180    1106    (-,-) 
  count_reg[2]/D <<<     -     R     DFFQX1         1    -     -     0    1106    (-,-) 
  
---------------------------------------------------------------------------------------
## Result: 
The generic netlist has been created, and area, power, and timing reports have been tabulated and generated using Genus.

