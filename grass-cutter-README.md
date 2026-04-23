# 🌿 Smart Solar Grass Cutter

<div align="center">

**An autonomous solar-powered robotic grass cutter with obstacle detection**

![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![IoT](https://img.shields.io/badge/IoT-Hardware-orange?style=flat-square)
![Solar](https://img.shields.io/badge/Powered-Solar%20Energy-yellow?style=flat-square)
![Status](https://img.shields.io/badge/Status-Prototype%20%2F%20Conceptual-blue?style=flat-square)

</div>

---

## 📌 Overview

The Smart Solar Grass Cutter is a conceptual robotics project that combines **renewable energy** with **autonomous movement logic**. The robot is designed to navigate a lawn, detect obstacles, and cut grass — all powered by solar energy, making it eco-friendly and low-maintenance.

This project explores the fundamentals of:
- Autonomous robot navigation
- Obstacle detection using sensors
- Solar energy integration for embedded systems
- Python-based control logic

---

## 🎯 Problem Statement

Traditional grass cutters require manual operation or rely on battery/fuel-powered motors. They are:
- Energy-inefficient and environmentally unfriendly
- Require constant human supervision
- High maintenance

**Our solution:** An autonomous grass cutter that runs on clean solar energy and navigates on its own.

---

## 🏗️ System Architecture

```
┌─────────────────────────────────────────────┐
│              Solar Panel                    │
│         (Power Generation Unit)             │
└───────────────────┬─────────────────────────┘
                    │ Power
                    ▼
┌─────────────────────────────────────────────┐
│            Microcontroller                  │
│         (Central Processing Unit)           │
│                                             │
│   ┌─────────────┐    ┌──────────────────┐   │
│   │  Obstacle   │    │  Movement Logic  │   │
│   │  Detection  │───▶│  (Python-based)  │   │
│   │  (Sensors)  │    │                  │   │
│   └─────────────┘    └──────────────────┘   │
└───────────────────┬─────────────────────────┘
                    │ Commands
                    ▼
┌─────────────────────────────────────────────┐
│           Motor Drive Unit                  │
│      (Wheels + Cutting Blade)               │
└─────────────────────────────────────────────┘
```

---

## ⚙️ Features

| Feature | Description |
|---------|-------------|
| 🌞 Solar Powered | Uses solar panels — zero fuel cost |
| 🤖 Autonomous Movement | Navigates without human input |
| 🚧 Obstacle Detection | Detects and avoids obstacles using sensors |
| 🔄 Auto-Return | Returns to base when battery is low |
| 📊 Simple Interface | Basic status display and alerts |

---

## 🛠️ Technologies Used

- **Python** — Core control logic and decision-making
- **Microcontroller** — Embedded hardware control (concept: Arduino/Raspberry Pi)
- **Ultrasonic Sensors** — Obstacle detection (HC-SR04)
- **Solar Panel + Battery** — Power system
- **DC Motors + Motor Driver** — Movement and blade control

---

## 📁 Project Structure

```
smart-solar-grass-cutter/
│
├── src/
│   ├── main.py              # Entry point, main control loop
│   ├── movement.py          # Motor control and navigation logic
│   ├── obstacle_detector.py # Sensor reading and obstacle logic
│   └── power_manager.py     # Solar/battery monitoring
│
├── docs/
│   ├── system_diagram.png   # Architecture diagram
│   └── circuit_diagram.png  # Hardware wiring
│
├── tests/
│   └── test_movement.py     # Unit tests for movement logic
│
├── requirements.txt
└── README.md
```

---

## 💻 Core Logic (Python)

```python
# obstacle_detector.py - Simplified obstacle detection logic

import time

OBSTACLE_THRESHOLD_CM = 20  # Stop if object is within 20cm

def measure_distance(sensor):
    """Reads distance from ultrasonic sensor."""
    sensor.trigger()
    time.sleep(0.00001)
    duration = sensor.read_echo()
    distance_cm = (duration * 34300) / 2
    return distance_cm

def is_obstacle_detected(sensor):
    """Returns True if an obstacle is within the threshold."""
    distance = measure_distance(sensor)
    return distance < OBSTACLE_THRESHOLD_CM

# movement.py - Simplified movement logic

def navigate(motors, sensor):
    """Main navigation loop with obstacle avoidance."""
    while True:
        if is_obstacle_detected(sensor):
            motors.stop()
            motors.turn_right(90)   # Turn to avoid obstacle
        else:
            motors.move_forward()
        time.sleep(0.1)
```

---

## 🚀 How to Run (Simulation Mode)

```bash
# Clone the repository
git clone https://github.com/ayush7984/smart-solar-grass-cutter.git
cd smart-solar-grass-cutter

# Install dependencies
pip install -r requirements.txt

# Run in simulation mode
python src/main.py --mode simulation
```

---

## 📈 Future Improvements

- [ ] GPS-based boundary mapping
- [ ] Mobile app for remote control and monitoring
- [ ] Rain sensor to pause operation
- [ ] AI-based path optimization for efficient coverage
- [ ] Real-time camera feed for obstacle classification

---

## 🤝 Contributing

Pull requests are welcome! For major changes, please open an issue first to discuss what you'd like to change.

---

## 👤 Author

**Ayush Mishra**
- 📧 [ayush7984k@gmail.com](mailto:ayush7984k@gmail.com)
- 🔗 [LinkedIn](https://linkedin.com/in/ayush7984)
- 🐙 [GitHub](https://github.com/ayush7984)

---

<div align="center">

*B.Tech CSE (AI/ML) · Lovely Professional University*

⭐ Star this repo if you found it interesting!

</div>
