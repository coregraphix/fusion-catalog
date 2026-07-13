# Step 1 — Program the FPGA bitstream

This step programs the Fusion FPGA bitstream into the Nano25's QSPI
flash. The bitstream is then loaded into the FPGA fabric automatically
on every power-up (AS configuration mode).

This is a **one-time operation per board** — the bitstream stays in
QSPI flash until reprogrammed.

## Download

The firmware is distributed as a single zip bundle attached to its
GitHub Release — the Download button on the Evaluate page always
points to the current one:

```
nano25-setup-firmware.zip   (~4.8 MB compressed)
├── README.md                                ← this guide (offline copy)
├── fusion_top_hps.jic                       ← FPGA bitstream + HPS first-stage (~16 MB)
└── program_qspi_flash/
    ├── flash_program.bat                    ← Windows batch: erase + program QSPI
    └── flash_erase.bat                      ← Windows batch: erase QSPI only
```

Extract the zip into a working folder. The relative paths between
the `.jic` and the batch scripts must be preserved (the scripts
reference `..\fusion_top_hps.jic`).

## Prerequisites

- DE25-Nano board powered (5V DC)
- USB Type-C cable connecting the board's USB Blaster III port to your PC
- **Quartus Prime Pro v25.1.1+** installed with USB Blaster III driver
- MSEL switches on the Nano25 set to AS mode: `SW5 MSEL[2:0] = 001`
  (factory default — see [`../../vendor/DE25_Nano_Getting_Started_Guide.pdf`](../../vendor/DE25_Nano_Getting_Started_Guide.pdf) §3.2)

## Procedure

### Option A — Quartus Programmer GUI (visual)

1. Power up the Nano25 and connect USB Type-C to your PC
2. Open Quartus Prime → **Tools → Programmer**
3. Click **Hardware Setup** → select `DE25-Nano [USB-1]` → Close
4. Click **Auto Detect** — the FPGA + QSPI flash chain appears
5. Select the **QSPI** device → click **Change File** → choose
   `fusion_top_hps.jic` from the extracted folder
6. Check **Program/Configure** for the QSPI device
7. Click **Start** — wait for "100% (Successful)"
8. Power-cycle the board — Fusion bitstream now loads automatically

### Option B — Batch script (faster)

From a Quartus shell (so `QUARTUS_ROOTDIR` is set in environment),
in the extracted bundle folder:

```bat
cd program_qspi_flash
flash_program.bat
```

This runs `quartus_pgm.exe -m jtag -c 1 -o "pvi;..\fusion_top_hps.jic"`
which erases + programs + verifies + initializes the QSPI flash in one shot.

To erase only (revert to blank QSPI):

```bat
cd program_qspi_flash
flash_erase.bat
```

## Verification

After programming + power-cycle:

- LED7 starts flashing (HPS boots from QSPI configuration of the FPGA + SD)
- The FPGA fabric now exposes the Fusion GPU peripherals to the HPS

Once Step 1 is complete, proceed to
[Step 2: flash the SD card](../sdcard/README.md).

## Notes

- The `.jic` bundles the FPGA bitstream with HPS first-stage logic
  needed for the Agilex 5 SoC boot flow.
- Quartus Prime Pro is a free download for Agilex 5 devices — no
  paid license required. See
  [`../../vendor/DE25_Nano_Getting_Started_Guide.pdf`](../../vendor/DE25_Nano_Getting_Started_Guide.pdf) §2.3.
