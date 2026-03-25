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
    input clk,
    output reg Q,
    output reg Q_bar
);

always @(posedge clk) begin
    case ({S,R})
        2'b00: begin
            Q <= Q;           // Hold
            Q_bar <= Q_bar;
        end
        2'b01: begin
            Q <= 0;           // Reset
            Q_bar <= 1;
        end
        2'b10: begin
            Q <= 1;           // Set
            Q_bar <= 0;
        end
        2'b11: begin
            Q <= 1'bx;        // Invalid
            Q_bar <= 1'bx;
        end
    endcase
end

endmodule
```

## 🧪 Testbench
```verilog
module sr_ff_tb;

reg S, R, clk;
wire Q, Q_bar;

sr_ff uut (
    .S(S),
    .R(R),
    .clk(clk),
    .Q(Q),
    .Q_bar(Q_bar)
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
- `waveform.png` → Simulation output

## 🚀 Key Learning
- Synchronous sequential logic
- Clock-triggered behavior
- SR Flip-Flop operation
- Cadence simulation workflow
