**Capstone Project | Summer Analytics 2025  
Consulting & Analytics Club × Pathway**

This project presents a real-time dynamic pricing engine for urban parking spaces. 
The system uses streaming data to adjust prices in real time, based on demand, traffic, queue length, vehicle type, and competitor behavior. 
The solution is implemented entirely in Python using `numpy`, `pandas`, and `Pathway`, with live visualization via `Bokeh`.

## Overview

Urban parking demand fluctuates throughout the day, yet prices are often static, leading to inefficiencies such as overutilization or underutilization. 
This project simulates a real-time pricing system that reacts dynamically to:

- Historical occupancy patterns  
- Queue lengths  
- Environmental conditions (traffic and events)  
- Vehicle type  
- Nearby competitor prices

Three pricing models are implemented:
1. **Model 1:** Linear Pricing  
2. **Model 2:** Demand-Based Pricing  
3. **Model 3:** Competitive Pricing with Geospatial Awareness

## Tech Stack

| Category        | Tools Used                             |
|----------------|-----------------------------------------|
| Language        | Python 3.x                              |
| Data Handling   | `pandas`, `numpy`                       |
| Streaming       | `Pathway`                               |
| Visualization   | `bokeh`, `panel`                        |
| Execution       | Google Colab                            |
| Architecture    | Event-based streaming with replay       |

**Architecture & Workflow Explanation**

**1. Data Ingestion**
The system begins with a dataset (dataset.csv) containing 14 parking lots' data across 73 days.
Data is streamed using pw.demo.replay_csv() at 100 rows/second to simulate real-time input.

**2. Feature Engineering**
Key features are extracted and engineered:
OccupancyRate = Occupancy / Capacity
TrafficLevel: Encoded as low=0.3, average=0.6, high=1.0
VehicleWeight: Mapped from type (e.g., truck=1.0, bike=0.3)

**3. Pricing Models**
Model 1 – Linear Baseline
Price increases linearly with occupancy.
Acts as a reference point.

**Model 2 – Demand-Based**
Calculates a composite demand score based on:
Occupancy rate (40%)
Queue length (20%)
Traffic level (20%)
Vehicle weight (10%)
Special day (10%)

**Model 3 – Competitive Pricing**
Uses Haversine distance to find nearby competitors.
If a competitor is within 500m and has a lower price, and current occupancy > 90%:

**4. Real-Time Execution**
Pathway processes the stream.
Features and models are applied in real time.
The final price is emitted continuously.

**5. Visualization**
Bokeh plots dynamically display:
Price trends over time
Comparison with competitor prices
Panel makes the dashboard servable in notebooks or apps.

**Core Features:**
Real-time demand scoring
Location-aware pricing adjustments
Continuous visualization
Fully explainable and bounded pricing logic
Google Colab compatible, lightweight implementation
