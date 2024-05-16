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
module elevator_control(
    input clk,            // Clock input
    input reset,          // Reset input
    input up_button,      // Up button input
    input down_button,    // Down button input
    input [3:0] current_floor,  // Current floor input (4 floors in total)
    output reg [3:0] next_floor // Next floor output
);

// Define states for the elevator controller
parameter IDLE = 2'b00;
parameter MOVE_UP = 2'b01;
parameter MOVE_DOWN = 2'b10;

reg [1:0] state;    // State register

always @(posedge clk or posedge reset) begin
    if (reset) begin
        state <= IDLE;
        next_floor <= 4'b0000;  // Initial floor
    end
    else begin
        case (state)
            IDLE: begin
                if (up_button && current_floor < 4'b0111) begin
                    state <= MOVE_UP;
                    next_floor <= current_floor + 1;
                end
                else if (down_button && current_floor > 4'b0000) begin
                    state <= MOVE_DOWN;
                    next_floor <= current_floor - 1;
                end
            end
            MOVE_UP: begin
                if (current_floor < 4'b0111)
                    next_floor <= next_floor + 1;
                else
                    state <= IDLE;
            end
            MOVE_DOWN: begin
                if (current_floor > 4'b0000)
                    next_floor <= next_floor - 1;
                else
                    state <= IDLE;
            end
            default: state <= IDLE;
        endcase
    end
end

endmodule

# OUTPUT:
![image](https://github.com/RESMIRNAIR/ELEVATOR_CONTROL/assets/154305926/6379ab0d-b73f-4740-bdda-45263b28f120)
# RESULT:
Hence Elevator control is verified.
