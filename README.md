
---

# 🧠 Advanced Chest Infection vs Pneumonia Diagnostic Tool

An **AI-inspired, multi-modal respiratory diagnostic web application** that integrates:

* Symptom-based weighted inference
* Risk factor modeling
* Simulated wearable biometrics
* Lung sound + cough analysis
* Interactive data visualisation
* Voice, audio, and chatbot interfaces

This tool is designed as a **research-grade prototype for digital health diagnostics**, combining frontend engineering with heuristic clinical reasoning.

---

## 🚀 Core Features

### 🩺 Diagnostic Engine

* Weighted scoring model for:

  * Chest Infection (Bronchitis)
  * Pneumonia
* Dynamic scoring adjustments using:

  * Symptoms
  * Risk factors
  * Simulated wearable data
  * Lung sound analysis
* Output classification:

  * Chest Infection leaning
  * Pneumonia leaning
  * Inconclusive

---

### 📊 Data Visualisation (Chart.js)

| Chart Type      | Purpose                        |
| --------------- | ------------------------------ |
| **Bar Chart**   | Absolute weighted scores       |
| **Radar Chart** | Normalised symptom proportions |
| **Pie Chart**   | Risk factor contribution       |
| **Line Chart**  | Historical evaluation trends   |

All charts are:

* Real-time updated
* State-persistent
* Fully resettable

---

### ⌚ Wearable Simulation Layer

Simulated biometric inputs:

* Heart Rate
* Body Temperature
* Respiration Rate
* Oxygen Saturation (SpO₂)

Dynamic influence:

* Elevated temperature → increases pneumonia weighting
* Low lung sound score → increases pneumonia likelihood

---

### 🎤 Audio & Voice Systems

#### Cough Recording (Web Audio API)

* 5-second microphone capture
* Simulated cough severity scoring

#### Voice Command System

* Speech-to-text via Web Speech API
* Automatically selects symptoms based on spoken input

#### Text-to-Speech Output

* Reads diagnostic result aloud

---

### 🤖 Chatbot Assistant

* Lightweight rule-based conversational system
* Context-aware responses:

  * “What” → clinical advice
  * “Why” → explanation of model
  * fallback → evaluation summary

---

### 🧾 Reporting & Export

| Format | Description                 |
| ------ | --------------------------- |
| TXT    | Full report                 |
| PDF    | Structured export via jsPDF |
| CSV    | Historical trend dataset    |

Includes:

* Symptoms
* Risk factors
* Score output
* Timestamp

---

### 🧠 Personal Health Journal

* Persistent entries (localStorage)
* Timestamped logs
* Export to TXT

---

### ⚙️ Advanced Settings System

* Real-time tuning of:

  * Symptom weights
  * Pneumonia weights
  * Risk factor weights
* Immediate recalculation on save

---

### 🌗 UI / UX Features

* Dark mode (persistent)
* Responsive layout
* Animated news ticker
* Modal-based settings panel
* Toggleable health journal

---

### 🔔 Smart Notifications

* Periodic browser reminders to re-evaluate symptoms

---

### 📡 Sharing Features

* Web Share API integration
* Twitter/X sharing support

---

## 🧪 Diagnostic Methodology

The system uses a **heuristic weighted inference model**:

```
Total Score = Σ(Symptom Weights) + Σ(Risk Factors) + Dynamic Signals
```

Dynamic modifiers:

* Temperature > 37°C → Pneumonia++
* Lung score < 5 → Pneumonia++
* Risk stacking → Amplified severity

Trend tracking:

```
Score Difference = Pneumonia - Chest Infection
```

Stored over time for longitudinal analysis.

---

## 🛠️ Tech Stack

| Layer      | Technology              |
| ---------- | ----------------------- |
| Frontend   | HTML5, CSS3, Vanilla JS |
| Charts     | Chart.js                |
| PDF Export | jsPDF                   |
| Audio      | Web Audio API           |
| Voice      | Web Speech API          |
| Storage    | localStorage            |

---

## 📂 Project Structure

```
/project-root
│
├── index.html   # Full application (all logic embedded)
├── README.md    # Documentation
```

---

## ⚠️ Disclaimer

This tool is:

* ❌ NOT a medical device
* ❌ NOT clinically validated
* ❌ NOT a substitute for professional diagnosis

It is intended for:

* Educational purposes
* Prototyping
* Research and experimentation

---

## 🔬 Future Enhancements

Planned improvements:

* Real ML model integration (TensorFlow.js)
* Real audio classification (cough CNN)
* API-based health data ingestion
* Doctor dashboard + patient profiles
* Cloud sync + authentication
* Real-time anomaly detection

---

## 📸 Preview Concept

*(Recommended to add screenshots or a demo GIF here in your repo)*

---

## 📜 License

MIT License – free to use, modify, and distribute.

---

## 👨‍💻 Author

Developed by **Kai Piper**
Focused on:

* AI systems
* Simulation environments
* Digital health innovation

---

## ⭐ Contribution

Pull requests, forks, and feature suggestions are welcome.

---

## 💡 Summary

This project is essentially a **hybrid between:**

* Clinical decision support system
* Interactive health dashboard
* Experimental AI diagnostic model

It demonstrates how **multi-modal data fusion** can be implemented purely in the browser.

---

