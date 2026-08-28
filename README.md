# Custom-RISC-V-SoC-with-INT8-Matrix-Accelerator

A synthesizable System-on-Chip (SoC) targeting AMD Artix-7 FPGAs (Nexys-A7), integrating a 32-bit RISC-V CPU core with a custom AXI4-Lite interconnect, memory-mapped peripherals, and a dedicated INT8 Multiply-Accumulate (MAC) matrix acceleration engine.

## Key Subsystems

* **CPU Core:** Integrated 32-bit RV32I core (PicoRV32 for baseline bring-up, migrating to lowRISC Ibex pipelined core).


* **Interconnect:** Custom synthesizable AXI4-Lite bus matrix implementing full 5-channel transaction handshaking (`AR`, `R`, `AW`, `W`, `B`), address decoding, and peripheral routing.


* **INT8 MAC Accelerator:** Dedicated hardware datapath featuring an array of INT8 signed multipliers, 32-bit accumulators, hardware ReLU activation, and fixed-point quantization scaling.


* **Memory & Peripherals:** Dual-port Block RAM (BRAM) controller for instruction/data tightly coupled memory, memory-mapped UART for terminal interaction, and hardware performance counters.


* **Software Stack:** Bare-metal C runtime compiled with `riscv32-unknown-elf-gcc`, utilizing memory-mapped register pointers for hardware control.

---

## Verification & Toolchain

* **Simulation & Verification:** `cocotb` (Python-based testbenches) combined with Verilator and Icarus Verilog.


* **Golden Reference Model:** Cycle-accurate bit-level verification against a Python/NumPy matrix multiplication and quantization model.


* **Synthesis & Implementation:** AMD Vivado Design Suite targeting the Digilent Nexys-A7 (XC7A100T).


* **Software Toolchain:** GNU RISC-V Embedded GCC Toolchain (`riscv32-unknown-elf-gcc`).

---

## Directory Structure

```
├── doc/                 # Architecture specifications, diagrams, register maps
├── fpga/                # Vivado project scripts, constraints (.xdc), top-level wrappers
├── rtl/                 # Synthesizable SystemVerilog/Verilog source files
│   ├── core/            # RISC-V CPU core and wrapper logic
│   ├── bus/             # AXI4-Lite crossbar, arbiters, decoders
│   ├── accelerator/     # INT8 MAC array, accumulators, quantization units
│   └── peripherals/     # BRAM controller, UART controller, timer
├── sim/                 # cocotb testbenches, Python golden models, Makefiles
└── sw/                  # Bare-metal C test programs, linker scripts, startup code
    ├── drivers/         # Peripheral driver headers (UART, MAC MMIO)
    └── tests/           # Functional tests and matrix multiplication benchmarks

```

---

## Development Milestones

* [x] Top-level SoC architecture specification and AXI bus mapping.
* [ ] **Phase 1:** PicoRV32 integration, basic BRAM controller, and `cocotb` instruction execution tests.


* [ ] **Phase 2:** AXI4-Lite interconnect implementation, address decoder verification, and UART peripheral bring-up.


* [ ] **Phase 3:** INT8 MAC datapath design, fixed-point quantization block, and NumPy golden model validation.


* [ ] **Phase 4:** Bare-metal C driver integration, matrix offload benchmarks, and Nexys-A7 hardware validation.


* [ ] **Phase 5:** Migration from PicoRV32 to lowRISC Ibex pipelined core and timing closure profiling.
