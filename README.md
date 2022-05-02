![image](https://user-images.githubusercontent.com/67062356/166248517-93e7886f-9bba-4859-8aef-e4857320900a.png)

# RTL-design-using-Verilog-with-SKY130-Technology
a Workshop by Kunal Ghosh and VSDIAT

Table of Contents:
- [Day 1 Introduction to Open-Source simulator Iverilog](##Day-1:)
- Day 2 Timing libs, hierarchical vs flat synthesis and efficient flop coding styles
Day 3 combinational and sequential optimisations
Day 4 GLS blocking vs non blocking and synthesis-simulation
Day 5 if case for loop and for generate

## Day-1:
### Introduction to Open-Source simulator Iverilog:
We were introduced to the tool iverilog along with the concepts of simulation, simulator, design, test bench and the vcd file(value change dump)


![image](https://user-images.githubusercontent.com/67062356/166202238-388a2350-ce3f-4b5f-9c20-873bf3337639.png)


The above image tells us about the functioning of a test bench in the design flow hierarchy
Test benches have no primary inputs or outputs.


 ![image](https://user-images.githubusercontent.com/67062356/166202256-945e2dc7-97af-4b27-8d81-1aef1aabb18b.png)
 

The role of iverilog as a simulator was explained along with the creation of the vcd file.


### Labs Using Iverilog and GTK Wave:
The first task on the first day of the workshop, we cloned the directories, the repository contained all the files and programs which would be required for the full duration of the workshop.
We had a walkthrough the files we cloned and came to know about the existence of the various Verilog and the library files. We also glazed through the various folders and sub folders. 


![image](https://user-images.githubusercontent.com/67062356/166202302-21a792ca-5db0-49ac-8bc9-4d65ec7ec36d.png)

 
•	In the image above we list all the files present within the verilog_files directory
•	The semantics are tb_file name for the test bench code of each Verilog file
•	Also visible are primitive.v and sky130_fd_sc_hd.v which are used in the later parts of the workshop for obtaining GLS and its GTKWave output. 

Next we had an introduction with the tool iverilog and the procedure to obtain the gtkwave output.
The first code we simulated was good_mux.v  
Here we look at the Verilog code of good_mux.v and its test bench:


![image](https://user-images.githubusercontent.com/67062356/166202372-4a6e8aad-b9ef-44d0-b214-1403bbacd2d3.png)

 
Next we used the GTKWave viewer to obtain the waveform output for the above Verilog code and analysed it for different inputs:


![image](https://user-images.githubusercontent.com/67062356/166202396-ae73d188-ac4a-4d6c-9391-95f9eec8df26.png)

 
We checked for different inputs and the corresponding outputs in the simulation output.

### Introduction to YOSYS and Logic Synthesis:

We understood the meaning and functioning of a synthesizer and the working of YOSYS tool as a synthesizer.


![image](https://user-images.githubusercontent.com/67062356/166202437-ea990672-72f5-4c81-a3bc-10dbf4e6469b.png)

 
We came to know about the existence of the .lib file and its use, and how YOSYS as a tool uses the Verilog code and the .lib file to synthesize the RTL design 
Existance of multiple cells of same type:
There exists multiple ‘flavours’ of the same cell e.g. AND gate in a library file. The different cells provide different areas and performance. Hence there are fast and slow cells.
Fast cells are used to reduce combinational delays and increase the overall performance of the design.
Slow cells are used to prevent hold violations and meet the requirements of the circuit


![image](https://user-images.githubusercontent.com/67062356/166202479-acf054d9-4bd1-45a6-aafe-2af6ae70a36a.png)

 
 
Finally, we looked at the hardware synthesis illustration of a Verilog model and how it maps to the various components. This helped us better understand about Synthesis of a Verilog code.


![image](https://user-images.githubusercontent.com/67062356/166202507-2d4c0552-7ca7-4bf2-a4e7-e8f484173b4c.png)

 
### Labs Using YOSYS and Sky130 PDKs:
We invoked the yosys tool and had a procedure overview of how to use the tool to generate the synthesis using the library files.
We read the library files from the respective directory


![image](https://user-images.githubusercontent.com/67062356/166202528-6a2be58d-1a84-4b81-a759-daf4c3073724.png)

 
Next we read the Verilog file which was to be synthesized
Next we specify the module which is to be synthesized using the respective command for it in YOSYS
Next we realised the logic in our Verilog files through the standard cells present in the library files.


![image](https://user-images.githubusercontent.com/67062356/166202557-1d72f040-c3f6-4cf3-87e3-e9cf9966d5c3.png)

 
Finally we view the synthesis output in the yosys dot viewer:


![image](https://user-images.githubusercontent.com/67062356/166202580-c3ea9745-119a-4a1d-963c-5476f761f819.png)

 
Next we created the netlist Verilog file for the synthesized design, we used the switch -noattr to discard all the additional information apart from the one we need, and then had a look at the file in text editor.


![image](https://user-images.githubusercontent.com/67062356/166202612-79b5a858-c453-4f32-b6eb-2a85ec6e80e2.png)

 
We analysed the different parts of the netlist file and their meanings
#### This concluded the first day of the workshop.

## Day 2:
Day 2 was titled ‘ Timing libs, hierarchical vs flat synthesis and efficient flop coding styles’
The topics which we were introduced to were 
•	Introduction to timing .libs
o	Theory and Lab sessions (Introduction to dot lib)
•	Hierarchical vs Flat Synthesis
o	Theory and Lab sessions(Hier synthesis flat synthesis)
•	Various Flop Coding Styles and optimisations
o	Why flop coding styles
o	Lab flop synthesis 
### Introduction to timing .libs:	
•	Library files

![image](https://user-images.githubusercontent.com/67062356/166227285-f9b7b756-1a01-4bc2-813d-990379cba00d.png)

 
o	First line tells the name of the library
o	130nm library
o	Tt-typical
o	Libraries can be slow fast or typical
o	25c-temperature
o	PVT-Process Voltage Temperature 
	Process-Variations due to fabrication
	Voltage-Variations due to Voltage
	Temperature-Variations due to temperature( semiconductors are very sensitive to temperature)
	PVT lists all the different working conditions for components across all working environments
 
 ![image](https://user-images.githubusercontent.com/67062356/166227302-6cd8f875-ed56-4785-9843-f4eb85a0e2f3.png)


o	Type of technology
o	Units 
o	Various cells present in the library for the different conditions

![image](https://user-images.githubusercontent.com/67062356/166227312-1b4c64cc-f3ef-4f86-9dbb-5441a050cbe3.png)


 
### Hierarchical vs Flat Synthesis:
•	Walkthrough multiple_modules.v file 

![image](https://user-images.githubusercontent.com/67062356/166227331-a1bb5735-110b-4c91-8912-5092cccf7c80.png)


 
o	2 submodules
o	1 AND gate 1 Or gate
o	Instantiation of two submodules
•	Expected hardware design:
 
 
 ![image](https://user-images.githubusercontent.com/67062356/166227352-e49fd210-9893-4c94-93b7-c47a40f41dde.png)


•	Synthesis of multiple_modules.v


 ![image](https://user-images.githubusercontent.com/67062356/166227365-02c07744-9687-4cb7-b688-23843cb81b0d.png)

 ![image](https://user-images.githubusercontent.com/67062356/166227390-8d1dd726-1b55-4203-a270-8a1b4bb368f2.png)



•	we obtain the dot viewer output


![image](https://user-images.githubusercontent.com/67062356/166227411-ab718375-2112-428a-bb49-e2f6e1336722.png)


 
•	we observe that the dot viewer shows two sub modules instead of the gates as in the structure of our code
•	hierarchies are preserved
•	preference of nand gate with inverted inputs over and gate  PMOS stacking results in low mobility
  
•	Next we use the flatten command to give out a flat netlist
•	This makes the hierarchies not preserved
 
 ![image](https://user-images.githubusercontent.com/67062356/166227438-e9d9d6bd-8966-45f5-9424-f3bf90e5514d.png)


•	Next we obtain the dot viewer output

![image](https://user-images.githubusercontent.com/67062356/166227461-f68e9b7b-ced7-4495-8992-ae0590ef9e11.png)

 
•	Now we obtain the yosys synthesis for submodule 1 only

![image](https://user-images.githubusercontent.com/67062356/166227496-b5f9ce12-cb92-4420-91fc-9d687c938f22.png)

 
•	Dot viewer output
 
 ![image](https://user-images.githubusercontent.com/67062356/166227518-b30e53c0-c36c-4643-add1-13ce8bec17e6.png)

 
•	Module level synthesis is preferred when there are multiple instantiations of the same module
•	Divide and conquer approach is another method to using multiple instantiations and massive designs
### Various Flop Coding Styles and optimisations:
•	How to code a flop and the various kinds of flops available and the coding styles
•	In combinational circuits the values get updated after a propagation delay
o	These may cause glitches
o	When one signals reach a combinational ckt and the others do not and hence the previous values get considered and leads to glitches
 
 ![image](https://user-images.githubusercontent.com/67062356/166227636-39194eae-ea7d-4cce-8f9b-9ae6a73d6497.png)


•	more combinational circuits lead to more glitches as the glitches get propagated
•	we use flops to overcome these glitches, a flop between comb circuits results in no propagation of glitches
•	outputs are stable

![image](https://user-images.githubusercontent.com/67062356/166227660-940ec09c-ed92-4976-a786-02bff921af7a.png)

 
•	reset and set can be synchronous or synchronous
•	asynchronous signals are not dependent on clock signals for their value
•	synchronous signals are dependent on clock signals for their application on the circuit
•	we may have both synchronous and asynchronous resets for the same circuit

![image](https://user-images.githubusercontent.com/67062356/166227685-aea27e77-774c-4670-bef9-2863d799d851.png)

 
•	next we obtain the iverilog simulation for the asynchronous reset dff

![image](https://user-images.githubusercontent.com/67062356/166227714-1d1656d9-5387-44bd-b46a-467c910348db.png)

 ![image](https://user-images.githubusercontent.com/67062356/166227728-03ab586b-a582-43e2-9c08-4a84117dd8e5.png)


 
•	next we also obtain the yosys dot viewer output for the same

![image](https://user-images.githubusercontent.com/67062356/166227750-5d4829b9-6965-4355-8c6d-ef3d195944d3.png)

 
•	Now we obtain the synchronous reset simulation and yosys outputs for the dff

 
 ![image](https://user-images.githubusercontent.com/67062356/166227764-ddc220ae-4570-4d4a-9b36-9e55223adc4f.png)

![image](https://user-images.githubusercontent.com/67062356/166227796-c3b7582f-48bc-4fcd-9137-41219a6e5c84.png)

 ![image](https://user-images.githubusercontent.com/67062356/166227815-497d3337-d43d-4c3a-819f-0bd1c7357169.png)


### Interesting Optimisations:
•	Multiplication by 2 is equivalent to concatenation of one 0 in the right to the multiplicand
•	We see this in action when we simulate the mult2 verilog file
 
 ![image](https://user-images.githubusercontent.com/67062356/166227847-9a01d808-c56d-4b55-92c9-dae28a0917b2.png)

 ![image](https://user-images.githubusercontent.com/67062356/166227863-f5ade1d8-e9d8-4b45-bb82-57acae575ff2.png)


•	We obtain the Verilog code and yosys dot viewer outputs for the same
 
 ![image](https://user-images.githubusercontent.com/67062356/166227880-4da8e79a-2ad2-402a-ab75-099d8edcf9fd.png)

 ![image](https://user-images.githubusercontent.com/67062356/166227911-b3e07025-a7b7-4760-b0ca-3d844624790b.png)



•	Next we see that multiplication by 9 is equal to multiplication by (8+1) which is equivalent to concating the number with itself
•	We see the Verilog code and obtain the synthesis output for the same
   
![image](https://user-images.githubusercontent.com/67062356/166227942-b851afec-5f87-42a3-b637-533e3cb5205c.png)
![image](https://user-images.githubusercontent.com/67062356/166227964-5cf5f232-e629-49bb-9cfa-a6093bf3b2c4.png)



This ends workshop day 2

## Day 3:
Day 3 was titled ‘combinational and sequential optimisations’
The topics which we were introduced to were
•	Introduction to Optimisations(theory)
•	Combinational Logic Optimisations(lab)
•	Sequential Logic Optimisations(lab)
•	Sequential Optimisations for unused outputs(theory)
### Introduction to Optimisations
Logic Optimisation:
•	Combinational Logic Optimisation
o	Squeezing the logic to get most optimised design(Area and power savings)
o	Constant Propagation(Direct Optimisation)

![image](https://user-images.githubusercontent.com/67062356/166248799-33d0540c-5628-403b-bae1-c18a060d5320.png)

 
o	Boolean Logic Optimisation
 
 ![image](https://user-images.githubusercontent.com/67062356/166248829-041e8419-d066-4c51-abd7-b606dd9fa31f.png)


•	Sequential Logic Optimisation
o	Sequential Constant(eg of DFF with ip grounded and reset signal, with nand gate, logic shortens to form

![image](https://user-images.githubusercontent.com/67062356/166248912-b52f7049-5ba9-452c-a019-3b1c3b233dd7.png)

 
o	Y=1, reset example for logic which cannot be optimised
•	Advanced Optimisations
o	Cloning
 
 
 ![image](https://user-images.githubusercontent.com/67062356/166248977-8d21eccc-b51d-4a65-a84e-9fa7730d1e7c.png)


o	Retiming

![image](https://user-images.githubusercontent.com/67062356/166249022-e39480a6-bf91-4d59-8cd7-7b0410bbd2da.png)

 
o	State Optimisation
	Optimisation of unused states
	This is optimisation of unused states. Using this technique, we can come up with the most optimised state machine.

Combinational Logic Optimisations(lab)

In this lab files  we use the opt_check files from the library
•	Our first example for optimisation was opt_check.v
o	We see the file which is a 2:1 mux is optimised into a 2 input and gate
 
 
![image](https://user-images.githubusercontent.com/67062356/166249259-6f4b40f6-1b6d-49a0-bdf6-d1879cf3b67a.png)

 ![image](https://user-images.githubusercontent.com/67062356/166249290-1661327b-601d-487b-adc5-271eeb5ccd74.png)


•	The next example is opt_check2 which is optimised as an or gate after synthesis

![image](https://user-images.githubusercontent.com/67062356/166249327-e362c258-76fa-430c-9cf6-ecdde3f96d90.png)

 
•	The next example was opt_check3.v which was synthesized as a 3 input and gate

![image](https://user-images.githubusercontent.com/67062356/166249356-f04314d1-b03a-49af-8a02-45527d096bc7.png)

 
•	We further synthesized multiple_modules_opt and opt_check4

![image](https://user-images.githubusercontent.com/67062356/166249415-a031d80b-2c86-4a28-89a0-0869f4824299.png)

 ![image](https://user-images.githubusercontent.com/67062356/166249441-8b08416b-28e9-4bb7-8c43-15878448dc82.png)


 
Sequential Logic Optimisations(lab):
In these lab sessions we looked at sequential optimisation techniques, all the file names were along dff_const
•	In the dff_const1 file we analysed the timing graphs to conclude that it cannot be treated as a sequential constant. So we look for the synthesis tool output to support our conclusions.
 
 ![image](https://user-images.githubusercontent.com/67062356/166249489-1af88039-2dcd-495a-aa05-39cba404cd68.png)

![image](https://user-images.githubusercontent.com/67062356/166249534-26e5940a-1f09-4c21-b144-41c60e2921ae.png)

 
•	As visible in the GTKWave output, this circuit cannot be treated as a sequential constant
•	And that is confirmed by the yosys dot viewer output

•	On the other hand we see that dff_const can be interpreted as a sequential constant
•	This is also confirmed by the simulation and synthesis output 
  
  ![image](https://user-images.githubusercontent.com/67062356/166249574-8ac7ece9-88b7-4946-ac5a-65a868cd41b3.png)
![image](https://user-images.githubusercontent.com/67062356/166249623-8b0066f5-3eb5-4d83-867d-c189fb60b728.png)

![image](https://user-images.githubusercontent.com/67062356/166249663-da8d7579-2ba4-4e05-a315-87b2c0bae059.png)

In the next example dff_const3 we see that none of the flops are sequential constants and that is confirmed by the simulation and synthesis outputs
 
 ![image](https://user-images.githubusercontent.com/67062356/166249685-158bdde0-5c81-4e94-913e-191904f23147.png)
 
 ![image](https://user-images.githubusercontent.com/67062356/166249708-0a65842b-d007-4629-bae5-de985ae80af2.png)


 
In the similar fashion we executed dff_const4 and dff_const5 in which the former resulted in a sequential constant whereas the latter led to synthesis of dffs
 
 ![image](https://user-images.githubusercontent.com/67062356/166249727-b22b8198-af2f-43f8-9a1a-05b03ed174f9.png)

 ![image](https://user-images.githubusercontent.com/67062356/166249745-0dd67f8d-bb2d-4196-be90-51dba7b80f9f.png)
 
 ![image](https://user-images.githubusercontent.com/67062356/166249765-d0c297d0-6493-4cc5-9ad7-64fdd6ae5578.png)

![image](https://user-images.githubusercontent.com/67062356/166249781-8c3a20b5-c94e-4e47-aebc-820209b5cf17.png)

 

•	Next we saw unused outputs optimisation in which if a particular output is not useful in the code its optimised we use count_opt in the simulation and synthesis
 
 
 ![image](https://user-images.githubusercontent.com/67062356/166249805-24bb7329-1144-491e-bc4e-8504271bc2f9.png)


Without hierarchial design: 

![image](https://user-images.githubusercontent.com/67062356/166249830-0e23c478-8753-4272-84f8-59f73dbd3823.png)


This completes Day 3

## Day 4:
Day 4 was titled ‘GLS blocking vs non blocking and synthesis-simulation’
The topics which we were introduced to were
•	GLS Synthesis-Simulation mismatch and blocking-non blocking statements(theory)
•	GLS and synthesis simulation mismatch(lab)
•	Synth-sim mismatch for blocking statement(lab)

### Gate Level Simulation
GLS stands for Gate Level Simulation. We have been doing the simulation and verification of our rtl design. GLS helps us perform verification and simulation of our synthesized design.
GLS is a very useful tool as it helps us fix design errors quite early .

![image](https://user-images.githubusercontent.com/67062356/166250052-5f1baa34-bdc7-46b8-aeba-80cf25891332.png)


Synthesis - Simulation mismatch arises due to the following reasons:
•	Missing sensitivity list

![image](https://user-images.githubusercontent.com/67062356/166250081-47d33d46-ac3e-4579-944e-856017467d24.png)

 
•	Blocking vs Non-blocking assignments

![image](https://user-images.githubusercontent.com/67062356/166250126-ad675587-87c0-4940-b951-9a2864e2ba1f.png)

 
•	Non standard verilog coding
•	The first example bad_mux.v shows us an example of missing sensitivity list:
 
 
 ![image](https://user-images.githubusercontent.com/67062356/166250157-93b9f9f4-2e4a-4ecc-a098-ec2016372835.png)


•	The second example bad_mux.v shows us an example of missing sensitivity list:

![image](https://user-images.githubusercontent.com/67062356/166250193-31f9e64f-e1ff-48e5-bd67-33567d480fe4.png)

   
We see the rtl and netlist simulations(GLS) not matching, this is a case of synthesis simulation mismatch.

Next we look at blocking vs non blocking assignments in Verilog:

![image](https://user-images.githubusercontent.com/67062356/166250231-7d3047d7-f7aa-4fbf-b92f-116d29eee0f9.png)

 
Blocking vs Non-blocking assignments also cause simulation-synthesis mismatch. These assignment statements are used in 'always' blocks and special care needs to be take when using them. The main reason to use either Blocking or Nonblocking assignments is to generate either combinational or sequential logic
Now we see a synthesis simulation mismatch due to use of blocking statements in the code blocking_caveats.v

![image](https://user-images.githubusercontent.com/67062356/166250284-ee3ba7e2-f7e2-45e8-ac96-130cf74bc5d1.png)

  
This concluded day 4

## Day 5:
Day 5 was titled ‘if case for loop and for generate’
The topics which we were introduced to were
•	If case constructs(theory)
•	Incomplete if case(lab)
•	Incomplete overlapping case(lab)
•	For loop and for generate(theory)
•	for loop” and “for generate(lab)

### If case constructs
•	Procedural if statement
•	if statement is equivalent to using a continuous assignment with a conditional operator,
•	assign out = (condition) ? a : b;
•	However, the procedural if provides new ways to make mistakes.
•	If output is not assigned for all inputs a latch is inferred
•	We visualize the outputs obtained for the incomp_if1 with the inferred latch behaviour
  
  ![image](https://user-images.githubusercontent.com/67062356/166250546-4b981298-d0b5-45a0-bf4f-69a3abbe8a6d.png)
  
  ![image](https://user-images.githubusercontent.com/67062356/166250578-10a25597-cbb8-404e-a5a9-9b3ae8f466be.png)


•	Next we see that in incomp_if2 logic the enable to the latch inferred is some combinational logic of i1 & i2
•	Again this is a case of incomplete if construct
  
  ![image](https://user-images.githubusercontent.com/67062356/166250609-9687fbe6-2544-4a3d-97c4-db13040fafc1.png)
![image](https://user-images.githubusercontent.com/67062356/166250630-506c04f4-f8d0-42a3-84af-7a0c76fbf69b.png)



### Incomplete overlapping case:
•	Case statements in Verilog are nearly equivalent to a sequence of if-elseif-else that compares one expression to a list of others. Case statements are more convenient than if statements if there are a large number of cases.
•	Case statements have no hierarchy unlike if statements
•	Case statements too infer latches if the assignment is incomplete for different cases
•	Default statements do not male sure that we wont get any inferred latches
•	The first case which we compare is incomp_case we see an inferred latch in the output:
   
   ![image](https://user-images.githubusercontent.com/67062356/166250684-465097a3-fae5-4d8b-a1dc-46f206ac262f.png)
![image](https://user-images.githubusercontent.com/67062356/166250703-b111880c-f680-43ff-84a7-9097dcddc720.png)


•	Next we see the logic of comp_case without any inferred latches:
  
  ![image](https://user-images.githubusercontent.com/67062356/166250721-87d57bd6-f556-4d23-aa05-7a33a360d887.png)

![image](https://user-images.githubusercontent.com/67062356/166250742-88902cc6-ba48-4009-ac4c-3edc910a6fb9.png)


•	We see that in case of partial assignment too latches are inferred if we are not careful
  
  ![image](https://user-images.githubusercontent.com/67062356/166250764-f6844015-df22-4c2f-b9a9-9e4dc6ff6a87.png)
  ![image](https://user-images.githubusercontent.com/67062356/166250808-411b851e-97bf-4205-9aa4-8a91e6512dc7.png)


•	Next we see what bad coding style does to a synthesis and simulation mismatch:
•	We use bad_case.v
•	We see the inferred design, the rtl output and the netlist output:

![image](https://user-images.githubusercontent.com/67062356/166250847-2a0a5bec-87ab-45b6-b147-558542b0ca43.png)
![image](https://user-images.githubusercontent.com/67062356/166250862-34a73f77-9973-4426-8e67-96fac1a3b518.png)
![image](https://user-images.githubusercontent.com/67062356/166250883-15216e6c-3dd2-4a52-9751-60698ca8d031.png)


   
### For loop and for generate:
•	Now we the difference between for loop and for generate loop:
•	For loop is used for evaluation of hardware within an always block
•	For generate loop is used outside an always block for multiple instantiation of a component or module
 
 ![image](https://user-images.githubusercontent.com/67062356/166250924-fdb03be2-6d25-4f79-b5aa-781e537618d2.png)

![image](https://user-images.githubusercontent.com/67062356/166250949-c55a7c91-a85f-42d0-b9dc-61b3a71b75c5.png)

 

•	We see the usage of for loop in the demux output and compare it with the case output:
  
  
  ![image](https://user-images.githubusercontent.com/67062356/166250980-8aa2f5ce-bd9e-440b-bdc7-d6792ebfd892.png)
![image](https://user-images.githubusercontent.com/67062356/166251030-cb1869a6-99d3-4062-8206-7077ab50c329.png)


•	We see the usage of for loop in mux output:  

![image](https://user-images.githubusercontent.com/67062356/166251056-b4ae88a3-398a-4815-aac9-64ade90f0736.png)


•	Finally we see the usage of ripple carry adder in the for generate output:
   ![image](https://user-images.githubusercontent.com/67062356/166251088-37f027a9-8ff8-4d51-881c-0d9cf92eaffa.png)
![image](https://user-images.githubusercontent.com/67062356/166251108-59a89991-a7ed-422c-ab11-0663e4747332.png)

![image](https://user-images.githubusercontent.com/67062356/166251120-6a5adeaf-64e2-44ad-a974-1ac96a208719.png)


•	This concludes Day 5 and the workshop





