# 🚗 VisionDrive – AI-Powered Driver Monitoring System

VisionDrive is an AI-powered driver monitoring system designed to improve road safety by detecting driver fatigue, distraction, and mobile phone usage in real time.

The system uses computer vision and machine learning techniques to monitor driver behavior, calculate driving risk levels, and generate alerts to encourage safer driving.

## 🎯 Project Objectives

- Detect driver fatigue and drowsiness.
- Identify driver distraction through head movement and direction.
- Detect mobile phone usage while driving.
- Calculate an overall driving risk score.
- Generate real-time alerts for unsafe driving behavior.
- Store monitoring sessions and alert history in MongoDB.

## ✨ Key Features

### 1. Fatigue Detection
- Eye Aspect Ratio (EAR) calculation.
- Blink detection and prolonged eye closure detection.
- Percentage of Eye Closure (PERCLOS).
- Mouth Aspect Ratio (MAR) and yawning detection.
- Fatigue level classification.

### 2. Distraction Detection
- Head pose estimation.
- Detection of prolonged looking away from the road.
- Identification of head directions such as left, right, and up.

### 3. Mobile Phone Detection
- YOLO-based mobile phone detection.
- Identifies potential mobile phone usage while driving.

### 4. Risk Assessment
- Combines fatigue and distraction information.
- Calculates an overall driving risk score.
- Classifies risk into LOW, MODERATE, HIGH, and NOT_ASSESSED levels.

### 5. Real-Time Alert System
Generates alerts for:
- Drowsiness.
- Driver distraction.
- Mobile phone detection.
- High-risk driving conditions.

### 6. Session and Alert Management
- Stores monitoring sessions in MongoDB.
- Maintains session statistics and risk summaries.
- Stores alert messages, severity, and timestamps.
- Provides APIs to retrieve session and alert history.

## 🏗️ System Architecture

```text
              Driver Webcam
                    |
                    v
             Video Frame Input
                    |
          +---------+---------+
          |                   |
          v                   v
    Fatigue Detection   Distraction Detection
          |                   |
          |             Head Pose Detection
          |                   |
          |             Phone Detection
          |                   |
          +---------+---------+
                    |
                    v
             Risk Scoring Engine
                    |
                    v
              Alert Generation
                    |
          +---------+---------+
          |                   |
          v                   v
      WebSocket             MongoDB
          |                   |
          v                   v
   React Dashboard       Session History
                         Alert History
```

## 🛠️ Technology Stack

| Component | Technologies |
|---|---|
| Backend | Python, FastAPI |
| Computer Vision | OpenCV, MediaPipe |
| Machine Learning | YOLO, NumPy |
| Real-Time Communication | WebSockets |
| Database | MongoDB, PyMongo |
| API Documentation | FastAPI Swagger UI |
| Frontend | React.js |

## 📁 Project Structure

```text
VisionDrive/
│
├── backend/
│   ├── main.py
│   ├── database.py
│   ├── risk_scoring.py
│   │
│   ├── fatigue/
│   │   └── fatigue_detector.py
│   │
│   └── distraction/
│       ├── head_pose.py
│       ├── distraction_detection.py
│       ├── phone_detection.py
│       └── models/
│
├── test_fatigue.py
├── test_websocket.py
├── test_database.py
│
├── requirements.txt
├── .gitignore
└── README.md
```

*Note: The structure above highlights the main project files. Additional modules and model files may be present.*

## ⚙️ Installation and Setup

### Prerequisites

- Python 3.10 or later (use a version compatible with the installed dependencies).
- MongoDB Community Server.
- Git.
- Webcam.

### Step 1: Clone the Repository

```bash
git clone https://github.com/YOUR-USERNAME/VisionDrive.git
cd VisionDrive
```

### Step 2: Create a Virtual Environment

```bash
python -m venv .venv
```

Activate it on Windows:

```powershell
.venv\Scripts\activate
```

### Step 3: Install Dependencies

```bash
pip install -r requirements.txt
```

### Step 4: Start MongoDB

Make sure the MongoDB server is running locally.

The current backend database configuration uses:

```text
mongodb://localhost:27017/
```

Database name:

```text
visiondrive
```

Collections:
- monitoring_sessions
- alerts

### Step 5: Run the Backend

```bash
uvicorn backend.main:app --reload --host 127.0.0.1 --port 8000
```

If your Windows environment has issues with the project directory path, run Uvicorn from `C:\` using the project's absolute path and `--app-dir`.

### Step 6: Open API Documentation

Visit:

```text
http://127.0.0.1:8000/docs
```

FastAPI Swagger UI provides interactive documentation for testing the backend endpoints.

## 🔌 API Endpoints

| Method | Endpoint | Description |
|---|---|---|
| GET | `/` | Backend welcome message |
| GET | `/health` | Health check |
| GET | `/sessions` | Retrieve monitoring sessions |
| GET | `/sessions/{session_id}` | Retrieve a specific session |
| GET | `/alerts` | Retrieve all alerts |
| GET | `/alerts/{session_id}` | Retrieve alerts for a session |
| WebSocket | `/ws/monitor` | Real-time driver monitoring |

## 🔄 WebSocket Communication

VisionDrive uses WebSocket communication to receive webcam frames and transmit real-time monitoring results.

WebSocket URL:

```text
ws://127.0.0.1:8000/ws/monitor
```

The backend processes incoming JPEG frames and returns monitoring information, including:

- Fatigue detection results.
- Distraction detection results.
- Phone detection status.
- Overall risk score and risk level.
- Generated alerts.

## 🗄️ Database Design

### Monitoring Sessions

Stores:
- Session ID.
- Start and end timestamps.
- Session status.
- Number of processed frames.
- Latest monitoring results.
- Risk summary.
- Recent monitoring results.

### Alerts

Stores:
- Alert ID.
- Session ID.
- Alert type.
- Severity.
- Alert message.
- Timestamp.

## 👥 Team Contributions

VisionDrive is developed collaboratively by a team of four members.

| Member | Responsibility |
|---|---|
| Member 1 | Driver Fatigue Detection |
| Member 2 | Driver Distraction and Phone Detection |
| Member 3 | Backend Development and System Integration |
| Member 4 | Frontend Development and Dashboard |

## 🚀 Future Enhancements

- Improved fatigue detection accuracy.
- Enhanced gaze tracking.
- Advanced driver behavior analysis.
- Improved dashboard analytics.
- Cloud-based session storage.
- Mobile application integration.

## ⚠️ Disclaimer

VisionDrive is an academic prototype developed for educational and research purposes. Its risk scores and alerts are experimental and should not be treated as a certified driver-safety system or a substitute for attentive driving.

## 📌 Project Status

Backend development, AI module integration, real-time communication, and database APIs have been implemented and tested locally. Frontend integration and complete system testing are part of the remaining development work.

---

**VisionDrive – Making Every Drive Safer with AI.** 🚗
