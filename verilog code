// Verilog Design Code
//single port RAM

module single_port_ram(
input [7:0] data, input [5:0] addr, input clk, input we, output reg [7:0] dout
);
reg [7:0] mem[63:0];
always @(posedge clk) begin
if (we)
mem[addr] <= data;
else
dout <= mem[addr];
end
endmodule

//dual port RAM

module dual_port_ram(
input [7:0] data_a, data_b, input [5:0] addr_a, addr_b, input we_a, we_b, clk, output reg [7:0] q_a, q_b
);
reg [7:0] mem[63:0];
always @(posedge clk) begin
if (we_a)
mem[addr_a] <= data_a;
else
q_a <= mem[addr_a];
end
always @(posedge clk) begin
if (we_b)
mem[addr_b] <= data_b;
else
q_b <= mem[addr_b];
end
endmodule

//ROM

module rom (
input [5:0] addr, // 6-bit address (64 locations)
output reg [7:0] data // 8-bit data output
);
reg [7:0] mem[63:0]; // ROM memory with 64 locations of 8 bits each
initial begin
// Preload ROM with data
mem[0] = 8'hAA;
mem[1] = 8'hBB;
mem[2] = 8'hCC;
mem[3] = 8'hDD;
mem[4] = 8'hEE;
mem[5] = 8'hFF;
// Initialize other locations as needed
end
always @(*) begin
data = mem[addr]; // Continuous read operation
end
endmodule

//Test Bench Code
//single port RAM tb

module single_port_ramtb;
reg [7:0] data;
reg [5:0] addr;
reg we, clk;
wire [7:0] dout;
single_port_ram spr1(.data(data), .addr(addr), .we(we), .clk(clk), .dout(dout));
initial begin
$dumpfile("dump.vcd");
$dumpvars(1, single_port_ramtb);
clk = 1'b1;
forever #5 clk = ~clk;
end
initial begin
data = 8'h01; addr = 5'd0; we = 1'b1; #10;
data = 8'h02; addr = 5'd1; #10;
data = 8'h03; addr = 5'd2; #10;
addr = 5'd0; we = 1'b0; #10;
addr = 5'd1; #10;

end
endmodule

//Dual port RAM tb
module dual_port_ram_tb;
reg [7:0] data_a, data_b;
reg [5:0] addr_a, addr_b;
reg we_a, we_b, clk;
wire [7:0] q_a, q_b;
dual_port_ram
uut(.data_a(data_a), .data_b(data_b), .addr_a(addr_a), .addr_b(addr_b), .we_a(we_a), .we_b(w
e_b), .clk(clk), .q_a(q_a), .q_b(q_b));
initial begin
$dumpfile("dump.vcd");
$dumpvars(1, dual_port_ram_tb);
clk = 1'b1;
forever #5 clk = ~clk;
end
initial begin
data_a = 8'h33; addr_a = 6'h01; data_b = 8'h44; addr_b = 6'h02; we_a = 1'b1; we_b = 1'b1;
#10;
data_a = 8'h55; addr_a = 6'h03; addr_b = 6'h01; we_b = 1'b0; #10;
addr_a = 6'h02; addr_b = 6'h03; we_a = 1'b0; #10;
end
endmodule

//ROM tb

module rom_tb;
reg [5:0] addr; // 6-bit address input
wire [7:0] data; // 8-bit data output
rom uut (
.addr(addr),
.data(data)
);
initial begin
$dumpfile("rom.vcd");
$dumpvars(1, rom_tb);
// Test cases
addr = 6'd0; #10; // Read from address 0
addr = 6'd1; #10; // Read from address 1
addr = 6'd2; #10; // Read from address 2
addr = 6'd3; #10; // Read from address 3
addr = 6'd4; #10; // Read from address 4
addr = 6'd5; #10; // Read from address 5
$finish;
end
endmodule
