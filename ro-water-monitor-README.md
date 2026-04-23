# 💧 RO Water Monitoring Device

<div align="center">

**Real-time water quality monitoring system for Reverse Osmosis (RO) units**

![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![IoT](https://img.shields.io/badge/IoT-Sensors-00BCD4?style=flat-square)
![Status](https://img.shields.io/badge/Status-Prototype-green?style=flat-square)

</div>

---

## 📌 Overview

The **RO Water Monitoring Device** is a prototype IoT system that continuously monitors the water quality of a Reverse Osmosis (RO) purification unit. It reads data from multiple sensors, processes it in real-time using Python, and alerts the user when water quality drops below safe thresholds.

The system monitors parameters like **TDS (Total Dissolved Solids)**, **pH**, **temperature**, and **flow rate** — giving users confidence in their drinking water quality.

---

## 🎯 Problem Statement

Most home RO units give no feedback on:
- Whether the output water is actually clean
- When the filter needs replacing
- Real-time water quality metrics

**Our solution:** An affordable sensor-based monitoring device that tracks water quality in real-time and sends alerts when values go out of range.

---

## 🏗️ System Architecture

```
┌──────────────┐    ┌──────────────┐    ┌──────────────┐
│  TDS Sensor  │    │   pH Sensor  │    │  Flow Meter  │
└──────┬───────┘    └──────┬───────┘    └──────┬───────┘
       │                   │                   │
       └───────────────────┼───────────────────┘
                           │ Sensor Data (Analog/Digital)
                           ▼
               ┌───────────────────────┐
               │    Microcontroller    │
               │  (Arduino / RPi)      │
               └───────────┬───────────┘
                           │ Serial / GPIO
                           ▼
               ┌───────────────────────┐
               │   Python Data Layer   │
               │  - Data acquisition   │
               │  - Processing/alerts  │
               │  - Logging to CSV     │
               └───────────┬───────────┘
                           │
                           ▼
               ┌───────────────────────┐
               │   Display / Alerts    │
               │  (LCD Screen / LED /  │
               │   Console Interface)  │
               └───────────────────────┘
```

---

## ⚙️ Monitored Parameters

| Parameter | Safe Range | Sensor Used |
|-----------|-----------|-------------|
| TDS (Total Dissolved Solids) | < 500 ppm | TDS Sensor |
| pH Level | 6.5 – 8.5 | pH Sensor |
| Water Temperature | 10°C – 30°C | DS18B20 |
| Flow Rate | > 0.5 L/min | Flow Meter Sensor |

---

## 🛠️ Technologies Used

- **Python** — Data acquisition, processing, and alert logic
- **IoT Sensors** — TDS, pH, temperature, flow sensors
- **Microcontroller** — Arduino / Raspberry Pi for interfacing sensors
- **CSV Logging** — Historical data tracking
- **Serial Communication** — Python ↔ Microcontroller data transfer

---

## 📁 Project Structure

```
ro-water-monitor/
│
├── src/
│   ├── main.py           # Main monitoring loop
│   ├── sensor_reader.py  # Reads raw data from sensors via serial
│   ├── data_processor.py # Converts raw values to readable units
│   ├── alert_system.py   # Triggers alerts based on thresholds
│   └── data_logger.py    # Logs readings to CSV
│
├── data/
│   └── readings_log.csv  # Sample data output
│
├── docs/
│   └── wiring_diagram.png
│
├── requirements.txt
└── README.md
```

---

## 💻 Core Logic (Python)

```python
# data_processor.py - Process and validate sensor readings

SAFE_LIMITS = {
    "tds_ppm":    (0, 500),
    "ph":         (6.5, 8.5),
    "temp_c":     (10, 30),
    "flow_lpm":   (0.5, float('inf'))
}

def is_within_safe_range(parameter, value):
    """Returns True if the value is within the safe range."""
    low, high = SAFE_LIMITS[parameter]
    return low <= value <= high

def generate_report(readings: dict) -> dict:
    """Generates a status report from sensor readings."""
    report = {}
    for param, value in readings.items():
        status = "✅ SAFE" if is_within_safe_range(param, value) else "⚠️ ALERT"
        report[param] = {"value": value, "status": status}
    return report


# alert_system.py - Alert user when thresholds are breached

def check_and_alert(readings):
    """Prints alerts for any parameter outside safe limits."""
    report = generate_report(readings)
    for param, info in report.items():
        if "ALERT" in info["status"]:
            print(f"[ALERT] {param} is {info['value']} — outside safe range!")
```

---

## 📊 Sample Output

```
===== RO Water Quality Monitor =====
Timestamp   : 2025-04-15 10:32:45
TDS         : 342 ppm      ✅ SAFE
pH          : 7.2           ✅ SAFE
Temperature : 24.5 °C      ✅ SAFE
Flow Rate   : 0.8 L/min    ✅ SAFE
=====================================
All parameters are within safe limits.
```

---

## 🚀 How to Run

```bash
# Clone the repository
git clone https://github.com/ayush7984/ro-water-monitor.git
cd ro-water-monitor

# Install dependencies
pip install -r requirements.txt

# Run with simulated sensor data
python src/main.py --mode demo

# Run with real hardware (specify serial port)
python src/main.py --port COM3
```

---

## 📈 Future Improvements

- [ ] Web dashboard for live monitoring (Flask/Streamlit)
- [ ] SMS/email alerts when quality drops
- [ ] Machine learning to predict filter replacement schedule
- [ ] Mobile app integration via Bluetooth
- [ ] Cloud data logging for trend analysis

---

## 🤝 Contributing

Pull requests are welcome! Please open an issue first for major changes.

---

## 👤 Author

**Ayush Mishra**
- 📧 [ayush7984k@gmail.com](mailto:ayush7984k@gmail.com)
- 🔗 [LinkedIn](https://linkedin.com/in/ayush7984)
- 🐙 [GitHub](https://github.com/ayush7984)

---

<div align="center">

*B.Tech CSE (AI/ML) · Lovely Professional University*

⭐ Star this repo if you found it useful!

</div>
