# 🚨 Motion Detection & Alert System using OpenCV

## 📖 Project Overview
This project is an exploratory Computer Vision pipeline built to detect motion in video streams and trigger alerts based on temporal thresholds. Using OpenCV, the system processes video frames, identifies moving objects (like people), tracks how long they remain in the frame, and visually flags them if they linger beyond a predefined security threshold.

![Motion Detection Output Demo](Screenshot%202026-05-31%20220302.png)

This project was developed in **Google Colab** as a hands-on way to learn video processing, background subtraction, and contour detection in OpenCV.

## 🛠️ Tech Stack
* **Language:** Python
* **Computer Vision:** OpenCV (`cv2`)
* **Data Manipulation:** NumPy
* **Environment:** Google Colab

---

## 🚀 How It Works (The Pipeline)

### 1. Environment Setup & Video Ingestion
* Installed `opencv-python-headless` for server-side processing without GUI dependencies.
* Utilized `google.colab.files` to handle the uploading of video files (e.g., MP4s) directly into the notebook environment.

### 2. Motion Detection & Processing
* **Frame Differencing / Background Subtraction:** The core logic isolates moving subjects from the static background across sequential frames.
* **Image Preprocessing:** Frames are converted to grayscale and blurred (Gaussian Blur) to reduce noise and prevent false positives.
* **Thresholding:** Converts the processed frame into a binary mask where white pixels represent movement and black represents the static background.

### 3. Contour Detection & Bounding Boxes
* Used `cv2.findContours` to identify the boundaries of the white (moving) regions in the binary mask.
* Filtered out micro-movements (like leaves blowing or camera noise) by setting a minimum contour area.
* Used `cv2.boundingRect` to draw clean, geometric rectangles around valid moving targets.

### 4. Tracking & Alert System
* **Temporal Tracking:** Implemented a custom dictionary to track the exact timestamp when a moving object is first detected.
* **Threshold Logic:** Calculated the elapsed time for each detected object.
* **Dynamic Visual Feedback:** * **Safe (Green):** If the object has been in the frame for a short duration, the bounding box remains green.
  * **Alert (Red):** If the elapsed time exceeds the security threshold, the bounding box turns red, and `cv2.putText` overlays an "ALERT!" warning with the elapsed time directly onto the frame.

### 5. Display & Output
* Used `cv2_imshow` (Colab's safe rendering method) to display processed frames. This prevents the Colab environment from crashing due to memory overload while still providing clear visual feedback of the system in action.

---

## 🧠 Key Concepts & Skills Learned
1. **Video Processing Fundamentals:** Understanding how to break a video down into individual frames, process them, and re-render them with overlays.
2. **Contour Analysis:** Learning how OpenCV interprets shapes and boundaries, and how to extract coordinates to draw geometric bounding boxes.
3. **State Management in Loops:** Moving beyond static images to video requires maintaining "state" (like tracking how long an object has been visible) across a continuous `while` loop.
4. **Google Colab Workarounds:** Learning how to adapt standard OpenCV GUI functions to work within a browser-based Jupyter Notebook environment safely.
