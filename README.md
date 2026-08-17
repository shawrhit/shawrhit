# Rohit Kumar Shaw

Firmware engineer. I write code that has to be right the first time, because by the time it fails, it's usually inside something you can't easily open back up.

Currently at **Anedya Systems**, Ahmedabad — building the low-level stack for a Beken BK7258, which is a chip most of the internet hasn't written a single line of documentation for. That's been the job, lately: reading silence where a datasheet should be, and turning it into something that works.

[shawrhit@gmail.com](mailto:shawrhit@gmail.com) · [linkedin.com/in/shawrhit](https://linkedin.com/in/shawrhit) · [shaws.systems](https://shaws.systems)

---

## What I've been building

**A WebRTC port that, as far as I can tell, didn't exist before.**
Ported `libpeer` onto the BK7258 — dual RISC-V, Armino/FreeRTOS, 8MB PSRAM, no prior art. Killed by pthread and mbedtls linker errors on the first attempt, alive again after finding the one flag (`MBEDTLS_SSL_DTLS_SRTP`) buried in the mbedtls config that nobody thought to mention. Now does 720p peer-to-peer and holds a stable connection over TURN relay, confirmed frame-by-frame in `webrtc-internals`. Small thing to describe, took a while to earn.

**A full connectivity SDK, underneath that.**
MQTT, OTA, and a key-value Valuestore layer — the unglamorous plumbing every device needs before it can be trusted to update itself in the field without someone driving out to fix it by hand.

**A bug that turned into an accounting lesson.**
TURN traffic was over-reporting. Root cause: `iceTransportPolicy: 'relay'` quietly opens four ports per session, not one. The kind of thing that looks like a mystery until you count carefully.

**A cyclotron doesn't get to fail gracefully.**
Earlier, at VECC — the Department of Atomic Energy's cyclotron facility — I wrote PSoC firmware for stripper control: multi-slave I2C, fault detection, watchdog recovery. Safety-critical in the literal sense. Good training for caring about edge cases.

---

## Longer-running things

**KryOS** — a fault-tolerant edge gateway for medical cold-chain monitoring, built as my undergraduate thesis. Buildroot Linux on a Raspberry Pi 4, ESP-MESH for quorum consensus between nodes, a custom kernel driver (`kryos_spi.ko`), and a protocol I called ASQC for keeping state honest when nodes disagree. Headed for an IEEE journal, supervised by Dr. Rupaban Subadar.

**RESONANCE** — acoustic fingerprinting for detecting leaks in underground pipes, on a MAX32630FTHR. Submitted to the AIoT Design Challenge 2026. The idea: a pipe under stress sounds different before it fails, if you're listening correctly.

**Two Arduino libraries, actually in the Library Manager** — `ESP32_Azure_MQTT_Manager` and `ESP32 AWS MQTT Manager`. Native MQTT-over-TLS, zero dependency on external clients, built because the existing options all made you choose between convenience and control. [GitHub →](https://github.com/shawrhit)

---

## Stack, roughly

```
RTOS & low-level    FreeRTOS, bare-metal C, ISR design, watchdog recovery
Silicon              BK7258 (RISC-V), ESP32, PSoC 5LP, PIC, Raspberry Pi
Wire protocols       MQTT, WebRTC/libpeer, TURN/STUN, Modbus, I2C, SPI, UART
Systems              Buildroot Linux, custom kernel drivers, Docker toolchains
Also                 Python, applied ML (unsupervised learning, RL)
```

---

*The closer the code sits to the hardware, the fewer places there are left to hide.*
