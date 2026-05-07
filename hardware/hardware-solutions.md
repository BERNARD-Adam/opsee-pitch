# OpSee — Edge Hardware Solutions

## Overview

Three hardware tiers to replace the Belden OpEdge + BHDO stack, built entirely on open-source permissive foundations.

| Layer | Technology | License |
|---|---|---|
| Edge Platform | EdgeX Foundry | Apache 2.0 |
| Carrier Boards | Seeed Studio OSHW-Jetson-Series | Apache 2.0 |
| Application | OpSee (proprietary) | — |

No vendor lock-in at any layer. All hardware designs are published with full schematics and 3D files.

---

## Tier 1 — Starter (Free / Low-Cost)

> Basic OT data collection. No AI/LLM. Ideal for small deployments, evaluation, or cost-sensitive sites.

### Hardware: Raspberry Pi 5 (4GB or 8GB)

| Spec | Value |
|---|---|
| CPU | Quad-core ARM Cortex-A76 @ 2.4 GHz |
| RAM | 4 GB or 8 GB LPDDR4X |
| GPU | VideoCore VII (no AI acceleration) |
| Storage | microSD or NVMe via PCIe HAT |
| Networking | Gigabit Ethernet, Wi-Fi 5, BLE 5.0 |
| USB | 2x USB 3.0, 2x USB 2.0 |
| Power | 5V / 5A USB-C (~4W idle) |
| **Price** | **~$60 (4GB) / ~$95 (8GB)** |

### Industrial Add-ons Required

| Component | Purpose | Price |
|---|---|---|
| DIN rail metal case (e.g. Waveshare PI5-CASE-D) | Industrial mounting, protection | ~$15–25 |
| RS485 / CAN HAT | Modbus RTU, industrial bus connectivity | ~$15–30 |
| NVMe HAT + SSD (optional) | Expanded storage via PCIe | ~$30–50 |

### Total BOM: ~$100–$140

### Software Stack

```
┌──────────────────────────────┐
│  OpSee Application           │
├──────────────────────────────┤
│  EdgeX Foundry               │
│  (OT data collection,        │
│   rules engine, export)      │
├──────────────────────────────┤
│  Raspberry Pi OS (Linux)     │
├──────────────────────────────┤
│  Raspberry Pi 5              │
└──────────────────────────────┘
```

### Capabilities

- Protocol connectivity: Modbus RTU/TCP, OPC-UA, MQTT, BACnet (via EdgeX device services)
- Edge rules engine (eKuiper) for local alerting
- Data export to cloud / enterprise systems
- Device command & control
- REST API gateway with security

### Limitations

- No AI/LLM inference on-device
- Not industrial-grade out of the box (requires add-ons for RS485, DIN rail)
- Single M.2 slot shared between storage and peripherals

---

## Tier 2 — Standard (Industrial-Ready)

> Turnkey industrial gateway. Built-in RS485, DIN rail, NVMe. No AI/LLM. Ready for production deployment.

### Hardware: Seeed reComputer R1000

| Spec | Value |
|---|---|
| CPU | Quad-core ARM Cortex-A72 @ 1.5 GHz (Raspberry Pi CM4) |
| RAM | 4 GB or 8 GB |
| Storage | 32 GB eMMC + **M.2 NVMe slot** (128GB–1TB) |
| Industrial I/O | **3x RS485**, 2x Ethernet (GbE), 1x HDMI, 3x USB 2.0 |
| Wireless | Wi-Fi, BLE, optional LoRaWAN / Zigbee / 4G LTE |
| Enclosure | DIN-rail mountable, industrial-grade housing (included) |
| Temp Range | Industrial operating range |
| **Price** | **~$209** |

### NVMe Note

The reComputer R1000 has a single M.2 M-Key slot supporting NVMe 2280 SSDs (128GB to 1TB). This slot is shared — you must choose between an NVMe SSD or an AI accelerator (e.g. Hailo-8, Coral M.2). For Tier 2 (no AI), use it for storage.

### Software Stack

```
┌──────────────────────────────┐
│  OpSee Application           │
├──────────────────────────────┤
│  EdgeX Foundry               │
│  (OT data collection,        │
│   rules engine, export)      │
├──────────────────────────────┤
│  Raspberry Pi OS (Linux)     │
├──────────────────────────────┤
│  Seeed reComputer R1000      │
│  (CM4, DIN rail, RS485 x3)  │
└──────────────────────────────┘
```

### Capabilities

- Everything in Tier 1, plus:
- **Native RS485 x3** — direct Modbus RTU to PLCs/sensors without HATs
- **Dual Ethernet** — separate OT and IT networks
- **Industrial enclosure** included — DIN rail, no assembly
- Optional wireless (LoRaWAN, Zigbee, 4G LTE) for remote sites
- Plug-and-play production deployment

### Limitations

- No AI/LLM inference on-device
- CM4 is slightly slower than Raspberry Pi 5
- Single M.2 slot (choose between NVMe SSD or AI accelerator)

---

## Tier 3 — Premium (Edge AI + LLM)

> Full EdgeX platform with on-device LLM inference. For advanced analytics, natural language queries on OT data, and autonomous edge intelligence.

### Hardware: NVIDIA Jetson AGX Orin + Seeed J501 Carrier Board

The Seeed J501 carrier board is **pin-compatible with all Jetson AGX Orin variants**. You are free to source whichever Orin module fits your performance and budget requirements independently from any supplier.

#### Compute Module — NVIDIA Jetson AGX Orin (Choose Your Variant)

| Spec | AGX Orin 32GB | AGX Orin 64GB | AGX Orin Industrial 64GB |
|---|---|---|---|
| GPU | 1792-core Ampere + 56 tensor cores | 2048-core Ampere + 64 tensor cores | 2048-core Ampere + 64 tensor cores |
| CPU | 8-core ARM Cortex-A78AE | 12-core ARM Cortex-A78AE | 12-core ARM Cortex-A78AE (lower freq.) |
| AI Performance | **200 TOPS** | **275 TOPS** | **248 TOPS** |
| DLA | 2x NVDLA v2.0 | 2x NVDLA v2.0 | 2x NVDLA v2.0 |
| RAM | 32 GB LPDDR5 | **64 GB LPDDR5** | **64 GB LPDDR5 ECC** |
| Memory Bandwidth | 205 GB/s | 205 GB/s | 205 GB/s |
| Storage | 64 GB eMMC 5.1 | 64 GB eMMC 5.1 | 64 GB eMMC 5.1 |
| Power | 15–40W | 15–60W | 15–75W |
| Temp Range | -25°C to +80°C | -25°C to +80°C | **-40°C to +85°C** |
| ECC Memory | No | No | **Yes** |
| **Module Price** | **~$999** | **~$1,599 / ~€1,904** | **Contact distributor** |
| Form Factor | 100 x 87 mm | 100 x 87 mm | 100 x 87 mm (pin-compatible) |

#### Which Orin To Choose?

| Use Case | Recommended Variant | Why |
|---|---|---|
| Small LLMs (3B–7B), single user, basic edge AI | **AGX Orin 32GB** | Sufficient memory for quantized 7B models, lowest cost |
| Medium LLMs (7B–13B), multi-request, vision AI | **AGX Orin 64GB** | 64GB unified memory fits 13B unquantized, headroom for concurrent requests |
| Large LLMs (13B–70B), mission-critical, harsh environments | **AGX Orin Industrial 64GB** | ECC memory for data integrity, extended temp range (-40°C to +85°C), longer lifetime |

#### LLM Performance Comparison by Variant

Single-request inference (MAXN power mode, jetson_clocks enabled):

| Model | Quantization | AGX Orin 32GB | AGX Orin 64GB | Notes |
|---|---|---|---|---|
| **3B** (Llama 3.2, Phi-2) | Q4_K_M | ~30–40 tok/s | ~35–45 tok/s | Both variants handle this easily |
| **7B** (Mistral, Llama 2) | Q4_K_M | ~15–20 tok/s | ~18–25 tok/s | Sweet spot for 32GB |
| **13B** (Llama 2-13B) | Q4 | ~8–12 tok/s | ~12–16 tok/s | 64GB can run FP16 (no quantization) |
| **13B** (Llama 2-13B) | FP16 | Memory limited | ~8–10 tok/s | **64GB only** — requires ~26GB VRAM |
| **70B** (Llama 2-70B) | Q4 | Not feasible | ~3–5 tok/s | Requires ~35GB — 64GB only |

#### Multi-Request / Concurrent Inference

This is where the **memory difference becomes critical**. LLM serving with multiple simultaneous users requires memory for each active KV-cache context.

| Scenario | AGX Orin 32GB | AGX Orin 64GB |
|---|---|---|
| **7B model, 1 concurrent request** | ~18 tok/s, ~14GB used | ~22 tok/s, ~14GB used |
| **7B model, 2–3 concurrent requests** | Feasible (~10–12 tok/s each), memory tight | Comfortable (~15–18 tok/s each) |
| **7B model, 5+ concurrent requests** | **OOM risk** — KV-cache exhausts 32GB | Feasible (~10–12 tok/s each) |
| **13B model, 1 concurrent request** | Quantized only, ~10 tok/s | FP16 possible, ~10 tok/s |
| **13B model, 2+ concurrent requests** | **Not feasible** — insufficient memory | Feasible with Q4 (~8 tok/s each) |
| **7B + EdgeX + OpSee running simultaneously** | ~15GB free for LLM (EdgeX uses ~2–3GB) | ~47GB free for LLM |

> **Rule of thumb**: The 32GB variant works for **single-user / single-request** scenarios. The 64GB variant is needed for **multi-request serving**, larger models, or running LLM alongside other memory-hungry services (vision AI, EdgeX with many device services).

#### Carrier Board — Seeed reServer Industrial J501

| Spec | Value |
|---|---|
| Form Factor | 110 x 110 mm (ultra-compact) |
| Networking | **10G SFP+ Ethernet**, Gigabit Ethernet (RJ45) |
| Industrial I/O | **RS-485**, **CAN bus**, USB 3.2, HDMI 2.1 |
| Expansion | Multiple M.2 slots, GMSL camera support (optional) |
| Camera | Up to 8x GMSL2 cameras via extension board |
| Video | 8K decode support |
| Compatibility | **All Jetson AGX Orin variants** (32GB, 64GB, Industrial) — same 699-pin connector |
| License | **Apache 2.0** (open-source hardware) |
| **Price** | **~$379** (carrier board only) |

#### Enclosure Options

| Approach | Description | Price | Best For |
|---|---|---|---|
| **Seeed Developer Kit bundle** | Carrier + heatsink/fan + Orin + 128GB NVMe + PSU. No sealed industrial enclosure. | ~$1,444 (32GB) / ~$2,144 (64GB) | Prototyping, first 10 units |
| **Seeed custom config** (contact sales) | Request chassis + carrier + heatsink without Orin module, source module independently. Email: order@seeedstudio.com | TBD | Pilot / small batch |
| **Custom CNC aluminum enclosure** | Fanless design using open-source 3D files from Seeed's GitHub. Chassis acts as passive heatsink. | ~$150–400/unit | 10–100 units |
| **Custom die-cast enclosure** | Tooled aluminum enclosure for volume production. | ~$5–20/unit (after $3–5K tooling) | 100+ units |

#### Total Tier 3 Pricing (module + carrier, excluding enclosure)

| Configuration | Module | Carrier | Total |
|---|---|---|---|
| AGX Orin 32GB + J501 | ~$999 | ~$379 | **~$1,378** |
| AGX Orin 64GB + J501 | ~$1,599 | ~$379 | **~$1,978** |
| AGX Orin Industrial 64GB + J501 | Contact distributor | ~$379 | **~$2,500+** (estimated) |

### Software Stack

```
┌──────────────────────────────┐
│  OpSee Application           │
│  + NLP Interface to OT Data  │
├──────────────────────────────┤
│  LLM Runtime                 │
│  (llama.cpp / TensorRT-LLM   │
│   / Ollama)                  │
├──────────────────────────────┤
│  EdgeX Foundry               │
│  (OT data collection,        │
│   rules engine, export)      │
├──────────────────────────────┤
│  JetPack SDK (Linux / L4T)   │
├──────────────────────────────┤
│  Jetson AGX Orin (32/64/Ind) │
│  + Seeed J501 Carrier        │
│  + Industrial Enclosure      │
└──────────────────────────────┘
```

### Capabilities

- Everything in Tier 1 & 2, plus:
- **On-device LLM** — natural language queries on OT data, anomaly explanation, report generation
- **Up to 275 TOPS AI** — computer vision, predictive maintenance, multi-sensor fusion
- **Multi-request LLM serving** (64GB variants) — multiple users/agents querying simultaneously
- **10G Ethernet** — high-bandwidth data ingest (cameras, high-frequency sensors)
- **CAN bus** — automotive, robotics, machine-to-machine
- **ECC memory** (Industrial variant) — data integrity for safety-critical applications
- **Extended temp range** (Industrial variant) — -40°C to +85°C for extreme environments
- **Open-source hardware** — full schematics and 3D files available for custom enclosure design
- **Module flexibility** — choose and source the Orin variant independently based on your needs

---

## Tier Comparison

| | Tier 1 — Starter | Tier 2 — Standard | Tier 3 — Premium |
|---|---|---|---|
| **Device** | Raspberry Pi 5 | Seeed reComputer R1000 | Jetson AGX Orin + Seeed J501 |
| **Price** | ~$100–140 | ~$209 | ~$1,378–$2,500+ |
| **CPU** | 4x A76 @ 2.4 GHz | 4x A72 @ 1.5 GHz | 8–12x A78AE @ 2.2 GHz |
| **RAM** | 4–8 GB | 4–8 GB | 32–64 GB (unified, optional ECC) |
| **AI Performance** | None | None | 200–275 TOPS |
| **LLM Capable** | No | No | Yes (3B–70B depending on variant) |
| **Multi-Request LLM** | No | No | 32GB: single-request / 64GB: multi-request |
| **Industrial I/O** | Via HATs (add-on) | Native (3x RS485, 2x GbE) | Native (RS485, CAN, 10GbE) |
| **Enclosure** | DIN rail case (add-on) | Included (DIN rail) | Separate (buy or custom) |
| **Industrial Ready** | With add-ons | Out of the box | With enclosure solution |
| **Extreme Temp (-40°C)** | No | No | Industrial variant only |
| **Open Source HW** | Partial | Seeed designs | Apache 2.0 (Seeed J501) |
| **EdgeX Foundry** | Yes | Yes | Yes |
| **Target** | Eval, small sites | Production OT gateway | Edge AI + LLM |

---

## Sourcing Summary

| Component | Supplier | Link |
|---|---|---|
| Raspberry Pi 5 (8GB) | raspberrypi.com / resellers | [Buy](https://www.raspberrypi.com/products/raspberry-pi-5/) |
| DIN rail case for Pi 5 | Waveshare | [PI5-CASE-D](https://www.waveshare.com/pi5-case-d.htm) |
| Seeed reComputer R1000 | Seeed Studio | [Buy](https://www.seeedstudio.com/reComputer-R1025-10-p-5895.html) |
| Jetson AGX Orin 64GB (module) | Silicon Highway Direct | [Buy](https://www.siliconhighwaydirect.com/product-p/900-13701-0050-000.htm) |
| Seeed J501 carrier board | Seeed Studio | [Buy](https://www.seeedstudio.com/reServer-Industrial-J501-Carrier-board-for-Jetson-AGX-Orin-p-5950.html) |
| Seeed J501 open-source files | GitHub | [OSHW-Jetson-Series](https://github.com/Seeed-Studio/OSHW-Jetson-Series) |
| EdgeX Foundry | GitHub / Docker Hub | [edgexfoundry.org](https://www.edgexfoundry.org/) |

---

## Licensing

| Component | License | Commercial Use |
|---|---|---|
| EdgeX Foundry | Apache 2.0 | Yes — free, no royalties |
| Seeed J501 hardware design | Apache 2.0 | Yes — free, can manufacture derivatives |
| NVIDIA JetPack SDK | NVIDIA EULA | Yes — free for Jetson hardware |
| BHDO (Belden — current) | Proprietary subscription | Annual fee, closed source |
