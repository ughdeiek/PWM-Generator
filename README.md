PWM GENERATOR:

The PWM Generator block generates pulses for carrier-based pulse width modulation (PWM) converters using two-level topology. The block can be used to fire the forced-commutated devices (FETs, GTOs, or IGBTs) of single-phase, two-phase, three-phase, two-level bridges, or a combination of two three-phase bridges.


Pulse width modulation (PWM) is a modulation technique that generates variable-width pulses to represent the amplitude of an analog input signal.



In this repo we perform 3 main steps :

1. SYNTHESIS AND GLS.
   
2. PHYSICAL DESIGN
   
3. GDS TO TAPEOUT


SYNTHESIS AND GATE LEVEL SIMULATION:

1.  cd ~/sky130RTLDesignAndSynthesisWorkshop/verilog_files

2.  iverilog pes_pwm_gen.v pes_pwm_tb.v -o pes_pwm_gen.out

3.  ./pes_pwm_gen.out 

4.gtkwave pwm.vcd


![WhatsApp Image 2023-10-16 at 15 32 34_bf388a8f](https://github.com/ughdeiek/PWM-Generator/assets/142580251/bdadba7f-1782-4e77-8ea0-d75612172eaa)


![WhatsApp Image 2023-10-16 at 15 32 39_12751d98](https://github.com/ughdeiek/PWM-Generator/assets/142580251/9cbfe210-ae20-4d07-b312-07d76c797aaf)




5. yosys


 ![WhatsApp Image 2023-10-16 at 15 32 35_fc8ea2d1](https://github.com/ughdeiek/PWM-Generator/assets/142580251/281858f8-a4a4-4b3c-976e-6221fc668087)


 ![WhatsApp Image 2023-10-16 at 15 32 35_7a63b1a9](https://github.com/ughdeiek/PWM-Generator/assets/142580251/2b68ced2-97af-4f71-aca5-dab73ea1dd36)

 6. synth -top pes_pwm_gen
    ![WhatsApp Image 2023-10-16 at 15 32 35_d97daaac](https://github.com/ughdeiek/PWM-Generator/assets/142580251/3c86834d-ac5a-4dbc-8d62-899cd668de43)
 
    ![WhatsApp Image 2023-10-16 at 15 32 36_04cd1aca](https://github.com/ughdeiek/PWM-Generator/assets/142580251/1d65b5fd-c749-487e-ab3c-aa4a4c5a81c9)


    ![WhatsApp Image 2023-10-16 at 15 32 36_bc6f4574](https://github.com/ughdeiek/PWM-Generator/assets/142580251/e57a00cb-a5d1-4b38-8054-43382f693d28)

  

  7. commands are visible in the screenshot below:

  ![WhatsApp Image 2023-10-16 at 15 32 37_1e74b56f](https://github.com/ughdeiek/PWM-Generator/assets/142580251/b0ed8f22-6625-486c-a9b3-4ed7288b7666)

  
  8. netlist creation:

     ![WhatsApp Image 2023-10-16 at 15 32 36_17886551](https://github.com/ughdeiek/PWM-Generator/assets/142580251/e729998d-8367-4021-8002-b085106ab469)


     ![WhatsApp Image 2023-10-16 at 15 32 37_08d22599](https://github.com/ughdeiek/PWM-Generator/assets/142580251/6c06e032-7c0a-4924-996f-46c6aca2e81d)



   
     ![WhatsApp Image 2023-10-16 at 15 32 37_46da2253](https://github.com/ughdeiek/PWM-Generator/assets/142580251/fb377a54-ce72-445c-81f1-21cc4f776043)
 



  10.  ./a.out




  11. gtkwave pwm.vcd











Physical Design

In integrated circuit design, physical design is a step in the standard design cycle which follows after the circuit design. At this step, circuit representations of the components (devices and interconnects) of the design are converted into geometric representations of shapes which, when manufactured in the corresponding layers of materials, will ensure the required functioning of the components. This geometric representation is called integrated circuit layout. This step is usually split into several sub-steps, which include both design and verification and validation of the layout.



OPENLANE:

OpenLane is an open-source VLSI flow built around open-source tools. That is, it's a collection of scripts that run these tools, in the right order, transforming their inputs and outputs as appropriate, and organising the results (like Berkeley's own HAMMER).


INSTALLATION OF OPENLANE:

https://openlane.readthedocs.io/en/latest/


INTERACTIVE MODE:







Generating Layout:

go to openlane folder and type the following commands : 


$ cd designs
$ mkdir pes_pwm_gen
$ cd pes_pwm_gen
$ mkdir src
$ vim config.tcl
$ cd src
$ vim pes_pwm_gen.v

The contents of config.tcl are:

![Screenshot from 2023-11-03 04-25-53](https://github.com/ughdeiek/PWM-Generator/assets/142580251/bd73829d-ef3a-4a92-9549-d2c31b3e8c26)



In openlane folder in terminal:



$ make mount
$ ./flow.tcl -interactive

    In the tcl console:

% package require openlane 0.9
% prep -design pes_pwm_gen




SYNTHESIS:

In ASIC flow, synthesis is the part of the front-end design, while the back-end design takes the synthesized netlist as an input. So, the synthesized netlist should meet all netlist quality checks to reduce multiple iterations, which reduces the turnaround time and efforts.

% run_synthesis

![Screenshot from 2023-11-03 04-16-13](https://github.com/ughdeiek/PWM-Generator/assets/142580251/cb0873f8-b56f-455d-af32-c14d4725c5d7)



From this we see that chip area for the module is : 1425.11


Flop ratio: Flop ratio = Number of D Flip flops / Total number of cells


Flop ratio for my design is 0.3125









FLOORPLAN:

Floor Planning involves determining the location, shape, and size of modules in a way that one can avoid congestion. Floor Planning is a quintessential step which decides the layout of the VLSI design. A well-optimized floor planning allows an ASIC design that has higher performance.

% run_floorplan


Core Area :

![Screenshot from 2023-11-03 04-06-50](https://github.com/ughdeiek/PWM-Generator/assets/142580251/aba2452e-e690-4aa8-b42e-17156db82cbe)





Die Area:

![Screenshot from 2023-11-03 04-07-27](https://github.com/ughdeiek/PWM-Generator/assets/142580251/69827254-d9e8-41f8-a9a9-bfa152723495)



Navigate to that directory and open in terminal and type:



magic -T /home/nirupama/OpenLane/pdks/sky130A/libs.tech/magic/sky130A.tech read lef ../../tmp/merged.lef def read pes_pwm_gen.floorplan.def &

Floorplan Picture:

![Screenshot from 2023-11-03 04-09-35](https://github.com/ughdeiek/PWM-Generator/assets/142580251/62bd2cd3-5945-4626-b9f6-81188eec1698)





PLACEMENT:

The goal of a placement tool is to arrange all the logic cells within the flexible blocks on a chip. Ideally, the objectives of the placement step are to. Guarantee the router can complete the routing step. Minimize all the critical net delays. Make the chip as dense as possible.

% run_placement



    Navigate to that directory and open in terminal and type:


magic -T /home/nirupama/OpenLane/pdks/sky130A/libs.tech/magic/sky130A.tech read lef ../../tmp/merged.lef def read pes_pwm_gen.placement.def &



Placement picture:

![Screenshot from 2023-11-03 04-10-39](https://github.com/ughdeiek/PWM-Generator/assets/142580251/db6360e5-cf84-4631-8c2b-cf63750fd1c5)


CLOCK TREE SYNTHESIS:

Clock Tree Synthesis (CTS) is the technique of balancing the clock delay to all clock inputs by inserting buffers/inverters along the clock routes of an ASIC design. As a result, CTS is used to balance the skew and reduce insertion latency.


% run_cts



ROUTING:

Routing in VLSI is making physical connections between signal pins using metal layers. Following Clock Tree Synthesis (CTS) and optimization, the routing step determines the exact pathways for interconnecting standard cells, macros, and I/O pins.

% run_routing


Navigate to that directory and open in terminal and type:


magic -T /home/nirupama/OpenLane/pdks/sky130A/libs.tech/magic/sky130A.tech read lef ../../tmp/merged.lef def read pes_pwm_gen.def &



![Screenshot from 2023-11-03 04-12-36](https://github.com/ughdeiek/PWM-Generator/assets/142580251/61830576-a049-4825-b7a2-bcad44a7d4ee)






Area Report:



![Screenshot from 2023-11-03 04-13-38](https://github.com/ughdeiek/PWM-Generator/assets/142580251/eb25ddb1-f583-40ad-b31b-3f0a8803b57b)







POST-LAYOUT RESULTS:


GATE COUNT:

![Screenshot from 2023-11-03 04-16-13](https://github.com/ughdeiek/PWM-Generator/assets/142580251/fd558ae0-610a-4084-af7e-2b15e3f9ed7d)


Total number of cells:  128



AREA:


![Screenshot from 2023-11-03 04-33-15](https://github.com/ughdeiek/PWM-Generator/assets/142580251/07e632bc-12bf-4458-a0be-35209da214b0)



PERFORMANCE:

![image](https://github.com/ughdeiek/PWM-Generator/assets/142580251/6a48d110-1970-4a28-9a33-e429f41d8a42)


FLOP/STANDARD CELL:



![Screenshot from 2023-11-03 04-16-13](https://github.com/ughdeiek/PWM-Generator/assets/142580251/aeda80d1-ccfe-4959-9dcb-d35539405801)



sky130_fd_sc_hd    dfxtp_2         40             is hence used and flop ratio is given by 0.3125.









     
