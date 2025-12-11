# Autonomous Car for Road Penalties

A real-time, edge-to-cloud traffic-monitoring platform designed for autonomous-vehicle supervision, intelligent traffic enforcement, and automated road-penalty assessment. The system integrates **YOLOv8 detection**, **Raspberry Pi edge processing**, **Flask backend services**, and a **modern web dashboard** for visualization and analytics.

---

## Key Features

### Edge Intelligence (Raspberry Pi)

* Real-time YOLOv8 vehicle detection and motion tracking
* Object classification (car, bus, motorcycle, truck, bicycle)
* Virtual line-crossing logic for accurate vehicle counting
* Live visual overlay for debugging and monitoring

### Backend API & Storage

* Flask REST API for receiving detection payloads
* SQLite database for persistent event logging
* Endpoints for latest status, history retrieval, and system reset
* Modular architecture for future enforcement logic

### Interactive Web Dashboard

* Live visualization of motion, vehicle count, timestamps, and detection payloads
* Dark/Light theme toggling
* Downloadable JSON reports
* In-browser session history
* Motion alert UI overlay

---

## System Architecture

```
+-------------------+        Wi-Fi/LAN        +------------------------+
|   Raspberry Pi    | ---------------------> |     Flask Backend      |
| YOLOv8 Detection  | JSON payloads (1s)     |  /send /latest /history|
+-------------------+                        +-----------+------------+
        |                                                 |
        | Local video preview                             | SQLite DB
        |                                                 v
        |                                        +--------------------+
        |                                        |   traffic.db       |
        |                                        +--------------------+
        |
        v
+--------------------------------------------------------------+
|                     Web Dashboard (index.html)               |
| Live status, vehicle count, JSON details, reports, controls  |
+--------------------------------------------------------------+
```

---

## Repository Structure

```
/index.html      → Web dashboard UI  
/server.py       → Flask backend (API + database)  
/yolo_pi.py      → Raspberry Pi YOLOv8 detection client  
/traffic.db      → SQLite DB (auto-created)  
```

---

## Installation & Setup

### 1. Raspberry Pi (YOLO Client)

```
pip install ultralytics opencv-python requests
python yolo_pi.py
```

Ensure `BACKEND_URL` in `yolo_pi.py` points to your server IP.

### 2. Backend Server

```
pip install flask sqlite3
python server.py
```

### 3. Dashboard

Open in browser:

```
http://<server-ip>:5000/
```

---

## API Endpoints

| Endpoint           | Method | Purpose                       |
| ------------------ | ------ | ----------------------------- |
| `/send`            | POST   | Receive YOLO detection packet |
| `/latest`          | GET    | Return latest event state     |
| `/history?limit=N` | GET    | Fetch recent detections       |
| `/reset`           | POST   | Reset live metrics            |
| `/clear_history`   | POST   | Clear database logs           |

---

## Detection Payload Structure

Example JSON sent from Raspberry Pi:

```json
{
  "timestamp": "2025-01-01T12:00:00",
  "motion_detected": true,
  "vehicle_count": 14,
  "vehicles": [
    {
      "id": 5,
      "type": "car",
      "confidence": 0.92,
      "bbox": [120, 150, 200, 280],
      "center": [160, 215]
    }
  ]
}
```

---

## Potential Extensions

* Speed estimation and automated speeding penalties
* License Plate Recognition (LPR) integration
* Multi-camera vehicle tracking
* Cloud syncing (AWS/GCP/Azure)
* AI-driven violation classification
* Integration with autonomous-car routing and safety systems

