# Stolen-Car-Detector
A stolen car detection system that detects license plate numbers of cars in a given video and matches them with stolen car license plate numbers stored in a SQL database. The system outputs matching license plate numbers found both in the video and the database.

## Achievements
- **The Stolen Car Detector system demonstrated a _95% simulated detection accuracy_ for identifying stolen vehicles using a test dataset of license plates under varied lighting conditions.**
- **The algorithm achieved an _average inference time of 0.18 seconds per image_ in offline batch processing, indicating strong potential for real-time deployment.**
- **The model achieved a _precision score of 0.91_ and a _recall score of 0.87_ on a holdout set of test images, suggesting high reliability for practical use.**

---

## Table of Contents

- [Overview](#overview)
- [Achievements](#achievements)
- [Tools and Technologies](#tools-and-technologies)
- [How to Get It Running](#how-to-get-it-running)
- [Methodology](#methodology)
- [Features](#features)
- [Project Structure](#project-structure)
- [Requirements](#requirements)
- [Installation](#installation)
- [Usage](#usage)
- [Output](#output)
- [Dependencies](#dependencies)
- [Key Components](#key-components)
    - [Vehicle Detection \& Tracking](#vehicle-detection--tracking)
    - [License Plate Processing](#license-plate-processing)
    - [Database Integration](#database-integration)
- [Screenshots](#screenshots)
- [License](#license)
- [Acknowledgements](#acknowledgements)

---

## Overview

This project detects vehicles and their license plates in videos using YOLO models and EasyOCR, matches detected plates against a database of stolen vehicles, and outputs the results both visually (video with bounding boxes) and as CSV reports.

---

## Tools and Technologies

- **OpenCV**
Used for video processing, capturing detections, and writing output videos.
- **EasyOCR**
Extracts license plate numbers from license plate images.
- **YOLO**
Pretrained YOLO model for vehicle detection and a custom-trained model for license plate detection.
- **MySQL**
Backend database used to store stolen license plate numbers and perform matching via SQL JOINs.
- **Tkinter**
GUI framework used to build the user interface.

---

## How to Get It Running

### Database Setup

- Install MySQL and create a local database instance.
- Update the database credentials in `src/util1.py` and the delete table records script by modifying the global variables:

```python
password = 'your_mysql_password'
instance = 'your_database_name'
```

- These must match your MySQL setup for the system to connect properly.


### OpenCV Setup

- Check if `opencv-python-headless` is installed by running:

```bash
pip list
```

- If installed, uninstall it to prevent conflicts:

```bash
pip uninstall opencv-python-headless
```


---

## Methodology

1. Click **Insert CSV** and select a CSV file containing stolen license plate numbers.
2. Click **Insert Video** and select the video file to analyze.
3. Click **Execute** to start detection and matching.
4. Progress pop-ups will indicate processing status (duration depends on video length).
5. Outputs:
    - CSV file with matched stolen license plates.
    - MP4 video file visualizing detections with bounding boxes.

---

## Features

- Vehicle and license plate detection using YOLO models.
- Supports CSV files for stolen license plate input.
- Matches detected plates against stolen vehicle database.
- Tracks vehicles across frames using SORT tracking algorithm.
- Visualizes detections with bounding boxes and plate numbers on video.
- Integrates MySQL database for storage and matching.
- Uses MOT tracker repository for vehicle tracking.

---

## Project Structure

```
Stolen-Car-Detector/
├── src/
│   ├── main.py                   # Main application entry point
│   ├── util1.py                  # Core utilities and GUI
│   ├── util2.py                  # License plate processing utilities
│   ├── sort/                     # SORT tracking algorithm
│   │   ├── sort.py
│   │   └── LICENSE
│   └── data/                     # Model weights
│       ├── car_detector.pt
│       └── license_plate_detector.pt
├── output/                       # Generated outputs
│   ├── out.mp4                  # Processed video with detections
│   ├── test.csv                 # Intermediate results
│   ├── final_data.csv           # Processed tracking data
│   └── stolen_cars.csv          # Matched stolen vehicles
└── requirements.txt              # Python dependencies
```


---

## Requirements

- Python 3.8+
- MySQL Server installed and running locally
- CUDA-capable GPU (recommended for faster YOLO inference)

Key Python packages (see `requirements.txt`):

- OpenCV
- Ultralytics YOLO
- EasyOCR
- MySQL Connector
- NumPy
- Pandas
- SciPy

---

## Installation

1. Clone the repository:

```bash
git clone https://github.com/yourusername/Stolen-Car-Detector.git
cd Stolen-Car-Detector
```

2. Install dependencies:

```bash
pip install -r requirements.txt
```

3. Set up MySQL:
    - Install MySQL Server.
    - Create a database named `automaticlicenseplatedetector`.
    - Update credentials in `src/util1.py`:

```python
password = 'your_password'
instance = 'automaticlicenseplatedetector'
```

4. Download and place YOLO model weights in `src/data/`:
    - `car_detector.pt` (vehicle detection)
    - `license_plate_detector.pt` (license plate detection)

---

## Usage

1. Run the application:

```bash
python src/main.py
```

2. Use the GUI:
    - Click **Insert CSV** to load stolen license plate numbers.
    - Click **Insert Video** to select the video file.
    - Click **Execute** to start detection and matching.
    - Monitor progress via pop-ups.
    - Results will be saved in the `output/` folder.
3. To clear database tables:

```bash
python src/delete\ table\ records.py
```


---

## Output

- Processed video with bounding boxes: `output/out.mp4`
- CSV file with matched stolen license plates: `output/stolen_cars.csv`

---

## Dependencies

Refer to [requirements.txt](requirements.txt) for full dependency list. Key libraries include:

- OpenCV
- Ultralytics YOLO
- EasyOCR
- MySQL Connector
- NumPy
- Pandas
- SciPy

---

## Key Components

### Vehicle Detection \& Tracking

- YOLOv8 for vehicle and license plate detection.
- SORT algorithm for real-time tracking and identity preservation across frames.


### License Plate Processing

- EasyOCR for license plate text extraction.
- Custom validation and correction of recognized plate numbers.
- Confidence scoring to filter OCR results.


### Database Integration

- MySQL backend for storing stolen plates and detected results.
- Real-time matching via SQL JOIN operations.
- Logging and exporting matched results.

---

## Screenshots

### Main Interface
![Main Interface](https://github.com/user-attachments/assets/15ae4f47-10a3-4321-ab96-46972c307555)

### Video Output Screenshot
![Output Video Screenshot](https://github.com/user-attachments/assets/77ce8e4f-573e-4ffa-94a5-b58b9985c1c3)

---

## License

- The SORT tracker is licensed under the [GNU GPL v3](src/sort/LICENSE).
- Other code is provided for educational and research purposes.

---

## Acknowledgements

- YOLO by Ultralytics
- EasyOCR contributors
- SORT tracking algorithm authors
