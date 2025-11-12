# Real-Time Geodetic NMPC CaaS UAV Framework

### [Public Portfolio Version - Master's Thesis]

Licensed under a custom Academic/Commercial license. See LICENSE.md for details.

This repository showcases the architecture of a high-performance, **Dockerized** framework for advanced UAV autonomy. The project was developed as a Master of Science M.S.c. Thesis at the  ** University of Applied Sciences of  Karlsruhe (H-KA)** in cooperation with the **Fraunhofer Institute of Optronics, System Technologies and Image Exploitation (IOSB)** in Karlsruhe , Germany.

This framework is a standalone **"Controller-as-a-Service" (CaaS)** platform, built from the ground up in Python and C++, designed for real-world, long-range Geodetically corrected autonomous missions.

## 1. A Full-Stack Architecture

This project demonstrates a unique "full-stack" profile, bridging three key domains:

### Pillar 1: Robotics & Advanced Control ("Autonomous-Pilot")
* **Advanced Control:** Implements a suite of **NMPC (Nonlinear Model Predictive Control)** controllers for high-performance trajectory optimization.
* **Geodetic-Aware Controller:** A 17-state controller operating in the **ECEF** (Earth-Fixed) frame, compensating for Earth's rotation (Coriolis Effect) for long-range navigation.
* **Local Controller:** A 13-state controller operating in the **ENU** frame, optimized for local, high-speed maneuvers with integrated **obstacle avoidance  & Target Interception**.
* **Real-Time Solvers:** Uses **Acados & CasADi** to auto-generate high-speed C-code solvers, enabling sub-20 ms control loops.
* **Motor lag modeling:** Modeled motor lag for realism of the motor dynamics of the UAV

### Pillar 2: Geomatics & Estimation ("Navigator")
* **High-Fidelity State Estimation:** A **23-state Unscented Kalman Filter (UKF)** provides robust, real-time GPS/IMU sensor fusion and bias estimation.
* **Geodetic Intelligence:** The framework is **geodetically-aware**. It actively corrects for altitude using the **EGM96 geoid model**, enabling precise navigation in global coordinate systems.

### Pillar 3: Backend & DevOps ("Engine")
* **"Controller-as-a-Service" API:** The entire control system is served via a **FastAPI (REST)** backend. This allows any external client (a Digital Twin, a mission planner, or a ground station) to request and command the controllers in real-time.
* **Containerization:** The framework (including all complex scientific dependencies) is 100% **Dockerized** for instant, reproducible deployment on any system.

## 2. Key Validation Mission (Conceptual)

The framework's primary validation was a simulated **105km (Karlsruhe to Freiburg)** autonomous flight. This mission successfully proved the CaaS architecture's ability to:
* Maintain a stable track over a 1.4-hour flight.
* Handle geodetic-scale navigation (compensating for Coriolis and EGM96 geoid).
* Execute over **100,000 real-time optimization steps without a single failure**.

## 3. Tech Stack

* **Control & Simulation:** Python, C++, NMPC, **Acados**, **CasADi**, UKF, NumPy
* **Backend & DevOps:** **Docker**, **FastAPI**, REST APIs, CI/CD
* **Geospatial / Geomatics:** PyProj, Rasterio, EGM96 Geoid Model
* **Visualization Frontend:** Dash, Plotly, Leaflet.js
