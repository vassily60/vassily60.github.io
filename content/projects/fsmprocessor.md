---
title: "A Simple Processor in Verilog"
description: "A small Verilog processor that loads, moves, adds, and subtracts 8 bit values."
weight: 20
cover:
  image: "/images/processorimage.jpg"
---

<br>

# A tiny processor, one step at a time

A processor can seem like a mysterious box that turns instructions into results. For a small project, we can just consider some parts of it, and break it into a few simple pieces.

I wrote a small processor in Verilog. It has four 8 bit registers, a shared 8 bit bus, and arithmetic logic for adding or subtracting. Inside the code, the processor is more like a little control room where each piece does its work one step at a time.

<br>

## The control room: an FSM

The processor uses a finite state machine (FSM) to decide what to do next. It is a little bit like a manager following a checklist: wait for a job, collect the instruction, understand it, do the work, and signal that the step is complete.

Here are the states from my code:

```verilog
parameter [2:0] S_IDLE   = 3'b000,
                S_FETCH  = 3'b001,
                S_DECODE = 3'b010,
                S_EXEC   = 3'b011,
                S_WRITE  = 3'b100;
```

In simple words, here is what each state does:

- **Idle:** wait for the `w` signal to say an instruction is ready.
- **Fetch:** save the instruction fields (`F`, `Rx`, and `Ry`).
- **Decode:** identify which operation and registers were selected.
- **Execute:** choose control signals and perform the operation.
- **Write:** raise `Done` to show that this pass is finished, then return to idle.

The drawing below is a map I drew representing that sequence and the operation paths.

![Hand-drawn FSM diagram showing the processor's standby, fetch, decode, and operation states.](/images/fsmprocessor.png)

<br>

## The kitchen analogy

The four registers (`R0` through `R3`) are like labeled storage bins. The shared bus is the countertop: only one bin should put its value on the countertop at a time, and another part can take that value from there.

The ALU is the calculator on the countertop (a little bit like kitchen utensils manipulating ingredients). For addition and subtraction, it uses the value saved in `A` and the value currently on the bus:

```verilog
OP_ADD: G <= A + BusWires;
OP_SUB: G <= A - BusWires;
```

`G` holds the answer until the write state puts it back into the destination register.

<br>

## The instructions

The two-bit `F` field selects one of four simple instructions:

- `00`: load the input `Data` into `Rx`.
- `01`: move the value in `Ry` into `Rx`.
- `10`: add `Rx` and `Ry`, saving the answer in `Rx`.
- `11`: subtract `Ry` from `Rx`, saving the answer in `Rx`.

The complete processor is below. The FSM is the checklist, and the registers, bus, and ALU are the workshop tools it coordinates.

<br>

## Complete Verilog code

```verilog
`timescale 1ns / 1ps

module proc (Data, Resetn, w, Clock, F, Rx, Ry, Done, BusWires);
    input [7:0] Data;
    input Resetn, w, Clock;
    input [1:0] F, Rx, Ry;
    output wire Done;
    output reg [7:0] BusWires;

    localparam [2:0] S_IDLE   = 3'b000,
                     S_FETCH  = 3'b001,
                     S_DECODE = 3'b010,
                     S_EXEC   = 3'b011,
                     S_WRITE  = 3'b100;

    localparam [1:0] OP_LOAD = 2'b00,
                     OP_MOVE = 2'b01,
                     OP_ADD  = 2'b10,
                     OP_SUB  = 2'b11;

    reg [2:0] state;
    reg [1:0] opcode, destination, source;
    reg [7:0] immediate, A, G;
    reg [7:0] registers [0:3];
    integer i;

    assign Done = (state == S_WRITE);

    always @(*) begin
        BusWires = 8'b0;

        case (state)
            S_EXEC: begin
                if (opcode == OP_LOAD)
                    BusWires = immediate;
                else
                    BusWires = registers[source];
            end
            S_WRITE: BusWires = G;
            default: BusWires = 8'b0;
        endcase
    end

    always @(posedge Clock or negedge Resetn) begin
        if (!Resetn) begin
            state       <= S_IDLE;
            opcode      <= OP_LOAD;
            destination <= 2'b00;
            source      <= 2'b00;
            immediate   <= 8'b0;
            A           <= 8'b0;
            G           <= 8'b0;

            for (i = 0; i < 4; i = i + 1)
                registers[i] <= 8'b0;
        end else begin
            case (state)
                S_IDLE: begin
                    if (w)
                        state <= S_FETCH;
                end

                S_FETCH: begin
                    opcode      <= F;
                    destination <= Rx;
                    source      <= Ry;
                    immediate   <= Data;
                    state       <= S_DECODE;
                end

                S_DECODE: begin
                    if ((opcode == OP_ADD) || (opcode == OP_SUB))
                        A <= registers[destination];
                    state <= S_EXEC;
                end

                S_EXEC: begin
                    case (opcode)
                        OP_LOAD: G <= BusWires;
                        OP_MOVE: G <= BusWires;
                        OP_ADD:  G <= A + BusWires;
                        OP_SUB:  G <= A - BusWires;
                        default: G <= 8'b0;
                    endcase
                    state <= S_WRITE;
                end

                S_WRITE: begin
                    registers[destination] <= BusWires;
                    state <= S_IDLE;
                end

                default: state <= S_IDLE;
            endcase
        end
    end
endmodule

```
