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

2)Testbench

`timescale 1ns/1ps
module timer_tb;
reg clk;
reg reset;
reg enable;
reg [3:0] preset;
wire [3:0] count;
wire alarm;

timer uut (
    .clk(clk),
    .reset(reset),
    .enable(enable),
    .preset(preset),
    .count(count),
    .alarm(alarm)
);


always #5 clk = ~clk;

initial begin
    // Initialize
    clk = 0;
    reset = 1;
    enable = 0;
    preset = 4'd5;   // target value

    // Apply reset
    #10 reset = 0;
    enable = 1;

    // Let it run
    #100;

    $stop;
end
initial begin
    $monitor("Time=%0t | Count=%d | Alarm=%b", $time, count, alarm);
end
endmodule


#waveform 
<img width="1280" height="720" alt="image" src="https://github.com/user-attachments/assets/11f67370-8416-4ffa-9229-3417fd34f0b5" />
<img width="1280" height="720" alt="image" src="https://github.com/user-attachments/assets/18019213-fe9c-41fe-8428-450fd71a490c" />
