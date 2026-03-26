# NeuraLens SmartGlass Generalized Model Training

![alt text](https://img.shields.io/badge/license-MIT-blue.svg)
![alt text](https://img.shields.io/badge/python-3.10%2B-green.svg)
![alt text](https://img.shields.io/badge/status-active-orange.svg)

This repository focuses on training the **Generalized Model** for the NeuraLens SmartGlass ecosystem. Unlike specialized models for niche items, this module trains a high-speed, broad-spectrum detection system using the **YOLOv11n (Nano)** architecture to identify everyday objects, people, and obstacles in real-time.

## 🚀 Overview
The Generalized Model serves as the "eyes" of the NeuraLens system for standard navigation. By utilizing **YOLOv11n**, we achieve the optimal balance between high-speed inference (essential for offline wearable hardware) and the accuracy required to detect over 80+ common object categories (COCO-based and custom indoor sets).

## ✨ Key Features
* **YOLOv11n Integration:** Leverages the latest YOLOv11 Nano architecture for ultra-lightweight and ultra-fast detection.
* **Broad Object Detection:** Pre-configured to recognize a wide range of categories including furniture, safety hazards, people, and common household items.
* **Edge-First Training:** Optimized training parameters specifically for export to low-power NPUs and mobile CPUs used in the SmartGlass.
* **Automated Augmentation:** Built-in data augmentation pipeline to ensure the model remains robust in different lighting conditions and camera angles.

## 🛠 Tech Stack
* **Language:** Python
* **AI Framework:** Ultralytics YOLOv11
* **Base Architecture:** YOLOv11n (Nano)
* **Optimization Tools:** TensorRT, ONNX, CoreML
* **Dataset Management:** Roboflow / COCO Format

## 📦 Installation

**1. Clone the repository:**
```bash
git clone https://github.com/Subash-Poudel1059/NeuraLens_SmartGlass_Generalized_Model_Training
cd NeuraLens_SmartGlass_Generalized_Model_Training
```

**2. Create and activate a virtual environment:**
```bash
python -m venv venv
# Linux / macOS
source venv/bin/activate
# Windows
venv\Scripts\activate
```

**3. Install dependencies:**
```bash
pip install -r requirements.txt
pip install ultralytics  # Specifically for YOLOv11
```

**4. Configure environment variables:**
Create `.env` with this content (adjust paths if needed):
```env
DATASET_YAML=./data/generalized_data.yaml
MODEL_SIZE=yolov11n
TRAINING_EPOCHS=100
DEVICE=0  # GPU ID or cpu
```

## 🚀 Usage

### Training YOLOv11n generalized model
```bash
python train.py --model yolov11n.pt --data data/coco8.yaml --epochs 100 --img 640
```

### Exporting for offline SmartGlass deployment
```bash
python export.py --model runs/detect/train/weights/best.pt --format tflite --int8
```

- `--model`: path to trained weights file (`best.pt`).
- `--format`: target deployment format (`tflite`, `onnx`, `openvino`).
- `--int8`: enable 8-bit quantization (max speed on offline hardware).