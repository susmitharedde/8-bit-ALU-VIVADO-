#codemodule bit_alu(
    input [7:0] A,
    input [7:0] B,
    input [2:0] opcode,
    output reg [7:0] result,
    output reg carry
);

always @(*) begin
    carry = 0;

    case(opcode)

        3'b000: begin
            {carry, result} = A + B;
        end

        3'b001: begin
            {carry, result} = A - B;
        end

        3'b010: begin
            result = A & B;
        end

        3'b011: begin
            result = A | B;
        end

        3'b100: begin
            result = A ^ B;
        end

        3'b101: begin
            result = ~A;
        end

        3'b110: begin
            result = A << 1;
        end

        3'b111: begin
            result = A >> 1;
        end

        default: begin
            result = 8'b00000000;
        end

    endcase
end

endmodule

#TESTBENCH

`timescale 1ns / 1ps

module bit_alu_tb;

reg [7:0] A, B;
reg [2:0] opcode;

wire [7:0] result;
wire carry;

bit_alu uut (
    .A(A),
    .B(B),
    .opcode(opcode),
    .result(result),
    .carry(carry)
);

initial begin

    A = 8'b00001111;
    B = 8'b00000011;

    opcode = 3'b000; #10;
    opcode = 3'b001; #10;
    opcode = 3'b010; #10;
    opcode = 3'b011; #10;
    opcode = 3'b100; #10;
    opcode = 3'b101; #10;
    opcode = 3'b110; #10;
    opcode = 3'b111; #10;

    $finish;

end

endmodule