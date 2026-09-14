# RTL-to-GDSII of Wishbone Quad-SPI Flash Controller (wbqspiflash)

## Overview
This project implements a complete digital ASIC physical design flow, taking the open-source **wbqspiflash** RTL core from Verilog RTL to a fabrication-ready GDSII layout. The core is a **Wishbone-bus-controlled Quad SPI (QSPI) Flash Controller**, originally developed by Dan Gisselquist (ZipCPU), which allows a CPU on a Wishbone-based SoC to read, write, and erase an external QSPI flash memory chip through simple Wishbone bus transactions.

The physical design flow was carried out using the open-source **OpenROAD / OpenLane** toolchain, targeting the **SkyWater Sky130 (130nm)** process design kit (PDK).

## About the Design
`wbqspiflash` bridges a Wishbone bus interface to an external QSPI flash device. It implements an internal state machine that handles low-level QSPI protocol operations — including read ID, read/write status, write enable, page programming, quad programming, and sector/block erase — while exposing standard Wishbone signals to the SoC and QSPI pins to the flash chip.

**Key I/O:**
- Wishbone side: `i_wb_cyc`, `i_wb_stb`, `i_wb_we`, `i_wb_addr`, `i_wb_data`, `o_wb_ack`, `o_wb_stall`, `o_wb_data`
- QSPI side: `o_qspi_sck`, `o_qspi_cs_n`, `o_qspi_mod`, `o_qspi_dat`, `i_qspi_dat`

## Toolchain & Technology
- **RTL Source:** Verilog (`wbqspiflash.v`, ZipCPU/qspiflash repository)
- **Synthesis:** Yosys
- **Physical Design:** OpenROAD (via OpenLane automated flow)
- **DRC / LVS:** Magic, Netgen
- **PDK:** SkyWater Sky130A

## Flow Stages
1. RTL Synthesis
2. Floorplanning & Power Planning
3. Placement
4. Clock Tree Synthesis (CTS)
5. Routing (Global + Detailed)
6. Static Timing Analysis (STA)
7. Design Rule Check (DRC)
8. Layout vs. Schematic (LVS)
9. GDSII Generation

## Outcome
Successfully generated a signed-off GDSII layout for the `wbqspiflash` core, verified for timing closure, DRC cleanliness, and LVS correctness, demonstrating a complete open-source RTL-to-GDSII ASIC implementation flow on the Sky130 process.

## References
- ZipCPU/qspiflash: https://github.com/ZipCPU/qspiflash
- OpenLane: https://github.com/The-OpenROAD-Project/OpenLane
- SkyWater Sky130 PDK: https://github.com/google/skywater-pdk
