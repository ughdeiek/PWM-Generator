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



   
    
  9. ./a.out


   ![WhatsApp Image 2023-10-16 at 15 32 37_46da2253](https://github.com/ughdeiek/PWM-Generator/assets/142580251/fb377a54-ce72-445c-81f1-21cc4f776043)



  10. gtkwave pwm.vcd

     
