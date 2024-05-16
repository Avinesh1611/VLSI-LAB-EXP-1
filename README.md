# SIMULATION AND IMPLEMENTATION OF LOGIC GATES,ADDERS AND SUBTRACTOR
## AIM: 
To simulate and synthesis Logic Gates,Adders and Subtractor using Xilinx ISE.

## APPARATUS REQUIRED: 
Xilinx 14.7 Spartan6 FPGA

## PROCEDURE: 
STEP:1 Start the Xilinx navigator, Select and Name the New project.         
STEP:2 Select the device family, device, package and speed.        
STEP:3 Select new source in the New Project and select Verilog Module as the Source type.        
STEP:4 Type the File Name and Click Next and then finish button. Type the code and save it.        
STEP:5 Select the Behavioral Simulation in the Source Window and click the check syntax.        
STEP:6 Click the simulation to simulate the program and give the inputs and verify the outputs as per the truth table.        
STEP:7 Select the Implementation in the Sources Window and select the required file in the Processes Window.        
STEP:8 Select Check Syntax from the Synthesize XST Process. Double Click in the Floorplan Area/IO/Logic-Post Synthesis process in the User Constraints process group. UCF(User constraint File) is obtained.        
STEP:9 In the Design Object List Window, enter the pin location for each pin in the Loc column Select save from the File menu.        
STEP:10 Double click on the Implement Design and double click on the Generate Programming File to create a bitstream of the design.(.v) file is converted into .bit file here.        
STEP:11 Load the Bit file into the SPARTAN 6 FPGA.       
STEP:12 On the board, by giving required input, the LEDs starts to glow light, indicating the output.       




## Logic Gates :
### Logic Diagram :
![image](https://github.com/navaneethans/VLSI-LAB-EXPERIMENTS/assets/6987778/ee17970c-3ac9-4603-881b-88e2825f41a4)

### Verilog code :
```
module logicgate (a,b,andgate,orgate,xorgate,nandgate,norgate,xnorgate,notgate);
input a,b;  
output andgate,orgate,xorgate,nandgate,norgate,xnorgate,notgate;
and(andgate,a,b);
or(orgate,a,b);
xor(xorgate,a,b);
nand(nandgate,a,b); 
nor(norgate,a,b);
xnor(xnorgate,a,b);
not(notgate,a);
endmodule
```

### Output Waveform :
![image](https://github.com/navaneethans/VLSI-LAB-EXP-1/assets/163638659/20eccc65-af15-47cb-b015-04d3f7114c8a)

## Half Adder :
### Logic Diagram :
![image](https://github.com/navaneethans/VLSI-LAB-EXPERIMENTS/assets/6987778/0e1ecb96-0c25-4556-832b-aeeedfdfe7b9)

### Verilog code :
```
module halfadder(a,b,sum,carry);
input a,b;
output sum,carry;
xor g1(sum,a,b);
and g2(carry,a,b);
endmodule
```

### Output Waveform :
![image](https://github.com/navaneethans/VLSI-LAB-EXP-1/assets/163638659/400309f5-fac8-4386-b342-c770161baa6e)

## Full adder :
### Logic Diagram :
![image](https://github.com/navaneethans/VLSI-LAB-EXPERIMENTS/assets/6987778/9bb3964c-438f-469d-a3de-c1cca6f323fb)

### Verilog code :
```
module fadd(a,b,c,sum,carry);
input a,b,c;
output sum,carry;
wire w1,w2,w3;
xor g1(w1,a,b);
and g2(w2,a,b);
xor g3(sum,w1,c);
and g4(w3,w1,c);
or g5(carry,w3,w2);
endmodule
```

### Output Waveform :
![image](https://github.com/navaneethans/VLSI-LAB-EXP-1/assets/163638659/ca305031-fcab-44af-a3b3-f5196b137ad0)

## Half Subtractor :
### Logic Diagram :
![image](https://github.com/navaneethans/VLSI-LAB-EXPERIMENTS/assets/6987778/731470b7-eb4e-49f8-8bb7-2994052a7184)

### Verilog code :
```
module halfsubtractor(a,b,diff,borrow);
input a,b;
output diff,borrow;
xor g1(diff,a,b);
and g2(borrow,~a,b);
endmodulemodule 
```
### Output Waveform :
![image](https://github.com/navaneethans/VLSI-LAB-EXP-1/assets/163638659/1aadaa77-6a4f-469e-a232-f56ac15994c5)

## Full Subtractor :
### Logic Diagram :
![image](https://github.com/navaneethans/VLSI-LAB-EXPERIMENTS/assets/6987778/d66f874b-c1f2-44b3-a035-7149b56430c1)

### Verilog code :
```
module fs(a,b,bin,d,bout);
input a,b,bin; 
output d,bout;
wire w1,w2,w3;
xor g1(w1,b,bin; 
xor g2(d,w1,a);
and g3(w2,a,~w1);
and g4(w3,~b,bin);
or g5(bout,w2,w3);
endmodule
```

### Output Waveform :
![image](https://github.com/navaneethans/VLSI-LAB-EXP-1/assets/163638659/193e48de-3971-41b2-84f9-349ce21146cf)

## 8 Bit Ripple Carry Adder :
### Logic Diagram :
![image](https://github.com/navaneethans/VLSI-LAB-EXPERIMENTS/assets/6987778/7385a408-40a5-4203-8050-b72818622d79)

### Verilog code :
```
module ripplemod(a, b, cin, sum, cout);
input [07:0] a;
input [07:0] b;
input cin;
output [7:0]sum;
output cout;
wire[6:0] c;
fulladd a1(a[0],b[0],cin,sum[0],c[0]);
fulladd a2(a[1],b[1],c[0],sum[1],c[1]);
fulladd a3(a[2],b[2],c[1],sum[2],c[2]);
fulladd a4(a[3],b[3],c[2],sum[3],c[3]);
fulladd a5(a[4],b[4],c[3],sum[4],c[4]);
fulladd a6(a[5],b[5],c[4],sum[5],c[5]);
fulladd a7(a[6],b[6],c[5],sum[6],c[6]);
fulladd a8(a[7],b[7],c[6],sum[7],cout);
endmodule
module fulladd(a, b, cin, sum, cout);
input a;
input b;
input cin;
output sum;
output cout;
assign sum=(a^b^cin);
assign cout=((a&b)|(b&cin)|(a&cin));
endmodule
```

### Output Waveform :
![image](https://github.com/navaneethans/VLSI-LAB-EXP-1/assets/163638659/9c8e0472-6b70-4b6f-a678-63862cb68523)

## Result :
Hence Logic Gates,Adders and Subtractor are simulated and synthesised using Xilinx ISE
