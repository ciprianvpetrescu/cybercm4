# CyberCM4

**A DIY handheld cybersecurity device — Wi-Fi auditing + SDR signal analysis in a battery-powered, open, customizable package.**

CyberCM4 is a final-year BSc (Hons) Cyber Security major project: a handheld penetration-testing
toolkit built on the Raspberry Pi Compute Module 4, combining dual-band monitor-mode Wi-Fi
adapters with a HackRF One software-defined radio in a self-contained, battery-powered unit.

It was designed to fill the gap between commercial tools — the Wi-Fi Pineapple and the Flipper Zero —
which are powerful but closed-source, single-purpose, or expensive. CyberCM4 is open, modular,
and educational: built from off-the-shelf parts, documented end to end, and tested against a
controlled lab network.

> **⚠️ Legal & ethical use only.** This device is for security testing on networks and devices you
> own or have explicit written permission to test. Unauthorized access is illegal in most
> jurisdictions. The author takes no responsibility for misuse.

---

## Why

- Commercial pentest handhelds are closed-source and limited to one attack surface.
- Modern engagements cover Wi-Fi *and* RF/IoT — carrying a Pineapple, a HackRF and a Flipper is awkward.
- CyberCM4 combines Wi-Fi auditing and SDR analysis into one open source-controlled unit, built to be understood.

## Hardware

| Component | Role |
|---|---|
| Raspberry Pi Compute Module 4 (CM4) | Compute core |
| 2× dual-band Wi-Fi adapters (monitor mode) | Simultaneous capture/attack channels |
| HackRF One SDR | 100 MHz – 6 GHz wideband RF analysis |
| 6-inch touchscreen | Handheld UI |
| 2× 4,000 mAh Li-Po + Pimoroni LiPo Amigo | Battery power management |
| External antennas | RF sensitivity |

Multi-boot environment: Raspberry Pi OS, Kali Linux (ARM64), DragonOS Pi64.
Out-of-tree Realtek RTL88xxAU DKMS drivers compiled for monitor mode and packet injection.

## Features / tested capabilities

- **Wi-Fi scanning & monitoring** — all channels on 2.4/5 GHz; dual-adapter design monitors
  two channels simultaneously; client probe request capture.
- **WPA2 handshake capture** — deauthentication attack (`aireplay-ng --deauth`) with
  `airodump-ng` capture; 4-way handshake recovered as the client re-joins.
- **Rogue AP / evil twin** — `hostapd` + `dnsmasq` fake AP (same SSID, different channel);
  client tricked into reconnecting, DHCP request and traffic sniffed.
- **Captive portal** — runs an AP and a monitor interface simultaneously; CPU ~50–60%
  under concurrent load — acceptable, no crashes or lost packets in a 10-minute stability run.
- **SDR analysis** — continuous wideband sweeps (HackRF), spectrum monitoring in GQRX,
  capture/demodulation/replay of 433.92 MHz ASK key-fob transmissions (Universal Radio Hacker).
- **Touchscreen launcher** — Python/PyQt UI wrapping capture and scanning workflows into single-tap actions.

## Benchmarks

- Compared against the Hak5 Wi-Fi Pineapple Mark VII and Flipper Zero.
- 50–60% CPU under concurrent AP + sniffer load.
- Sustained capture capped at 8–10 MHz bandwidth by USB throughput.
- Custom drivers: no kernel panics or freezes observed during testing.

## Getting started

1. Assemble per the hardware table (see project report for full build details).
2. Flash multi-boot SD/eMMC: Raspberry Pi OS, Kali ARM64, DragonOS Pi64.
3. Compile and install the RTL88xxAU DKMS driver.
4. Launch the PyQt touchscreen launcher (see `launcher/`).
5. Test only on your own lab network — see the legal note above.

## Repository layout

```
launcher/     Python/PyQt touchscreen launcher
docs/         Build notes and configuration guides
report/       Full project report (redacted) — optional
```

## Project report

The full 30-page report (literature review, implementation, testing & results, limitations,
conclusion) was completed for the BSc (Hons) Cyber Security programme. Contact the author for a copy.

## License

Open source — pick a license (MIT/GPL) before publishing. Hardware designs and scripts are
provided as-is for educational use.

---

*Built by Ciprian Petrescu — BSc (Hons) Cyber Security major project. Supervised by Segun Popoola.*
