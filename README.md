# RTL-design-using-Verilog-with-SKY130-Technology
a Workshop by Kunal Ghosh and VSDIAT
## Day 1:
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

