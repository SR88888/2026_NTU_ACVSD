# 2026 NTU ACVSD

Coursework from the 2026 **Advanced Computer-Aided VLSI System Design (ACVSD)** course at National Taiwan University. This repository includes lectures, labs, four homework assignments, and midterm and final projects, covering low-power design, clock domain crossing (CDC), buses, matrix accelerators, DFT, and physical design.

## Projects

| Assignment | Topic | Main resources |
| --- | --- | --- |
| HW1 | Lossy Bitmask Encoder with low-power design | [Specification](Homework/1/114-2_HW1.pdf), [submission](Homework/1/acvsd-16-hw1-v1.tar.gz) |
| HW2 | Rotation Invariant Local Binary Pattern | [Specification](Homework/2/114-2_HW2_v2.pdf), [submission](Homework/2/acvsd016-hw2-v3.tar.gz) |
| HW3 | Low Power Matrix Accelerator | [Project notes](Homework/3/114-2_HW3_note_v3.pdf), [submission](Homework/3/acvsd-16-hw3-v2.tar.gz) |
| HW4 | APR with scan-chain design and pad integration | [Specification](Homework/4/1142_HW4_v2.pdf), [report](Homework/4/b11901063_report.pdf) |
| Midterm | Vision Transformer Patch Embedding Accelerator | [Specification](Midterm/114-2_midterm_v1.pdf), [submission](Midterm/acvsd-16-midterm-v1.tar.gz) |
| Final | Multi-Core GEMM Accelerator | [Project slides](Final/114_2_final_slide_v6.pdf), [submission](Final/acvsd-hw-team5-final.tar.gz) |

## Submission Archive Contents

- **HW1**: `top.v`, the `core` module, an RTL file list, and `top.rtl.upf`.
- **HW2**: `LBP.v`, `CORE.v`, `AXI_r.v`, `AXI_w.v`, and `CDC.v`.
- **HW3**: `ALL` and `Ranking` design variants, including SIMD/GEMM cores, shared memory, an interconnect, a reset synchronizer, and UPF.
- **Midterm**: `vit_pe.v`, a compute core, AXI read/write modules, and synthesis/timing settings.
- **Final**: `top.sv`, `pe.sv`, `pe_config.sv`, `Router.sv`, `MAC.sv`, control and AXI checker files, and the project report.

Individual and team submission archives primarily contain designs and reports. Simulation requires the matching assignment environment, including its testbench, patterns, and memory models.

## Repository Layout

```text
.
├── Lecture/        # Low power, CDC, PLL, buses, NoC, DFT, APR, and signoff
├── Lab/
│   ├── 0/          # Workstation and ADFP environment
│   ├── 1/          # Low-power design
│   ├── 2/          # CDC and PLL
│   ├── 3/          # DFT and ATPG
│   ├── 4/          # APR (1)
│   ├── 5/          # APR (2)
│   ├── 6/          # Timing signoff
│   └── 7/          # Lab7 materials
├── Homework/1~4/    # Specifications, provided environments, submissions, and reports
├── Midterm/        # ViT Patch Embedding
└── Final/          # Multi-core GEMM
```

## Requirements

- A Linux/Unix shell and `tar`/`unzip`.
- Synopsys VCS and the required DesignWare models. Some flows require UPF/power-aware simulation support.
- Synopsys Design Compiler, Cadence Innovus, and the verification/signoff tools specified by each lab.
- Matching standard-cell and SRAM libraries. Some settings use N16 ADFP and paths such as `/usr/cad/...` and `/share1/...` on the course workstations.

Start with [Lab0](Lab/0), then check the tool environment and library settings for each assignment.

## Quick Start: HW2 RTL Simulation

Extract the provided environment and the submission into separate directories, then copy the submitted RTL and file list into the test environment:

```bash
git clone https://github.com/SR88888/2026_NTU_ACVSD.git
cd 2026_NTU_ACVSD

mkdir -p work/hw2
tar -xf Homework/2/1142_hw2_v2.tar -C work/hw2
tar -xzf Homework/2/acvsd016-hw2-v3.tar.gz -C work/hw2

cp work/hw2/b11901063_hw2/01_RTL/*.v work/hw2/1142_hw2/01_RTL/
cp work/hw2/b11901063_hw2/01_RTL/rtl_01.f work/hw2/1142_hw2/01_RTL/

cd work/hw2/1142_hw2/01_RTL
bash 01_run
```

`rtl_01.f` also references the AXI models and `testfixture.v` from the provided environment. Make sure the workstation's VCS environment is loaded before running the simulation.

## Exploring the Final Project

Run the following commands from the repository root:

```bash
mkdir -p work/final
tar -xzf Final/acvsd-hw-team5-final.tar.gz -C work/final
```

The design files and `report.pdf` are in `work/final/acvsd-hw-team5-final/`. The provided project environment is stored separately in [114-2-acvsd-final-v8.tgz](Final/114-2-acvsd-final-v8.tgz). Follow the [project slides](Final/114_2_final_slide_v6.pdf) to check interfaces, test procedures, and file lists when integrating the submission.

The HW3 submission also references `00_TB`, SRAM, and DesignWare from the assignment environment. Compare `ALL`/`Ranking` and other versions under the same test conditions, using the resulting simulation, power, area, and timing reports.
