# 💡 Analog Glow – Real-Time IoT LED Data Gauge

> A Raspberry Pi system that converts live weather and traffic data into LED brightness for instant physical awareness.

---

## 👥 Team — ElectroBoom

| Name | 
|---|---|
| Kalpesh Kisan Naik | 
| Shikhar Swarup | 
| Sonali Parishwad | 
| Ayush Kumar Sahu |

---

## 📌 Project Overview

**Analog Glow** is a real-time data visualization system that works **without screens**.

Instead of apps or dashboards, it uses **LED brightness as an information carrier**. The Raspberry Pi continuously fetches:

- 🌧️ Rain probability — from **OpenWeatherMap API**
- 🚦 Traffic delay — from **Google Maps Distance Matrix API**

These values are mapped to PWM signals controlling three LEDs:

| LED | Represents |
|---|---|
| 🔴 Red | Traffic intensity |
| 🟡 Yellow | Rain probability |
| 🟢 Green | Overall safe/normal condition |

The goal is **instant perception** — a user understands current conditions in under a second, just by glancing at the LEDs. This shifts interaction from **active** (checking your phone) to **passive** (ambient awareness).

---

## 💡 Inspiration

- **Ambient Computing** — Smart systems that provide information passively, without direct user interaction.
- **Traffic Signal Systems** — Using color and intensity to convey critical information instantly.
- **IoT Data Systems** — Collecting and processing real-time data from external APIs.
- **Minimal Interface Devices** — Fitness bands and indicators that use simple visual cues instead of screens.

### Original Twist

Most systems display data via graphical dashboards, mobile apps, or numerical displays — all requiring active attention.

This project **eliminates the traditional interface entirely**, using physical light output as the sole communication medium:

- ❌ No screen or graphical interface
- ❌ No user interaction required
- ✅ Real-time data through LED brightness — higher brightness = higher intensity of a condition

---

## 🏗️ System Architecture

```
Internet APIs → Python Processing → GPIO PWM Output → LEDs
```

### Input / Output Map

| System Part | Type | Function |
|---|---|---|
| OpenWeatherMap API | Input | Rain probability data |
| Google Maps API | Input | Traffic delay information |
| Raspberry Pi 4B | Processing | Executes code, controls GPIO |
| Python Script | Processing | API calls, normalization, logic |
| LEDs (Red, Yellow, Green) | Output | Real-time data via brightness |
| Power Supply | Support | Powers the system |

---

## 🔌 Electronics

### Components

| Component | Quantity | Purpose |
|---|---|---|
| Raspberry Pi 4B (4GB RAM) | 1 | Main controller |
| LEDs (Red, Yellow, Green) | 3 | Visual output |
| Resistors (220Ω–330Ω) | 3 | Current limiting |
| Breadboard | 1 | Prototyping |
| Jumper Wires | ~10 | Connections |
| USB-C Power Adapter (5V) | 1 | Power supply |

### GPIO Wiring

| GPIO Pin | Physical Pin | LED |
|---|---|---|
| GPIO17 | Pin 11 | 🔴 Red |
| GPIO27 | Pin 13 | 🟡 Yellow |
| GPIO22 | Pin 15 | 🟢 Green |

All LED cathodes share a **common ground** (Physical Pin 6).

**Wiring per LED:**
```
GPIO Pin → Resistor → LED Anode (+) → LED Cathode (−) → GND
```

---

## 💻 Software

### Tools & Libraries

| Tool / Library | Purpose |
|---|---|
| Python | Main programming language |
| `gpiozero` | GPIO control and PWM for LED brightness |
| `requests` | HTTP calls to external APIs |
| Raspberry Pi OS | Execution environment |

### Algorithm / Logic Flow

```
Start
  ↓
Initialize GPIO and LEDs
  ↓
Connect to internet
  ↓
Fetch weather data (OpenWeatherMap)
  ↓
Fetch traffic data (Google Maps)
  ↓
Parse and extract values
  ↓
Normalize values (0.0 → 1.0)
  ↓
Set LED brightness via PWM
  ↓
Wait (10–30 seconds)
  ↓
Repeat loop
```

**Decision Logic:**
- Higher rain probability → 🟡 Yellow LED brighter
- Higher traffic delay → 🔴 Red LED brighter
- Lower combined values → 🟢 Green LED brighter

**Error Handling:** If an API call fails, default fallback values are used to prevent a system crash.

---

## ✅ Definition of Success

### Minimum Viable Product
- [ ] Raspberry Pi controls 3 LEDs via GPIO
- [ ] At least one API (weather or traffic) integrated
- [ ] PWM brightness mapped from real data
- [ ] Continuous loop with periodic updates

### Stretch Features
- [ ] Data smoothing to prevent sudden brightness jumps
- [ ] Support for multiple locations (not just fixed inputs)
- [ ] Web/mobile interface for monitoring values
- [ ] Historical data logging
- [ ] Automatic error recovery & retry
- [ ] Physical enclosure for durability and aesthetics

---

## 📅 Hackathon Timeline

| Day | Date | Plan | Status |
|---|---|---|---|
| Day 1 | 30 April | Concept, hardware setup, API setup, initial Python script | ✅ In Progress |
| Day 2 | 1 May | Continue development | ⚠️ No hardware access (lab closed) |
| Day 3 | 2 May | Full integration, testing, final submission | 🔜 Upcoming |

### Update Log

| Day | Planned Goal | What Happened | Next Steps |
|---|---|---|---|
| 30 April | Build + API setup | Hardware + partial code done | Finish integration |
| 1 May | Continue development | No hardware access (holiday) | Resume next day |
| 2 May | Final integration | — | Submit project |

---

## 📋 Task Breakdown

| Task ID | Task | Deadline | Status |
|---|---|---|---|
| T1 | Finalize concept | 30 April | — |
| T2 | Hardware setup (LED + GPIO) | 30 April | — |
| T3 | API setup and testing | 30 April | — |
| T4 | Python implementation | 30 April | — |
| T5 | Integration (HW + SW) | 2 May | — |
| T6 | Testing and debugging | 2 May | — |
| T7 | Documentation | 30 Apr – 2 May | 🔄 Ongoing |

---

## 💰 Bill of Materials

| Item | Qty | Source | Cost (INR) |
|---|---|---|---|
| Raspberry Pi 4B | 1 | Kit | ₹0 |
| LEDs (R/Y/G) | 3 | Kit | ₹0 |
| Resistors (220–330Ω) | 3 | Kit | ₹0 |
| Breadboard | 1 | Kit | ₹0 |
| Jumper Wires | ~10 | Kit | ₹0 |
| USB-C Power Adapter | 1 | Kit | ₹0 |
| **Total** | | | **₹0** |

All components are sourced from existing kits. No additional purchases required.

---

## 🔧 Build & Fabrication Notes

- Breadboard-based prototype — no soldering required
- Each LED individually tested with a simple Python script after wiring
- API keys for OpenWeatherMap and Google Maps added to the Python script
- `gpiozero` and `requests` libraries installed on Raspberry Pi OS

---

## ⚠️ Risks & Unknowns

> *(To be filled in as the project progresses)*

---

## 🧪 Testing

> *(Testing logs and playtesting notes to be updated post-integration)*

---

*Built with ❤️ by Team ElectroBoom*
