# 🌟 Pulsing Glow – Real-Time IoT LED Data Gauge

> A Raspberry Pi-based system that converts real-time weather and traffic data into LED brightness for instant ambient awareness.

---

## 🏫 SKILL LAB PRACTICAL HACKATHON — Final Project

### 👥 Team Identity

**Studio / Group Name:** ElectroBoom

| Name | Primary Role | Secondary Role | Strengths |
|------|-------------|----------------|-----------|
| Kalpesh Naik *(Team Leader)* | Logical Thinking, Software, Electronics | Testing, Integration | Circuit design, hardware debugging, API integration |
| Shikhar Swarup | Coding, Software | Integration | Python programming |
| Sonali Parishwad | Documentation | Coordination | Structured writing, organization |
| Ayush Kumar Sahu | Documentation | Testing | Debugging |

---

## 💡 Project Overview

### One-Line Pitch
A Raspberry Pi-based system that converts real-time weather and traffic data into LED brightness for instant ambient awareness.

### Expanded Idea

This project presents a novel way of visualizing real-time data **without using screens or graphical interfaces**. Instead of relying on mobile applications or dashboards, the system uses LED brightness as a medium to communicate information.

The Raspberry Pi continuously fetches **rain probability** from a weather API and **traffic delay data** from a mapping API. These values are processed and mapped to PWM (Pulse Width Modulation) signals, which control the brightness of three LEDs:

- 🔴 **Red LED** → Traffic intensity
- 🟡 **Yellow LED** → Rain probability
- 🟢 **Green LED** → Overall safe conditions

The objective is to enable **instant understanding** — by simply observing LED brightness, users can interpret real-world conditions passively, without actively checking a device.

---

## ✨ Inspiration

| Source Type | Title / Link | What Inspired Us |
|------------|-------------|------------------|
| **API** | [TomTom Distance Matrix API](https://developer.tomtom.com/routing-api/documentation/tomtom-maps/product-information/introduction) | Real-time traffic delays to control Red LED intensity |
| **API** | [OpenWeatherMap API](https://openweathermap.org/api) | Live rain probability mapped to Yellow LED |
| **Research Paper** | [From Screens to Ambient AI (PDF)](https://puirp.com/index.php/research/article/download/121/105/114) | Shifting from active screen time to passive IoT awareness |
| **Video Tutorial** | [PWM with Raspberry Pi 4 LED Brightness Control](https://www.youtube.com/watch?v=6KO-KPX3Riw) | Hardware setup and PWM duty cycle logic |
| **Concept** | Ambient Computing | Passive data delivery without user interaction |
| **Real-world System** | Traffic Signals | Quick understanding through light indicators |

### Original Twist

Most systems present data using dashboards or mobile apps requiring user attention. This project **eliminates screen dependency** by using physical light output as the sole communication medium. Higher LED brightness = higher intensity condition. Lower brightness = normal/safe. Complex real-world data becomes a simple, intuitive, and continuously visible physical signal.

---

## 🗺️ System Architecture

### High-Level Flow

```
Internet APIs → Data Processing (Python on Raspberry Pi) → GPIO PWM Signals → LED Output
```

### Flowchart

> *See `/docs/flowchart_full_system.png` and `/docs/flowchart_pulsing_glow.png` for full diagrams.*

**Simplified Algorithm:**
```
START
  └─ Initialize GPIO/PWM
  └─ Get User Input (Source & Destination)
  └─ Convert to Coordinates (TomTom Geocode API)
  └─ Fetch Data from APIs
      ├─ Weather API (Rain Probability)
      └─ Traffic API (Delay in seconds)
  └─ Process & Normalize Data (0.0 → 1.0 scale)
  └─ Decision Logic
      ├─ Traffic High  → RED LED bright
      ├─ Rain High     → YELLOW LED bright
      └─ Safe          → GREEN LED bright
  └─ PWM Output Control (Pulsing Glow Effect)
  └─ Delay (Sleep)
  └─ LOOP (Repeat)
```

### Input / Output Map

| System Part | Type | What It Does |
|-------------|------|-------------|
| Weather API | Input | Provides rain probability |
| Traffic API | Input | Provides traffic delay |
| Raspberry Pi | Processing | Executes logic and controls GPIO |
| Python Script | Processing | Handles data processing |
| LEDs (R/Y/G) | Output | Display conditions via brightness |
| Power Supply | Support | Provides system power |

---

## 🖥️ Demo

**Terminal Output:**
```
--- Fetching New Data ---
[Traffic] Travel: 39.7 min | Delay: 0.0 min
Rain Chance : 0%
Traffic Delay: 0.0 min
  -> RED 0% | YELLOW 0% | GREEN 100%
```

*Pulsing Glow running | Wiring: GPIO17/27/22 → 220ohm → LEDs → Pin6 GND*

---

## ⚙️ Electronics

### Components Used

| Component | Quantity | Purpose |
|-----------|----------|---------|
| Raspberry Pi 4B | 1 | Main controller |
| LEDs (Red, Yellow, Green) | 3 | Output indicators |
| Resistors (220/330 Ohm) | 3 | Current limiting |
| Breadboard | 1 | Prototyping |
| Jumper Wires | Multiple | Connections |

### Wiring Plan

| GPIO Pin | LED Color | Function |
|----------|-----------|----------|
| GPIO 17 | 🔴 Red | Traffic intensity |
| GPIO 27 | 🟡 Yellow | Rain probability |
| GPIO 22 | 🟢 Green | Safe conditions |

All LED cathodes share a **common ground** connected to a GND pin on the Raspberry Pi. Each LED is connected in series with a current-limiting resistor.

### Circuit Description

```
GPIO17 ──[220Ω]──► RED LED ──┐
GPIO27 ──[220Ω]──► YEL LED ──┤── GND (Pin 6)
GPIO22 ──[220Ω]──► GRN LED ──┘
```

### Power Plan

| Parameter | Value |
|-----------|-------|
| Power Source | 5V USB supply |
| GPIO Voltage | 3.3V output |
| Current Safety | Limited via resistors |

### Dimensions

| Dimension | Value |
|-----------|-------|
| Length | 12 cm |
| Width | 10 cm |
| Height | 5 cm |
| Estimated Weight | 300 g |

---

## 💻 Software

### Tools & Libraries

| Tool / Platform | Purpose |
|----------------|---------|
| Python 3 | Main programming language |
| `gpiozero` | GPIO and PWM LED control |
| `requests` | API HTTP communication |
| `math` | Sine-wave pulsing animation |
| Raspberry Pi OS | Execution platform |

### Software Logic

**Startup Behavior:**
The Raspberry Pi boots and auto-launches the main Python script. It initializes GPIO pins 17, 27, and 22 for PWM via `gpiozero`, then runs a brief startup LED animation (RED → YELLOW → GREEN) to verify hardware.

**Data Fetching:**
- **OpenWeatherMap API** → rain probability (0–100%)
- **TomTom Distance Matrix API** → traffic delay in seconds on a predefined route

**Decision Logic:**
```python
# Normalize values to 0.0 – 1.0 scale
traffic_level = min(delay_seconds / MAX_DELAY, 1.0)
rain_level    = rain_percent / 100.0
safe_level    = max(0.0, 1.0 - traffic_level - rain_level)

# Apply to LEDs
red_led.value    = traffic_level
yellow_led.value = rain_level
green_led.value  = safe_level
```

**Error Handling:**
If internet drops or API times out, `try-except` blocks prevent crashes. The system enters a low-pulsing standby state and retries on the next loop iteration.

---

## 📦 Bill of Materials

| Item | Qty | Estimated Cost | Spec | Why This Choice |
|------|-----|---------------|------|----------------|
| Raspberry Pi 4B | 1 | ₹0 (Available) | 4B Model | Processing & WiFi |
| LEDs (R, Y, G) | 3 | ₹30 | Standard 5mm | Visual indication |
| Resistors | 3 | ₹30 | 220/330 Ohm | Current limiting |
| Breadboard | 1 | ₹10 | Half-size | Prototyping |
| Jumper Wires | Pack | ₹100 | Male-to-Male | Interconnections |
| **Total** | | **₹170** | | |

---

## 📋 Project Planning

### Task Breakdown

| Task ID | Task | Owner | Est. Hours | Status |
|---------|------|-------|-----------|--------|
| T1 | Logic, Software Architecture, Electronics | Kalpesh | 2 hrs | ✅ Done |
| T2 | Python Coding & API Integration | Shikhar | 4 hrs | ✅ Done |
| T3 | Documentation | Sonali | 3 hrs | ✅ Done |
| T4 | Documentation & Testing | Ayush | 2 hrs | ✅ Done |

### Build Milestones

| Bi-Hour | Goal | Outcome |
|---------|------|---------|
| Hour 1–2 | Plan & De-risk | Idea locked, BOM done, APIs tested |
| Hour 3–4 | Build Subsystems | GPIO tested, API data fetched, PWM logic working |
| Hour 5–6 | Integrate | Full loop running: API → logic → LEDs lit |
| Hour 7–8 | Refine & Finish | Bug fixes, smoothing added, docs complete |

### Update Log

| Day | Planned Goal | What Happened | Changes Made |
|-----|-------------|---------------|-------------|
| Day 1 | Hardware & code setup | Hardware & code setup completed | None |
| Day 2 | Documentation | Documentation done; hardware delayed | Awaited parts |
| Day 3 | Final integration | Final integration & testing done | None |

---

## ⚠️ Risks

| Risk | Likelihood | Impact | Mitigation | Owner |
|------|-----------|--------|-----------|-------|
| API failure | Low | High | Set default safe values | Shikhar |
| Internet drops | Medium | Medium | Retry mechanism in code | Shikhar |
| Hardware fault | Low | Medium | Proper testing, stable connections | Kalpesh |

---

## 🧪 Testing

### Test Plan

| What Needs Testing | How | Success Condition |
|-------------------|-----|------------------|
| LED Hardware | Manual GPIO script | LEDs turn on/off correctly |
| API Fetching | Print data to console | Accurate JSON values returned |
| PWM Logic | Observe brightness | Smooth variation reflecting data |

### Debugging Log

| Date | Problem | Type | Fix Applied | Result |
|------|---------|------|-------------|--------|
| Day 3 | GPIO pin mismatches | Hardware | Re-wired breadboard | ✅ Resolved |
| Day 3 | Harsh LED transitions | Code | Adjusted brightness scaling | ✅ Resolved |

---

## 🏁 Final Outcome

### What Works Well
- ✅ Real-time response to live API data
- ✅ Simple, passive, and intuitive visual design
- ✅ Low-cost implementation (under ₹200)
- ✅ Continuous autonomous operation

### What Needs Improvement
- Further brightness smoothing transitions (exponential moving average)
- Physical enclosure for permanent mounting

### What Changed from Original Plan
The system was slightly simplified to focus on core stability and reliable API functionality rather than adding stretch features like a web interface or data logging.

---

## 💭 Reflections

**Team:** Effective coordination enabled timely completion despite minor hardware constraints and API rate-limit challenges.

**Technical:** Gained practical experience in live API integration, stable GPIO control, and designing logic for continuous real-time execution.

**Design:** Simplicity vastly enhances usability. Physical feedback is often faster to process than a digital dashboard.

**If we had one more hour:** We would implement exponential moving average smoothing for graceful LED fading and build a small cardboard enclosure.

---

## ✅ Final Submission Checklist

- [x] Team details complete
- [x] Project description complete
- [x] Inspiration sources included
- [x] System architecture documented
- [x] BOM complete
- [x] Budget summary complete
- [x] Code flowchart added
- [x] Task breakdown complete
- [x] Update log current
- [x] Risk register complete
- [x] Testing log updated
- [x] Build photos included
- [x] Final reflection written

---

## 🔗 APIs Used

- [TomTom Developer Distance Matrix API](https://developer.tomtom.com/routing-api/documentation/tomtom-maps/product-information/introduction)
- [OpenWeatherMap API](https://openweathermap.org/api)

---

*Made with ❤️ by Team ElectroBoom | SKILL LAB Practical Hackathon*
