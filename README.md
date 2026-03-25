# sequential-circuits
sequential circuits implimented in Verilog HDL

# SR Flip-Flop (Verilog) – Cadence Simulation

## 📌 Description
This project implements a synchronous SR Flip-Flop using Verilog HDL. The output changes only on the positive edge of the clock (clk). The design is simulated using Cadence Xcelium (xrun) and waveform is verified in SimVision.

## ⏱ Clock Behavior
- Edge-triggered flip-flop
- Output updates only at `posedge clk`
- Clock generated in testbench using:
```verilog
always #5 clk = ~clk;
```

## 📊 Truth Table (On posedge clk)

| clk | S | R | Q (Next State) |
|-----|---|---|----------------|
| ↑   | 0 | 0 | No Change      |
| ↑   | 0 | 1 | 0 (Reset)      |
| ↑   | 1 | 0 | 1 (Set)        |
| ↑   | 1 | 1 | Invalid        |

## 💻 Verilog Code
```verilog
module sr_ff (
    input S,
    input R,
    input Clk,
    output reg Q0,
    output reg Q1
);

always @(posedge clk) begin
    case ({S,R})
        2'b00: begin
            Q0 <= Q0;           // Hold
            Q1 <= Q1;
        end
        2'b01: begin
            Q0 <= 0;           // Reset
            Q1 <= 1;
        end
        2'b10: begin
            Q0 <= 1;           // Set
            Q1 <= 0;
        end
        2'b11: begin
            Q0 <= 1'bx;        // Invalid
            Q1 <= 1'bx;
        end
    endcase
end

endmodule
```

## 🧪 Testbench
```verilog
module sr_ff_tb;

reg S, R, clk;
wire Q0, Q1;

sr_ff uut (
    .S(S),
    .R(R),
    .clk(clk),
    .Q0(Q0),
    .Q1(Q1)
);

// Clock generation
always #5 clk = ~clk;

// Stimulus
initial begin
    clk = 0;

    #10 S=0; R=0;  // Hold
    #10 S=1; R=0;  // Set
    #10 S=0; R=1;  // Reset
    #10 S=1; R=1;  // Invalid

    #20 $finish;
end

endmodule
```

## 📷 Waveform Output

![Waveform](https://github.com/Varshitha-H-N/sequential-circuits/blob/main/Screenshot%202026-03-25%20124939.png)

## 🛠 Tools Used
- Cadence Xcelium (xrun)
- SimVision

## 📂 Files Included
- `sr_ff.v` → Design file
- `sr_ff_tb.v` → Testbench
- `https://github.com/Varshitha-H-N/sequential-circuits/blob/main/Screenshot%202026-03-25%20124939.png
` → Simulation output

## 🚀 Key Learning
- Synchronous sequential logic
- Clock-triggered behavior
- SR Flip-Flop operation
- Cadence simulation workflow
