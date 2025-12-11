# Autonomous-Car-for-Road-Penalties
A real-time, edge-to-cloud traffic-monitoring platform designed for autonomous-vehicle supervision, intelligent traffic enforcement, and automated road-penalty assessment. The system integrates YOLOv8 detection, Raspberry Pi edge processing, Flask backend services, and a modern web dashboard for visualization and analytics.

# Key Features
Edge Intelligence (Raspberry Pi)

Real-time YOLOv8 vehicle detection and motion tracking

Object classification (car, bus, motorcycle, truck, bicycle)

Virtual line-crossing logic for accurate vehicle counting

Live visual overlay for debugging and monitoring

Backend API & Storage

Flask REST API for receiving detection payloads

SQLite database for persistent event logging

Endpoints for latest status, history retrieval, and system reset

Modular architecture for future enforcement logic

Interactive Web Dashboard

Live visualization of motion, vehicle count, timestamps, and detection payloads

Dark/Light theme toggling

Downloadable JSON reports

In-browser session history

Motion alert UI overlay
