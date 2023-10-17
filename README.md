PWM GENERATOR:

The PWM Generator block generates pulses for carrier-based pulse width modulation (PWM) converters using two-level topology. The block can be used to fire the forced-commutated devices (FETs, GTOs, or IGBTs) of single-phase, two-phase, three-phase, two-level bridges, or a combination of two three-phase bridges.


Pulse width modulation (PWM) is a modulation technique that generates variable-width pulses to represent the amplitude of an analog input signal.



In this repo we perform 3 main steps :

1. SYNTHESIS AND GLS.
   
2. PHYSICAL DESIGN
   
3. GDS TO TAPEOUT


SYNTHESIS AND GATE LEVEL SIMULATION:

1.  cd ~/sky130RTLDesignAndSynthesisWorkshop/verilog_files

2.  iverilog pes_pwm_gen.v pes_pwm_gen_tb.v -o pes_pwm_gen.out

3.  ./pes_pwm_gen.out 

4.gtkwave pwm.vcd


![WhatsApp Image 2023-10-16 at 15 32 34_bf388a8f](https://github.com/ughdeiek/PWM-Generator/assets/142580251/bdadba7f-1782-4e77-8ea0-d75612172eaa)


   
