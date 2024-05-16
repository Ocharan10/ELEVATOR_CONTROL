# ELEVATOR_CONTROL
# AIM
To design and simulate elevator control using vivado.
# Apparatus Required:
Pc with vivado software.
# PROCEDURE:
STEP:1 Start the Xilinx navigator, Select and Name the New project.

STEP:2 Select the device family, device, package and speed.

STEP:3 Select new source in the New Project and select Verilog Module as the Source type.

STEP:4 Type the File Name and Click Next and then finish button. Type the code and save it.

STEP:5 Select the Behavioral Simulation in the Source Window and click the check syntax.

STEP:6 Click the simulation to simulate the program and give the inputs and verify the outputs as per the truth table.

STEP:7 Select the Implementation in the Sources Window and select the required file in the Processes Window.

STEP:8 Select Check Syntax from the Synthesize XST Process. Double Click in the FloorplanArea/IO/Logic-Post Synthesis process in the User Constraints process group. UCF(User constraint File) is obtained.

STEP:9 In the Design Object List Window, enter the pin location for each pin in the Loc column Select save from the File menu.

STEP:10 Double click on the Implement Design and double click on the Generate Programming File to create a bitstream of the design.(.v) file is converted into .bit file here.

STEP:11 On the board, by giving required input, the LEDs starts to glow light, indicating the output.
# STATE DIAGRAM:
![image](https://github.com/RESMIRNAIR/ELEVATOR_CONTROL/assets/154305926/b42a1942-752f-4787-967c-b9c13ab3e763)
# VERILOG CODE:
module LiftC(clk,reset,req_floor,stop,door,Up,Down,y);

input clk,reset;

input [6:0] req_floor;
output reg[1:0] door;
output reg[1:0] Up;
output reg[1:0] Down;
output reg[1:0] stop;

output [6:0] y;
reg [6:0] cf ;

always @ (posedge clk)
begin

if(reset)
begin
cf=6'd0;
stop=6'd1;
door = 1'd1;
Up=1'd0;
Down=1'd0;
end
else
begin
if(req_floor < 6'd61)
begin

if(req_floor < cf )
begin
cf=cf-1;
door=1'd0;
stop=6'd0;
Up=1'd0;
Down=1'd1;
end


else if (req_floor > cf)
begin
cf = cf+1;
door=1'd0;
stop=6'd0;
Up=1'd1;
Down=1'd0;
end

else if(req_floor == cf )
begin
cf = req_floor;
door=1'd1;
stop=6'd1;
Up=1'd0;
Down=1'd0;
end
end


end


end


assign y = cf;

endmodule
# OUTPUT:
![image](https://github.com/RESMIRNAIR/ELEVATOR_CONTROL/assets/154305926/6379ab0d-b73f-4740-bdda-45263b28f120)
# RESULT:
Hence Elevator control is verified.
