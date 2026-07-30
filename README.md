# AI Powered-Vehicle Detection Analytics System

AI Vehicle Recognition System is an end-to-end AI-powered web application that detects vehicles, people, and number plates from images, videos, and live webcam streams. The system performs vehicle model classification, person type classification, OCR-based number plate recognition, detection history management, analytics generation, and PDF report export through a FastAPI backend and React frontend.

---

## Project Overview

The **AI-Based Vehicle, Number Plate and Person Recognition System** is designed for intelligent traffic monitoring, surveillance analytics, parking management, and smart transport applications.

The system can detect vehicles and persons from images, videos, and live webcam streams. It also detects number plates, reads plate text using OCR, classifies vehicle model names, classifies person types, stores detection history, shows dashboard analytics, and generates downloadable PDF reports.

---

## Key Features

### Image Detection

- Upload vehicle/person images
- Detect vehicles
- Detect persons
- Detect number plates
- Read number plate text
- Classify vehicle model name
- Classify person type
- Save detection result in database
- View annotated output image

### Video Detection

- Upload traffic videos
- Process frames using OpenCV
- Detect and track vehicles/persons
- Assign tracking IDs
- Export processed video
- Optional number plate OCR
- Save video session in history
- Show processed video preview

### Live Webcam Monitoring

- Access browser webcam
- Send frames to backend using WebSocket
- Detect vehicles/persons in real time
- Optional plate OCR
- Show processed AI output frame
- Save photo logs
- Record processed webcam output video
- Save recorded live detection as `webcam_video`

### Classification

- Vehicle model classification
- Person type classification
- Supports expandable class sets
- Easy model replacement through `trained_models/`


### PDF Report Generation

Each detection session can export a PDF report containing:

- Session summary
- Input type
- Detection counts
- Vehicle details
- Person details
- Number plate details
- Output image preview or video link
- Model confidence values

---

## Technology Stack

### Backend

- Python
- FastAPI
- SQLAlchemy
- PostgreSQL / SQLite
- OpenCV
- Ultralytics YOLO
- EasyOCR
- PyTorch
- TorchVision
- ReportLab
- WebSocket

### Frontend

- React
- Vite
- Axios
- React Router
- Recharts
- Lucide React
- Tailwind CSS

### Machine Learning / Deep Learning

- YOLO object detection
- YOLO tracking with ByteTrack
- CNN-based vehicle model classification
- CNN-based person type classification
- OCR-based number plate text recognition

---

## System Architecture

```text
User
│
├── Image Upload
├── Video Upload
└── Live Webcam
    │
    ▼
React Frontend
│
├── REST API requests
└── WebSocket live frames
    │
    ▼
FastAPI Backend
│
├── Vehicle Detection Model
├── Number Plate Detection Model
├── Vehicle Model Classifier
├── Person Type Classifier
├── OCR Service
├── Video Processing Service
├── Live Webcam Service
├── History Service
├── Analytics Service
└── PDF Report Service
    │
    ▼
Database
│
├── Detection Sessions
├── Vehicle Detections
├── Person Detections
└── Plate Detections
```

---

## Model Files

Keep all trained model files inside:

```text
backend/trained_models/
```

Required model files:

```text
backend/trained_models/
├── vehicle_detector.pt
├── plate_detector.pt
├── vehicle_model_classifier.pth
├── vehicle_model_classes.json
├── person_type_classifier.pth
└── person_type_classes.json
```

### Model Purpose

| File | Purpose |
|---|---|
| `vehicle_detector.pt` | Detects vehicle/person objects |
| `plate_detector.pt` | Detects number plate location |
| `vehicle_model_classifier.pth` | Predicts vehicle model name |
| `vehicle_model_classes.json` | Stores vehicle model class names |
| `person_type_classifier.pth` | Predicts person type |
| `person_type_classes.json` | Stores person type class names |


---

## Final Folder Structure

```text
AI-Powered-Vehicle-Detection-Analytics-System/
│
├── backend/
│   ├── app/
│   │   ├── main.py
│   │   ├── config.py
│   │   ├── database.py
│   │   ├── models/
│   │   │   ├── db_models.py
│   │   │   └── schemas.py
│   │   ├── api/
│   │   │   ├── image_routes.py
│   │   │   ├── video_routes.py
│   │   │   ├── live_routes.py
│   │   │   ├── history_routes.py
│   │   │   └── analytics_routes.py
│   │   ├── services/
│   │   │   ├── detection_service.py
│   │   │   ├── plate_ocr_service.py
│   │   │   ├── vehicle_classifier_service.py
│   │   │   ├── person_classifier_service.py
│   │   │   ├── video_service.py
│   │   │   ├── live_service.py
│   │   │   ├── history_service.py
│   │   │   ├── analytics_service.py
│   │   │   └── report_service.py
│   │   ├── utils/
│   │   │   ├── image_utils.py
│   │   │   ├── video_utils.py
│   │   │   └── bbox_utils.py
│   │   └── storage/
│   │       ├── uploads/
│   │       ├── outputs/
│   │       ├── crops/
│   │       └── reports/
│   ├── trained_models/
│   │   ├── plate_detector.pt
│   │   ├── vehicle_detector.pt
│   │   ├── vehicle_model_classifier.pth
│   │   ├── vehicle_model_classes.json
│   │   ├── person_type_classifier.pth
│   │   └── person_type_classes.json
│   ├── requirements.txt
│   ├── run.py
│   └── .env
│
├── frontend/
│   ├── src/
│   │   ├── api/
│   │   │   └── axiosInstance.js
│   │   ├── components/
│   │   │   ├── Sidebar.jsx
│   │   │   ├── StatCard.jsx
│   │   │   └── ChartBox.jsx
│   │   ├── pages/
│   │   │   ├── Dashboard.jsx
│   │   │   ├── ImageDetection.jsx
│   │   │   ├── VideoDetection.jsx
│   │   │   ├── LiveMonitoring.jsx
│   │   │   ├── DetectionHistory.jsx
│   │   │   └── SessionDetails.jsx
│   │   ├── App.jsx
│   │   ├── main.jsx
│   │   └── index.css
│   ├── package.json
│   ├── vite.config.js
│   └── .env
│
├── README.md
└── .gitignore
```

---

## Backend Environment Variables

Create:

```text
backend/.env
```

Example for local development:

```env
PROJECT_NAME=AI Vehicle Recognition System
VERSION=1.0.0
API_PREFIX=/api
DATABASE_URL=sqlite:///./vehicle_detection.db
BACKEND_BASE_URL=http://127.0.0.1:8000
FRONTEND_URL=http://localhost:5173
CONFIDENCE_THRESHOLD=0.35
MAX_VIDEO_SECONDS=120
VIDEO_PROCESS_EVERY_N_FRAMES=1
VIDEO_OCR_EVERY_N_FRAMES=30
```

---

## Sample Output

### Image Detection Output

```json
{
  "success": true,
  "message": "Image detection completed successfully.",
  "total_vehicles": 2,
  "total_persons": 1,
  "total_number_plates": 1,
  "vehicles": [
    {
      "label": "car",
      "confidence": 0.93,
      "vehicle_model": "Hyundai i20",
      "vehicle_model_confidence": 0.59,
      "box": {
        "x1": 0,
        "y1": 82,
        "x2": 198,
        "y2": 245
      }
    }
  ],
  "number_plates": [
    {
      "label": "licence",
      "plate_text": "TN59AB1234",
      "detection_confidence": 0.88,
      "ocr_confidence": 0.76
    }
  ]
}
```

---

## Model Training Plan

### Number Plate Detection

- Model: YOLO
- Output file: `plate_detector.pt`
- Dataset format: YOLO format
- Classes: number plate / licence / license plate

### Vehicle Detection

- Model: YOLO
- Output file: `vehicle_detector.pt`
- Classes: car, motorcycle, bus, truck, bicycle, person

### Vehicle Model Classification

- Model: EfficientNet-B0 / ResNet / MobileNet
- Output files:
  - `vehicle_model_classifier.pth`
  - `vehicle_model_classes.json`

### Person Type Classification

- Model: EfficientNet-B0 / ResNet / MobileNet
- Output files:
  - `person_type_classifier.pth`
  - `person_type_classes.json`

---

## Dataset Sources

The following datasets can be used for training or improving the model.

### Number Plate Detection

- Roboflow Indian License Plate Detection dataset includes open-source license plate images and a pre-trained model/API.
- Hugging Face UniDataPro license plate detection dataset contains license plate images from 32+ countries and provides OCR/detection-related annotations.

Source links:

- https://universe.roboflow.com/license-plate-detection-khhkb/indian-license-plate-detection-6tmbr
- https://huggingface.co/datasets/UniDataPro/license-plate-detection

### Vehicle Detection

- UAVDT is a vehicle detection/tracking dataset with annotated images for classes such as car, truck, and bus.
- Roboflow Aerial Vehicles dataset provides a Roboflow-exportable version with classes including car, truck, bus, and van.

Source links:

- https://datasetninja.com/uavdt
- https://universe.roboflow.com/uavdt/aerial-vehicles-hjarh

### Vehicle Model Classification

- Stanford Cars dataset contains 16,185 images across 196 vehicle classes, with classes at make/model/year level.

Source link:

- https://www.kaggle.com/datasets/eduardo4jesus/stanford-cars-dataset


---

## Future Enhancements

- Add more vehicle classes
- Add more Indian car and bike models
- Add truck and bus type classification
- Add helmet detection
- Add traffic police/security worker classification
- Add user authentication
- Add admin dashboard
- Add role-based access
- Add real-time alert system
- Add email report sharing
- Add mobile responsive live monitoring

---

## LinkedIn

- Link: www.linkedin.com/in/gokul-raj-k-5673982a8

---


