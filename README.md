# 🚲 BiclaNet – AI-Assisted Dashboard Demo (Milestone 2)
*IADE – Creative Computing & Artificial Intelligence (2025)*

This repo contains a **frontend-only AI dashboard demo** that shows how our group integrates:

- ✅ **ML predictions** (simulated data)
- ✅ **AI insights & recommendations**
- ✅ **Creative visualizations (p5.js)**

into the **BiclaNet** operator dashboard for **Milestone 2**.

---

## 🎯 Project Goal (Milestone 2)

Milestone 2 asks us to:

- Build a **small ML model** on simulated or collected data  
- Show how this model **interacts with our system**  
- Implement **AI logic** that generates meaningful insights  
- Use **creative coding** to visualize those insights

This demo does exactly that by:

1. Loading **predicted occupancy data** from `predictions.json`
2. Computing **Predicted Usage (24h)** and a **mini forecast**
3. Displaying **AI Optimization** suggestions from `ai_optimizations.json`
4. Driving a **p5.js “Live System Activity” visualization** from ML outputs
5. Showing a **Live AI Activity log** that simulates ongoing inference work

All of this runs **locally in the browser** with no backend.

---

## 🧩 Overview of the Demo

### What you see on the dashboard

- **Top cards**
  - Total pods
  - Active / Offline counts
  - Firebase & API status (simulated)
  - **Predicted Usage (24h)** — driven by ML predictions

- **Live System Activity (real-time)**
  - A glowing band animated with **p5.js**
  - Motion speed and amplitude are controlled by **predicted occupancy**

- **Live Pod Status table**
  - Sample pods with:
    - Last sync time
    - Location
    - Status (online / offline / maintenance)
    - Occupancy

- **AI Optimizations panel**
  - Loaded from `ai_optimizations.json`
  - Shows AI-generated recommendations and expected impact

- **Live AI Activity**
  - Text log where new “AI events” animate in every few seconds
  - Simulates ongoing inference tasks in the background

---

## 📁 Folder Structure

```bash
biclanet-ai-demo
│
├── index.html               # Main AI dashboard
├── style.css                # Dashboard styling
├── dashboard.js             # ML + AI logic and DOM rendering
├── system-activity.js       # p5.js "Live System Activity" visualization
│
├── predictions.json         # Simulated ML predictions (pod occupancy)
├── ai_optimizations.json    # Simulated AI recommendations
│
└── app.html                 # Placeholder for Rider App AI screen (future work)


