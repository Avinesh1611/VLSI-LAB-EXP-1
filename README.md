# SIMULATION AND IMPLEMENTATION OF LOGIC GATES,ADDERS AND SUBTRACTOR
## AIM:
To simulate and synthesis Logic Gates,Adders and Subtractor using Xilinx ISE.

## APPARATUS REQUIRED: 
Xilinx 14.7 Spartan6 FPGA

## PROCEDURE: 
STEP:1 Start the Xilinx navigator, Select and Name the New project. 
STEP:2 Select the device family, device, package and speed. 
STEP:3 Select new source in the New Project and select Verilog Module as the Source type. STEP:4 Type the File Name and Click Next and then finish button. Type the code and save it. STEP:5 Select the Behavioral Simulation in the Source Window and click the check syntax. STEP:6 Click the simulation to simulate the program and give the inputs and verify the outputs as per the truth table. 
STEP:7 Select the Implementation in the Sources Window and select the required file in the Processes Window. 
STEP:8 Select Check Syntax from the Synthesize XST Process. Double Click in the Floorplan Area/IO/Logic-Post Synthesis process in the User Constraints process group. UCF(User constraint File) is obtained. 
STEP:9 In the Design Object List Window, enter the pin location for each pin in the Loc column Select save from the File menu. 
STEP:10 Double click on the Implement Design and double click on the Generate Programming File to create a bitstream of the design.(.v) file is converted into .bit file here. STEP:11 Load the Bit file into the SPARTAN 6 FPGA 
STEP:12 On the board, by giving required input, the LEDs starts to glow light, indicating the output.

## Logic Gates :

### Logic Diagram :
![image](https://github.com/navaneethans/VLSI-LAB-EXP-1/assets/161815461/c1749a3f-2291-42f6-ba1e-7ae359466b37)

### Verilog code :
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

### Output Waveform :
![image](https://github.com/navaneethans/VLSI-LAB-EXP-1/assets/161815461/35b1d0f1-2d8b-4473-ae0d-8eb5d7cda8c3)

## Half Adder :

### Logic Diagram :
![image](https://github.com/navaneethans/VLSI-LAB-EXP-1/assets/161815461/c21b16a8-a862-452b-b7d4-7d8e3721928c)

### Verilog code :
module halfadder(a,b,sum,carry);
input a,b;
output sum,carry;
xor g1(sum,a,b);
and g2(carry,a,b);
endmodule

### Output Waveform :
![image](https://github.com/navaneethans/VLSI-LAB-EXP-1/assets/161815461/af9b57ff-3d14-49b3-8b74-85e6d2c38a62)

## Full  Adder :

### Logic Diagram :
![image](https://github.com/navaneethans/VLSI-LAB-EXP-1/assets/161815461/fdd184bf-7fab-40b7-a98a-d1462418fd0d)


### Verilog code :
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

### Output Waveform :
![image](https://github.com/navaneethans/VLSI-LAB-EXP-1/assets/161815461/c72dc938-acb8-4a2d-bcff-f18a0cc51016)

## Half Subtractor :

### Logic Diagram :
![image](https://github.com/navaneethans/VLSI-LAB-EXP-1/assets/161815461/5e1db944-6953-403d-a238-a493c130b24a)

### Verilog code :
module halfsubtractor(a,b,diff,borrow);
input a,b;
output diff,borrow;
xor g1(diff,a,b);
and g2(borrow,~a,b);
endmodulemodule 

### Output Waveform :
![image](https://github.com/navaneethans/VLSI-LAB-EXP-1/assets/161815461/fc791a96-5f03-4f0f-8298-23020cfe1984)

## Full Subtractor :

### Logic Diagram :
![image](https://github.com/navaneethans/VLSI-LAB-EXP-1/assets/161815461/ae1ebdbe-ce70-4a6c-b645-4306fcac488b)

### Verilog code :
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

### Output Waveform :
![image](https://github.com/navaneethans/VLSI-LAB-EXP-1/assets/161815461/3e71d00d-edfa-4cf3-b7a6-cf82bcba35d5)

## 8 Bit Ripple Carry Adder :

### Logic Diagram :
![image](https://github.com/navaneethans/VLSI-LAB-EXP-1/assets/161815461/17a44724-441d-4005-b115-b1e44da516e9)


### Verilog code :
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

### Output Waveform :
![image](https://github.com/navaneethans/VLSI-LAB-EXP-1/assets/161815461/eee5995a-faa4-4fc2-8e3e-ec622a935a98)

## Result:

Hence Logic Gates,Adders and Subtractor are simulated and synthesised using Xilinx ISE
