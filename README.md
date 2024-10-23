# JetsonNano-OpenCV-Mediapipe-SetUP
# (JetPack 4.6)

This guide walks through the process of setting up a Jetson Nano for the OpenCV and Mediapipe projects. The steps include configuring JetPack 4.6, installing necessary libraries, increasing swap memory for better performance, and setting up Python, TensorFlow, OpenCV, and MediaPipe.

## Step 1: Increase Swap Memory

Jetson Nano has limited RAM, and increasing swap memory helps improve performance, especially during intensive operations like training models or running complex applications.

```bash
git clone https://github.com/JetsonHacksNano/installSwapfile.git
cd installSwapfile/
./installSwapfile.sh
```

(*Explaination: The script increases the swap file size to allocate more virtual memory, improving system stability when handling memory-intensive processes.*)
