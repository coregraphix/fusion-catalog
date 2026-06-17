# Fusion Demos for Nano25

Try Fusion graphics on the Coregraphix DE25-Nano evaluation board
(Altera Agilex 5 SoC).

## Hardware context

The Nano25 is an FPGA SoC: it has both an **FPGA fabric** (where the
Fusion GPU is implemented as custom RTL) and an **ARM HPS** (where
Linux + Fusion userspace run). Both must carry Fusion-specific
content for any demo to run.

For the vendor's hardware documentation, see
[`vendor/`](vendor/). Of particular interest:

- `DE25_Nano_Getting_Started_Guide.pdf` — board overview, Quartus
  install, MSEL switches, MicroSD boot
- `DE25-Nano_User_manual_revB.pdf` — full pin/peripheral reference
- `DE25_Nano_Demonstration_Manual.pdf` — vendor demos
- `DE25-Nano_My_First_FPGA.pdf` — first-time FPGA tutorial

## Tier 1: Setup (one-time provisioning)

Provision your Nano25 to run Fusion. Two-step procedure:

1. Program the FPGA bitstream into QSPI flash (Quartus Programmer)
2. Flash the SD card with the Fusion Linux image

→ See [`setup/`](setup/)

After completing Tier 1, your Nano25 boots into the default Fusion
demo on power-up.

## Tier 2: Additional demos (post-setup iteration)

Once your Nano25 is Fusion-capable (Tier 1 done), you can drop
additional Fusion demos via SCP without re-flashing the SD card. The
Linux + FPGA environment is shared across all demos.

→ See [`catalog/`](catalog/)

## Tier 3: Build your own UI

Convinced and want to build your own UI? Download the Fusion SDK
Starter package and use the AI-assisted workflow.

→ See [`https://github.com/cgx33/fusion-sdk`](https://github.com/cgx33/fusion-sdk)
