# AI-driven Early Detection of Autism in Toddlers using Multimodal AI

Autism Spectrum Disorder (ASD) is a neurodevelopmental condition that affects communication, behavior, and social interaction. Early diagnosis can significantly improve intervention outcomes. The aim is to design a proof-of-concept AI model or pipeline that aims to detect early behavioral signs of autism in toddlers using non-invasive and multimodal data, particularly focusing on visual cues captured via camera systems.

---

### ✅ **1. Feature Identification**

We propose detecting the following **early behavioral signs** of ASD, observable through video:

* **Reduced Eye Contact**: Infrequent gaze toward caregiver's face during interaction.
* **Repetitive Movements**: Recurrent hand flapping, body rocking, or spinning.
* **Lack of Social Reciprocity**: Failure to respond to name, limited imitation or turn-taking.
* **Delayed Gesture Use**: Absence or reduction in gestures like pointing, waving, or showing.
* **Delayed Responsiveness**: Longer latency in responding to social or visual cues (without relying on speech).

---

### ✅ **2. Eye Contact Analysis**

**Objective**: Detect reduced or absent eye contact in toddlers.

#### 📷 **Method**:

* **Hardware**: Use a standard webcam or mobile phone camera.
* **Tools**: Use **face detection + eye gaze tracking** libraries:

  * **Dlib / OpenFace / MediaPipe Face Mesh** for landmark detection.
  * **Gaze tracking** using geometric vector from eyes to screen/caregiver.
* **Approach**:

  1. Detect toddler's face and eye landmarks.
  2. Estimate gaze direction.
  3. Monitor for gaze towards caregiver’s face or toy.
  4. Define thresholds (e.g., <30% eye contact time during a 2-minute interaction).

#### 📊 Output:

* A **gaze heatmap** and **eye contact score**.
* Flag if the gaze rarely aligns with the caregiver’s face.

---

### ✅ **3. Repetitive Behavior Detection**

**Objective**: Detect repetitive movements like hand flapping or rocking.

#### 🧠 **Model**:

* Use **pose estimation + temporal CNN/LSTM** for pattern detection.

  * **OpenPose / MediaPipe Pose** to extract body keypoints.
  * Feed pose sequences into a **1D CNN or LSTM** to classify motion patterns.

#### 🛠️ **Steps**:

1. Collect labeled video samples (ASD vs. non-ASD) showing repetitive vs. non-repetitive actions.
2. Use pose keypoints (arms, hands, torso) as input.
3. Train CNN/LSTM on time-series of joint movements.

#### ☀️ **Key Features**:

* High-frequency, cyclic movements of arms or torso.
* Symmetry in movement.
* Duration and frequency.

---

### ✅ **4. Speech-Less Language Delay Detection**

**Objective**: Detect language delays *without using audio*.

#### 🎥 **Behavioral Proxies**:

* **Reduced gesture use**: Lack of pointing, waving, or showing.
* **Delayed reaction**: Slower response to caregiver gestures or object presentations.

#### 🔍 **Method**:

* Use **pose estimation and object detection**:

  * Check for gestures involving extended arm and finger (pointing).
  * Measure **response time** to visual events (e.g., parent points or waves).
* **Attention estimation**: Use face orientation to see if toddler looks at new stimuli.

#### ⏱️ Features:

* Time-to-response (TTR) when toy is shown or caregiver gestures.
* Gesture frequency per minute.

---

### ✅ **5. Social Reciprocity Assessment**

**Objective**: Assess child’s interest in social interaction.

#### 📽️ **Video-based Tasks**:

* Simulate interaction:

  * Parent calls child’s name or initiates joint attention with toy.
* **Detect Response**:

  * Head turn, gaze shift, smile, or approach toward caregiver.

#### 🧰 **Method**:

* **Head orientation tracking**: Use facial landmarks to detect head turning.
* **Smile detection**: Optional face emotion analysis (OpenCV, DeepFace).
* **Hand tracking**: Detect child pointing or holding up toy for caregiver.

#### 📈 Behavior Score:

* No response to name call in >50% trials.
* No shared attention behaviors during object-focused play.

---

### 🔄 **Pipeline Summary**

| Module                 | Tools Used                | Output                      |
| ---------------------- | ------------------------- | --------------------------- |
| **Face/Gaze Tracking** | Dlib, OpenFace, MediaPipe | Eye contact frequency       |
| **Pose Estimation**    | OpenPose, MediaPipe Pose  | Repetitive behavior metrics |
| **Temporal Modeling**  | CNN / LSTM                | Action classification       |
| **Gesture Analysis**   | Keypoint tracking         | Gesture count & TTR         |
| **Social Response**    | Face/pose tracking        | Social reciprocity score    |

---

### 🧪 Sample Use Case Flow

1. Parent plays with child in front of webcam for 2-3 minutes.
2. System records video and runs real-time pose and face analysis.
3. AI extracts metrics:

   * Eye contact %, repetitive actions, gesture count, response time.
4. A **dashboard** visualizes scores and flags risk indicators.

---
