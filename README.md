# Camera Tracking and Virtual Avatars
## Introduction
We together have developed the Camera Tracking and Virtual Avatars application, which consists of 5 fearfully and wonderfully made demos.

The demos can be accessed online and don't require any installation process.

* Bear: https://avatarvirt.netlify.app/bear.html
* Frog: https://avatarvirt.netlify.app/frog.html
* Hand: https://avatarvirt.netlify.app/hand.html
* Tiger: https://avatarvirt.netlify.app/tiger.html
* Ping: https://avatarvirt.netlify.app/ping.html

The demos speak volumes. In fact, they are more powerful than all the words that we can manage to say here.
## Related Work
The field of real-time camera tracking and virtual avatar animation has seen significant growth, driven by advancements in machine learning and computer vision. Our work builds upon several key frameworks and methodologies that have defined the current landscape of browser-based motion capture.
### 1. MediaPipe Framework
**MediaPipe**, developed by Google, serves as the primary backbone for many modern tracking applications. It offers a suite of cross-platform, customizable ML solutions for live and streaming media.
 * **Hand Tracking:** MediaPipe Hands utilizes an efficient pipeline that provides 21 3D hand landmarks from a single frame. This is crucial for applications requiring high-precision gesture recognition.
 * **Face Mesh:** For facial avatars, MediaPipe Face Mesh estimates 468 3D face landmarks in real-time, allowing for detailed mapping of expressions and lip-syncing without the need for depth sensors.
 * **Holistic Tracking:** The MediaPipe Holistic pipeline integrates components for a combined hand, face, and pose perception, which is essential for full-body virtual representation.
### 2. OpenCV and Classical Computer Vision
Before the ubiquity of pre-trained ML models, **OpenCV** (Open Source Computer Vision Library) was the standard for tracking.
 * **Haar Cascades:** Traditionally used for face detection, though limited in capturing the nuance of expressions compared to deep learning models.
 * **Optical Flow:** Techniques like Lucas-Kanade are often used in conjunction with landmark detectors to smooth jitter and track movement between frames.
 * **Integration:** Many modern applications still use OpenCV for image preprocessing, such as grayscale conversion, denoising, and coordinate transformations, before passing frames to a neural network.
### 3. Deep Learning-Based Pose Estimation
Beyond MediaPipe, several academic and industry models have pushed the boundaries of accuracy:
 * **OpenPose:** One of the first multi-person 2D real-time keypoint detection systems. While highly accurate, it often requires significant GPU resources, making it less ideal for lightweight web applications.
 * **DensePose:** Developed by Facebook AI Research (FAIR), this moves beyond landmarks by mapping all human pixels of an RGB image to a 3D surface of the human body, providing a much richer "skin" for virtual avatars.
### 4. Web-Based Rendering and Animation
Tracking is only half of the challenge; the other half is mapping that data to a 3D model.
 * **Three.js & Babylon.js:** These libraries are the industry standards for rendering 3D content in the browser. They allow developers to take tracking coordinates and apply them to rigged 3D models via **Inverse Kinematics (IK)** or direct bone rotation.
 * **Kalidokit:** A specialized library often used alongside MediaPipe to translate raw landmark data into natural-looking rotations for 3D avatars (VRM models), handling the complex math required for "human-like" movement.
### 5. ARCore and ARKit
While our application focuses on browser-based accessibility, mobile-native frameworks like **Apple’s ARKit** and **Google’s ARCore** have set the benchmark for high-fidelity tracking. ARKit, in particular, uses the TrueDepth camera system to provide **BlendShape Coefficients**, which allow for extremely responsive facial "puppeteering"—a standard our application strives to emulate using standard RGB webcams.
## Methodology
For ease of use, all demos are in the form of self-contained HTML files. They can be hosted on any static web server or run locally.

The demos all use the MediaPipe framework. The general flow is as follows:
* Acquire access to the webcam
* Initialize MediaPipe to track body parts
* Draw tracking lines and dots on an overlay window to signal to the user that tracking is taking place
* Based on the tracking data, we then do something

We now focus on what we do with the tracking data.
### Bear, Frog, Tiger
For these three demos, an SVG is controlled by the tracking data.
* Bear
  * Five body parts of the bear are controlled by the five fingers on a hand. The code, through the tracking data and an algorithm, determines whether a finger is folded or not. When a finger is extended, a body part moves one way. And when a finger is folded, a body part moves the other way. Because human thumbs are opposable, the algorithm for checking whether the thumb is folded or not is slightly different.
  * The SVG is drawn as follows:
* Frog
  * The user's face is tracked. Then, the eyelids of the frog close or open depending on the eyelids of the user. The same goes for the mouth.
  * The algorithm for determining the extent of opening an eyelid is as follows:
  * The algorithm for determining the extent of opening the mouth is as follows:
  * The algorithm for animation interpolation is as follows:
* Tiger
  * Both the hands and the face are tracked.
### Hand
Unlike the previous 3 demos, there is no SVG that is driven by tracking data. Rather, it tracks the user's hand, and then from the tracking data, it draws a skeleton on the screen with Three.js. Then, it attaches 5 stickers to the palmar side of the fingers. The 5 stickers are 5 different animal emojis.
### Ping
Ping is an adaptation of the classic ping pong game but controlled with two hands. The left hand serves as Player 1 and the right hand serves as Player 2. For each hand, the game computes a composite hand folding score which is then used to control the paddle.

The algorithm to calculate the hand folding score is as follows:

The algorithm to move the paddle based on the hand folding score is as follows:
## Conclusion
The five demos together show that body part tracking is a practical technology that can run on diverse devices such as mobile phones and laptops. Body part tracking is reliable and can be used to create engaging experiences such as virtual avatars and games. From our experience, people are intrigued by the ability of our software to track body movements and animate characters on the screen, to the degree where they feel the characters on the screen are a part of their body during the duration of the demo.
