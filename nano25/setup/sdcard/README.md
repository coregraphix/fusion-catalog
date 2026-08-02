# Step 2 — Flash the SD card

This step writes the Linux + Fusion userspace image onto a MicroSD
card. The Nano25's HPS (ARM cores) boots from this card.

**Prerequisite**: Step 1 (firmware) must have been completed on the
target Nano25 board, otherwise the FPGA fabric will not have the
Fusion GPU and the userspace will fail at hardware init.

## What's in this folder

| File | Purpose |
|---|---|
| `nano25-setup-sdcard-v4.1.0.img.xz` | Compressed Linux + Fusion image (~800 MB compressed, ~7.5 GB uncompressed) |

## Prerequisites

- A MicroSD card, ≥ 8 GB
- A MicroSD card reader/writer
- A flashing tool:
  - **Windows**: [Win32 Disk Imager](https://win32diskimager.org/) or [Rufus](https://rufus.ie/)
  - **Linux/macOS**: `dd` (built-in)

## Procedure

### Windows — Win32 Disk Imager

1. Decompress the image (right-click → 7-Zip → Extract Here) to get `nano25-setup-sdcard-v4.1.0.img`
2. Insert the MicroSD card; note its drive letter (e.g. `E:`)
3. Open Win32 Disk Imager
4. Image File: select `nano25-setup-sdcard-v4.1.0.img`
5. Device: select your SD card drive letter — **double-check, this will erase the card**
6. Click **Write** — wait for completion (~15 min for 7.5 GB)
7. Eject safely

### Windows — Rufus

Rufus handles `.img.xz` directly without manual decompression:

1. Insert the MicroSD card
2. Open Rufus
3. Device: your SD card
4. Boot selection: `nano25-setup-sdcard-v4.1.0.img.xz`
5. Click **START**

### Linux / macOS

```bash
# Identify your SD card device (verify with lsblk or diskutil)
xz -dc nano25-setup-sdcard-v4.1.0.img.xz | sudo dd of=/dev/sdX bs=4M status=progress
sync
```

Replace `/dev/sdX` with your actual SD card device path. **Verify
this is your SD card and not your system disk** — `dd` is destructive.

## Verification

After flashing:

1. Eject the SD card from your PC
2. Insert it into the Nano25's MicroSD slot
3. Connect the Nano25's HDMI to a display
4. For touch interaction: connect the display's USB (touch) cable to
   the board's Type-C labelled **USB OTG** (of the two side-by-side
   Type-C ports, the one closest to the board corner)
5. Power on the Nano25 (5V DC)
6. After ~15 seconds, the Fusion demo appears on the display

LED7 is the Fusion firmware heartbeat: it blinks (~3 Hz) as soon as
the FPGA fabric is configured with the Fusion bitstream.

If LED7 blinks but the display stays blank:
- The firmware (Step 1) is fine — the problem is on the SD/Linux side
- Check HDMI connection / monitor input source
- Check the SD card is properly seated; if needed re-flash it (Step 2)

If LED7 does not blink at all:
- The FPGA fabric is not configured — verify Step 1 (firmware) was
  completed on this board
- Verify MSEL = AS mode (SW5 switch: MSEL[2:0] = 001, factory
  default — see DE25-Nano User Manual §3.1 or Getting Started
  Guide §3.2)

## Connecting to the board

The image is set up for frictionless access — you get a root shell
directly, no login or password required.

### Serial console

Connect the Nano25's USB-UART to your PC and open a terminal
(PuTTY, MobaXterm, `minicom`...) at **115200 bauds, 8N1**. The
console drops you straight into a root shell.

### SSH

The board configures its network by itself at boot and announces
itself as **`nano25.local`** — plug the Ethernet cable into your LAN,
or directly into your PC (point-to-point, no network infrastructure
needed), and connect:

```sh
ssh root@nano25.local
```

No password is required. You can now copy binaries with `scp` and
run them directly — stop the boot demo first to free the display:

```sh
ssh root@nano25.local 'systemctl stop fusion-demo'
scp my_app root@nano25.local:/root/
ssh root@nano25.local 'chmod +x /root/my_app && /root/my_app'
```

The default Fusion demo comes back at the next power-up.

If your network blocks mDNS (`nano25.local` does not resolve), the
board also always carries the static address **`192.168.77.15`**:
connect it directly to your PC, set your PC's adapter to
`192.168.77.10` (mask `255.255.255.0`), and use
`ssh root@192.168.77.15`.

> **Note**: this open-access configuration is intended for evaluation
> on a local development network. To lock the board down, set a root
> password with `passwd root`.

## Updating

To install a new SD image version (e.g. when a new Fusion release
ships), repeat the above procedure with the new `.img.xz`. Your
QSPI bitstream from Step 1 stays in place and does not need
reprogramming unless the FPGA design itself has changed.

If both QSPI and SD need a coordinated update, redo Step 1 + Step 2
in order.
