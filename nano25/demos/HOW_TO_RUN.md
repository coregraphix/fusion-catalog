# Run a Fusion demo on the Nano25

The same procedure applies to every ELF demo in this catalog — only the
binary filename changes.

## Prerequisites

- The one-time Nano25 setup is done (FPGA bitstream + SD card image —
  see the setup section on the Evaluate page).
- The board is powered, with HDMI connected to a display.
- Your PC and the board are on the same Ethernet network.

## 1. Give the board an IP address

Open the serial console (USB-UART, 115200 bauds — you land directly on
a root shell, no password) and assign an address:

```sh
ifconfig eth0 192.168.2.15
```

Pick any address that fits your local network. This is only needed
once per boot.

## 2. Deploy and run

From your PC (no password is required):

```bash
scp <demo>.elf root@192.168.2.15:/root/
ssh root@192.168.2.15 "chmod +x /root/<demo>.elf && /root/<demo>.elf"
```

The demo UI appears on the HDMI output.

## 3. Stop

`Ctrl+C` in the SSH session, or:

```bash
ssh root@192.168.2.15 "pkill <demo>"
```

## Troubleshooting

- **`scp` cannot connect** — check the IP is assigned (step 1) and
  that your PC is on the same subnet.
- **Demo starts but the display stays blank** — verify the HDMI
  connection and that the one-time setup completed (LED7 must blink
  ~3 times per second: that is the Fusion firmware heartbeat).
- **`Permission denied` at launch** — re-run the `chmod +x` step.
