# VATIF PCB Inspection System

This application is a full-stack automated optical inspection (AOI) tool for PCBs. It uses Gerber processing (pygerber), Computer Vision (OpenCV), and CNN inference (TensorFlow/Keras) to detect defects.

## Project Structure

- `/src`: React Frontend (Vite + Tailwind + Recharts)
- `/python_backend`: Production FastAPI service for CV/AI processing
- `/server.ts`: Node.js development gateway / Preview server

## Setup Instructions

### 1. Backend (Python/FastAPI)
Requires Python 3.9+

```bash
cd python_backend
pip install -r requirements.txt
python main.py
```

- Ensure your trained CNN model is placed at `python_backend/models/vatif_pcb_model.h5`.
- The FastAPI server runs on port 8000.

### 2. Frontend (React)
Requires Node.js 18+

```bash
npm install
npm run dev
```

The frontend will start on port 3000.

## Hardware Integration (ESP32-CAM)

The system is configured to handshake with an ESP32-CAM at IP `192.168.4.1`. 
The ESP32 should expose a `/capture` endpoint that returns a JPEG buffer.

## Defect Classes
- Solder Bridge
- Missing Component
- Misalignment
- No Solder / Cold Joint

## Inspection Workflow
1. **Gerber Upload**: Provide manufacturing files to generate a "Gold" reference image.
2. **ESP32 Trigger**: Capture the physical PCB image via the network.
3. **Alignment**: OpenCV SIFT/SIFT filters align the real image to the Gerber map.
4. **CNN Inference**: Detected anomalies are passed to the ResNet50-based CNN for classification.
