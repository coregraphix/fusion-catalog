# Run a Fusion demo on the Nano25

The same procedure applies to every ELF demo in this catalog — only the
binary filename changes.

## Prerequisites

- The one-time Nano25 setup is done (FPGA bitstream + SD card image —
  see the setup section on the Evaluate page).
- The board is powered, with HDMI connected to a display.
- The demos are **touch-enabled**: connect the display's USB (touch)
  cable to the board's Type-C labelled **USB OTG** — of the two
  side-by-side Type-C ports, it is the one closest to the board
  corner (the other one is the programming/UART port). Without it,
  the demos run display-only.
- Ethernet: plug the board into your LAN, **or** directly into your PC
  with a point-to-point cable — no network infrastructure needed.

## 1. Deploy and run

The board configures its network by itself at boot and announces
itself as **`nano25.local`**. No password is required.

The board boots into the default Fusion demo — stop it first to free
the display, then deploy and run yours:

```bash
ssh root@nano25.local "systemctl stop fusion-demo"
scp <demo>.elf root@nano25.local:/root/
ssh root@nano25.local "chmod +x /root/<demo>.elf && /root/<demo>.elf"
```

The demo UI appears on the HDMI output. The default demo comes back
at the next power-up.

## 2. Stop

`Ctrl+C` in the SSH session, or:

```bash
ssh root@nano25.local "pkill <demo>"
```

## Make a demo the boot demo

The boot demo is whatever `/root/fusion-demo` points to:

```bash
ssh root@nano25.local "ln -sf /root/<demo>.elf /root/fusion-demo && systemctl restart fusion-demo"
```

## If `nano25.local` does not resolve

Some corporate networks block mDNS. The board also always carries the
static address **`192.168.77.15`** — connect it directly to your PC
with an Ethernet cable, set your PC's adapter to `192.168.77.10`
(mask `255.255.255.0`), and use the address instead of the name:

```bash
ssh root@192.168.77.15
```

## Troubleshooting

- **`scp`/`ssh` cannot connect** — check the Ethernet link, and try
  the static-address fallback above.
- **`scp: dest open ... Failure`** — the file you are overwriting is
  currently running. Stop it first:
  `ssh root@nano25.local "systemctl stop fusion-demo"`.
- **Demo starts but the display stays blank** — verify the HDMI
  connection and that the one-time setup completed (LED7 must blink
  ~3 times per second: that is the Fusion firmware heartbeat).
- **`Permission denied` at launch** — re-run the `chmod +x` step.
