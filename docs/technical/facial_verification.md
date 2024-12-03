### **Overview**  
This document describes the facial verification system integrated into the Decentralized Identity and Reputation System. The system’s primary purpose is to replace traditional CAPTCHA mechanisms by verifying the humanity of a user through liveness detection. It ensures that only real humans can access or perform specific actions within the system, preventing bots and automated scripts.

---

### **Key Features**

1. **Liveness Detection**  
   - Verifies that the user interacting with the system is a live human being.  
   - Detects facial movements (e.g., blinking, smiling, head tilting) to confirm liveness.  

2. **No Data Storage**  
   - The system does not store facial data, images, or biometric hashes.  
   - All processing occurs in real time and is discarded after verification.  

3. **Human Detection**  
   - Identifies whether a human face is present and active.  
   - Rejects bots, static images, or pre-recorded videos.

4. **Access Control**  
   - Grants access to users who successfully pass the liveness check.

---

### **Workflow**

#### **1. Liveness Check**
1. User accesses the liveness check interface.  
2. The system captures live video input from the user's camera.  
3. Liveness prompts are displayed, such as:  
   - Blink your eyes.  
   - Turn your head to the left or right.  
   - Smile or raise your eyebrows.  
4. The system uses AI models to analyze the user's response in real time.

#### **2. Verification Decision**
1. If the liveness check is successful, the user is granted access.  
2. If the check fails (e.g., static image detected or prompts not followed), access is denied.

---

### **Technology Stack**

1. **AI Models for Liveness Detection**  
   - Models like `MediaPipe`, `OpenCV`, or `Dlib` to detect facial landmarks and track movements.  

2. **Frontend Integration**  
   - WebRTC for accessing live video input.  
   - React.js for an interactive and user-friendly interface.

3. **No Data Storage**  
   - All facial data is processed in real time and discarded immediately after verification.

---

### **Facial Verification Data Flow**

1. **Live Video Capture**  
   - User’s live video is captured using their camera via WebRTC.  

2. **Real-Time Analysis**  
   - The system processes the video feed and tracks facial movements to detect liveness.  

3. **Decision Making**  
   - If prompts are successfully completed, access is granted.  
   - Otherwise, the user is denied access.  

---

### **DiGraph Representation**

Below is the Graphviz **DiGraph** code illustrating the liveness-based facial verification system:

```plaintext
digraph FacialVerification {
    rankdir=LR;
    node [shape=box, fontname="Arial"];

    User [label="User (DAO Member)", shape=ellipse];
    Camera [label="Webcam/Smartphone Camera"];
    LivenessPrompts [label="Liveness Prompts"];
    LivenessAnalysis [label="Analyze Facial Movements"];
    Success [label="Access Granted"];
    Failure [label="Access Denied"];

    User -> Camera [label="Live Video Input"];
    Camera -> LivenessPrompts [label="Display Prompts"];
    LivenessPrompts -> LivenessAnalysis [label="Track Movements"];
    LivenessAnalysis -> Success [label="If Verified"];
    LivenessAnalysis -> Failure [label="If Not Verified"];
}
```

---

### **Advantages of Liveness-Based Verification**

1. **Enhanced Security**  
   - Prevents bots and spoofing attempts using static images or videos.  

2. **User Privacy**  
   - No facial data is stored, ensuring complete privacy for users.  

3. **Real-Time Verification**  
   - Processes and verifies liveness instantly.  

4. **Universal Access**  
   - Can be integrated into multiple workflows as an alternative to CAPTCHA systems.  

---

### **Integration Points**

1. **During DID Registration**  
   - Used to verify that the user is a real human when registering a new DID.  

2. **Before Sensitive Actions**  
   - Verification required before participating in activities like voting or messaging.

3. **General Access Control**  
   - Used to gate any action requiring proof of humanity.  
