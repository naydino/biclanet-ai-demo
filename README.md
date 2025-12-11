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


🤖 ML & AI Components
1️⃣ ML Predictions – predictions.json

This file represents the output of our ML model (for now, simulated):

Each item looks like:

{
  "pod_id": "POD-GCT-001A",
  "timestamp": "2025-12-10T09:00:00Z",
  "occupancy_rate": 0.78
}


occupancy_rate is a 0–1 value (0%–100% predicted usage)

Multiple timestamps per pod let us show a time-based forecast

In dashboard.js we:

Load this file with fetch("predictions.json")

Compute the average occupancy to get Predicted Usage (24h)

Render:

The percentage value

A colored usage bar

A series of small forecast bars

Pass the average value into the p5.js sketch:

if (window.setActivityLevel) {
  window.setActivityLevel(avg); // avg is 0–1
}


So the animation reflects the same ML predictions as the numeric metric.

2️⃣ AI Recommendations – ai_optimizations.json

This file represents higher-level AI decision suggestions:

{
  "title": "Relocate Underused Pods",
  "description": "Pods in Olaias show low turnover. Move 2 pods to Moscavide to capture unmet demand.",
  "impact": "+18% Revenue"
}


In dashboard.js we load the file and render a card for each entry:

Title → headline of the recommendation

Description → quick explanation of the reasoning

Impact → expected metric change (revenue, utilization, downtime)

This panel is your “strategy layer” on top of the raw predictions.

3️⃣ Live System Activity – system-activity.js (p5.js)

This is the creative coding component.

A p5.js sketch renders a horizontal band inside #systemActivityCanvas

Small “packets” of light move across the band

Their speed and vertical movement are controlled by activityLevel,
which is derived from predicted usage:

let activityLevel = 0.5;

window.setActivityLevel = function (level) {
  activityLevel = level; // 0–1 based on ML predictions
};


Higher predicted usage → more intense, restless animation.
Lower predicted usage → calmer, slower animation.

This connects the aesthetic component directly to ML data, demonstrating
“AI as a visual, living system” instead of only numbers.

The sketch can easily be swapped out for any other visualization if the team wants to experiment with different concepts.

4️⃣ Live AI Activity Log

In the AI panel we show a small “Live AI Activity” section.
Every few seconds, a new log line appears, e.g.:

Updated forecast for POD-GCT-001A · 82% expected occupancy

Recomputing comfort scores for IADE cluster…

Checking anomaly risk for night-time voltage drops…

Implementation idea (simplified):

function startAIActivity(predictions) {
  const list = document.getElementById("aiActivityList");
  const events = [
    // built from predictions + some static strings
  ];

  function addNext() {
    // create <li>, animate in, trim list length
  }

  addNext();
  setInterval(addNext, 2500);
}


This gives the feeling that the AI system is constantly working in the background,
even though we’re using simulated events.



🔁 How to Change / Replace the Simulated Data
🔹 Update ML predictions

Edit predictions.json:

- Add/remove entries

- Change occupancy_rate values (0–1)

- Keep the fields: pod_id, timestamp, occupancy_rate

When you save and refresh the page:

-Predicted Usage (24h) changes

-Small forecast bars update

-System Activity visualization becomes calmer or more active

-Perfect place for Inge to plug in her own model outputs.

🔹 Update AI recommendations

Edit ai_optimizations.json:

- Adjust titles

- Rewrite descriptions

- Change impact strings

 - The “AI Optimizations” panel will reflect the new content.

🌐 Connection to Main Group Repo

Main project repo:
👉 https://github.com/i-n-a/cicla-ecopod



🔮 Future Work & Extensions

Some directions we can take next:

1. Firebase Integration

Replace fetch("predictions.json") with Firebase listeners, e.g.:

onValue(ref(db, "predictions"), (snapshot) => {
  const predictions = snapshot.val();
  renderPredictedUsage(predictions);
  // other render functions...
});


This would turn the dashboard into a live operator view.


3. AI Chatbot Integration

- Add a “Ask BiclaNet AI” panel using:

- OpenAI Assistants API or similar

- Context from pods, predictions, and user inputs

Example questions:

- “Where should we relocate underused pods next week?”

- “Why is IADE cluster showing anomalies after 21:00?”

- “Summarize today’s usage vs forecast.”

4. More Advanced ML

Later sprints could include:

- Time-series models for hourly demand

- Weather-based usage prediction

- Anomaly detection for:

- power issues

- unusual lock events

- abnormal occupancy patterns


This demo is a shared sandbox for the AI/ML layer of BiclaNet.
