# Aura-Safety-Scout
🚗 Aura Safety Scout: AI-Powered Blind Spot & Conversational Agent
Aura Safety Scout is an advanced, AI-driven vehicle safety system designed to monitor blind spots in real-time. By combining edge hardware, computer vision, sensor fusion, and a conversational Large Language Model (LLM), Aura not only visually alerts drivers to hidden dangers but also verbally explains the situation on command, significantly reducing driver cognitive load.
Drive link for acessing the file:
https://drive.google.com/drive/folders/10YwvVb2m-2dhvnXVpWzIq7Xvpt9UW4WP?usp=sharing
⚙️ How It Runs (System Workflow)
The system operates on a continuous, low-latency pipeline to ensure real-time safety:

Data Acquisition (The Edge): A side-mounted camera and an ultrasonic sensor continuously monitor the vehicle's blind spot.

Wireless Transmission: A Raspberry Pi processes the raw sensor data (video frames and distance metrics) and transmits it wirelessly to the central processing hub (e.g., a laptop or in-car PC).

Computer Vision & Object Detection: The processing hub runs the video feed through a YOLOv8 model to identify objects (e.g., motorcycles, cars, pedestrians) in real-time.

Sensor Fusion: The system merges the visual bounding box data from YOLOv8 with the depth data from the ultrasonic sensor to create a high-confidence threat profile (e.g., "Motorcycle detected at exactly 3 meters").

UI & Visual Alerting: The application interface displays the live feed, drawing a glowing red bounding box around the detected threat alongside critical text (e.g., "Motorcycle: 3m - URGENT").

Conversational AI (Aura): If the driver asks, "Hey Aura, explain that alert," the integrated LLM agent uses Retrieval-Augmented Generation (RAG) to instantly process the system logs. It translates the raw alert data into a natural language response and outputs it via Text-to-Speech (TTS): "Warning: Motorcycle detected close on your right side at 3 meters."

🛠️ Tech Stack & Tools Used
Software & AI Models
Language/Ecosystem: Python 3.x

Computer Vision: YOLOv8 (Ultralytics) for real-time, high-speed object detection.

Image Processing: OpenCV for handling video streams, drawing bounding boxes, and UI overlays.

Conversational AI: Local LLM / RAG architecture to provide context-aware voice responses based on system logs.

Text-to-Speech (TTS): (e.g., pyttsx3 or Google TTS) for Aura's voice feedback.

Communication: WebSockets / Flask for low-latency video and data streaming from the Pi to the processing hub.

Hardware
Edge Compute: Raspberry Pi (Model 4/5 recommended for optimal streaming).

Vision Sensor: High-definition USB or Pi Camera module.

Proximity Sensor: Ultrasonic Sensor (e.g., HC-SR04).

Processing Hub: Laptop or dedicated onboard PC equipped with a decent GPU for running YOLOv8 smoothly.

🚀 Getting Started (Installation & Execution)
(Note: Adjust these steps based on your specific directory structure)

1. Hardware Setup:

Connect the camera and ultrasonic sensor to the Raspberry Pi.

Ensure the Raspberry Pi and the Processing Hub (Laptop) are on the same local network.

2. Raspberry Pi Node (Edge):

Bash

# Install dependencies
pip install -r edge_requirements.txt

# Run the sensor transmission script
python transmit_data.py --ip <LAPTOP_IP_ADDRESS>
3. Processing Hub (Laptop/PC):

Bash
# Navigate to the processing directory
cd ../processing_hub

# Install Python dependencies (Virtual environment recommended)
pip install -r requirements.txt

# Download YOLOv8 weights (if not included)
# Ensure your LLM environment is running (if using a local instance)

# Launch the main application and UI
python main_app.py
📊 System Effectiveness
The Aura Safety Scout pipeline is highly effective due to several core architectural decisions:

High Accuracy (Sensor Fusion): Relying solely on cameras can lead to false positives (shadows, reflections), while ultrasonic sensors alone cannot identify what the object is. Fusing YOLOv8's classification with exact ultrasonic distance mapping virtually eliminates false positives.

Low-Latency Edge Streaming: By offloading the heavy machine learning computation to a dedicated laptop/hub and only using the Pi for data collection, the system maintains high frames-per-second (FPS) crucial for highway speeds.

Reduced Cognitive Load: Traditional dash systems require drivers to take their eyes off the road to interpret complex UI diagrams. The conversational LLM agent allows the driver to keep their eyes forward while receiving precise auditory situational awareness.

Scalable Architecture: The modular separation between the edge node (sensors) and the processing hub mimics modern MLOps architectures, making it easy to swap in more powerful models (like future YOLO versions) without rebuilding the hardware.

For acessing the files Drive link:
https://drive.google.com/drive/folders/10YwvVb2m-2dhvnXVpWzIq7Xvpt9UW4WP?usp=sharing