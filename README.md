# 💪 Bicep Curls Counter

A real-time bicep curl counter using computer vision and pose estimation. This application uses MediaPipe and OpenCV to track your arm movements and automatically count your bicep curl repetitions through your webcam.

![Python](https://img.shields.io/badge/python-3.7+-blue.svg)
![MediaPipe](https://img.shields.io/badge/mediapipe-latest-green.svg)
![OpenCV](https://img.shields.io/badge/opencv-latest-red.svg)

## 🎯 Features

- **Real-time pose detection** using MediaPipe's pose estimation model
- **Automatic rep counting** based on elbow angle calculations
- **Visual feedback** with live angle display and rep counter overlay
- **Pose landmark visualization** to see tracked body points
- **Configurable for left or right arm** tracking

## 📋 Prerequisites

- Python 3.7 or higher
- Webcam or external camera
- Windows, macOS, or Linux

## 🚀 Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/ilyasbelaoud/bicep-curls-counter.git
   cd bicep-curls-counter
   ```

2. **Install required dependencies**
   ```bash
   pip install opencv-python mediapipe numpy
   ```

   Or create a virtual environment (recommended):
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   pip install opencv-python mediapipe numpy
   ```

## 💻 Usage

### Running as a Python Script

```bash
python bicepcounter.py
```

### Running as a Jupyter Notebook

1. Rename the file extension:
   ```bash
   mv bicepcounter.py bicepcounter.ipynb
   ```

2. Launch Jupyter Notebook:
   ```bash
   jupyter notebook
   ```

3. Open `bicepcounter.ipynb` and run all cells

### Controls

- **Press 'q'** to quit the application
- The counter will automatically increment when a full curl is detected

## 🎮 How It Works

1. **Pose Detection**: MediaPipe detects 33 body landmarks in real-time
2. **Angle Calculation**: The application calculates the angle between your shoulder, elbow, and wrist
3. **Rep Counting**: 
   - When your arm is extended (angle > 150°), the stage is set to "down"
   - When your arm is curled (angle < 45°) after being down, a rep is counted and stage changes to "up"
4. **Visual Feedback**: The current angle, rep count, and stage are displayed on screen

## ⚙️ Configuration

### Switching Arms

To track the right arm instead of the left, modify lines 51-56 in `bicepcounter.py`:

```python
# Change LEFT_ to RIGHT_
shoulder = [landmarks[mp_pose.PoseLandmark.RIGHT_SHOULDER.value].x,
            landmarks[mp_pose.PoseLandmark.RIGHT_SHOULDER.value].y]
elbow = [landmarks[mp_pose.PoseLandmark.RIGHT_ELBOW.value].x,
         landmarks[mp_pose.PoseLandmark.RIGHT_ELBOW.value].y]
wrist = [landmarks[mp_pose.PoseLandmark.RIGHT_WRIST.value].x,
         landmarks[mp_pose.PoseLandmark.RIGHT_WRIST.value].y]
```

### Adjusting Sensitivity

Modify the angle thresholds in lines 67-71:

```python
if angle > 150:  # Adjust this value for "down" position
    stage = "down"
if angle < 45 and stage == 'down':  # Adjust this value for "up" position
    stage = "up"
    counter += 1
```

### Camera Selection

By default, the application uses camera index 0. To use a different camera:

```python
cap = cv2.VideoCapture(1)  # Change 0 to your camera index
```

## 🛠️ Troubleshooting

### Camera Not Found
- Ensure your webcam is properly connected
- Try different camera indices (0, 1, 2, etc.)
- Check if another application is using the camera

### Poor Detection
- Ensure good lighting conditions
- Position yourself so your full upper body is visible
- Stand against a plain background for better detection

### Performance Issues
- Close other applications using the camera
- Reduce the frame resolution if needed
- Ensure your system meets the minimum requirements

## 📝 Known Issues

- Detection accuracy may vary with different lighting conditions
- The counter may occasionally miscount if movements are too fast or irregular
- Works best when the full upper body is visible in frame

## 🤝 Contributing

This is a beginner-friendly project! Contributions, issues, and feature requests are welcome.

## 📚 Resources & Inspiration

This project was inspired by and references the following resources:

- [MediaPipe Pose Documentation](https://google.github.io/mediapipe/solutions/pose.html)

## 📄 License

This project is open source and available for anyone to use and modify.

## 🙏 Acknowledgments

- Google MediaPipe team for the pose estimation model
- OpenCV community for computer vision tools
- The fitness tech community for inspiration

---

**Note**: This project was created as a learning exercise and may have some bugs or limitations. Feel free to improve upon it and share your enhancements!
