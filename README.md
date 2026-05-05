#Design of a timer with alarm
1)module design
module timer (
    input clk,
    input reset,
    input enable,
    input [3:0] preset,
    output reg [3:0] count,
    output reg alarm
);

always @(posedge clk or posedge reset) begin
    if (reset) begin
        count <= 0;     // CHANGE 1
        alarm <= 0;
    end 
    else if (enable) begin
        if (count < preset) begin
            count <= count + 1;   // CHANGE 2
            alarm <= 0;
        end 
        else begin
            alarm <= 1;
        end
    end
end

endmodule
2)module testbench
module timer (
    input clk,
    input reset,
    input enable,
    input [3:0] preset,
    output reg [3:0] count,
    output reg alarm
);

always @(posedge clk or posedge reset) begin
    if (reset) begin
        count <= 0;     // CHANGE 1
        alarm <= 0;
    end 
    else if (enable) begin
        if (count < preset) begin
            count <= count + 1;   // CHANGE 2
            alarm <= 0;
        end 
        else begin
            alarm <= 1;
        end
    end
end

endmodule

#waveform
<img width="1280" height="720" alt="image" src="https://github.com/user-attachments/assets/18019213-fe9c-41fe-8428-450fd71a490c" />
