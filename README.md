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

Reboot your PC: 
```bash
sudo reboot
```
After rebooting check swap space  by using this command:   `free -h`

## Step 2: Setup Pre-installation (Python and pip)

Ensure your system is updated and install Python 3 along with the latest version of pip, which is needed to install Python libraries.

```bash
sudo apt update
sudo apt-get install python3-pip
sudo pip3 install -U pip testresources setuptools==49.6.0
```
(*Explanation: This step updates the system and installs `pip`, the package manager for Python, ensuring that dependencies can be easily installed. We also upgrade `setuptools` and `testresources` to ensure compatibility with other libraries.*)

## Step 3: Install Required Python Libraries for TensorFlow

TensorFlow requires several system libraries for running deep learning models. This step installs essential dependencies.

```bash
sudo apt-get install libhdf5-serial-dev hdf5-tools libhdf5-dev zlib1g-dev zip libjpeg8-dev liblapack-dev libblas-dev gfortran
```
(*Explanation: These are required libraries for TensorFlow, including support for HDF5 (used for model storage), compression (zlib), image processing (libjpeg), and math operations (liblapack, libblas).*)

## Step 4: Install Additional Python Libraries

Some additional Python libraries are needed for TensorFlow to run on Jetson Nano. The specified versions are chosen for compatibility with JetPack 4.6 and the Jetson environment.

```bash
sudo pip3 install -U --no-deps numpy==1.19.4 future==0.18.2 mock==3.0.5 keras_preprocessing==1.1.2 keras_applications==1.0.8 gast==0.4.0 protobuf pybind11 cython pkgconfig
```
(*Explanation: This installs necessary libraries like `numpy`, `keras_preprocessing`, and `protobuf`, which are used by TensorFlow to handle data, process models, and execute computations efficiently.*)

## Step 5: Numpy Setup (Handling Large Data in Binary Format)

Numpy is a core library for numerical computation. To enable handling of large datasets in binary format, install the specific version of  `h5py` and `numpy`.

```bash
sudo env H5PY_SETUP_REQUIRES=0 pip3 install -U h5py==3.1.0
```
(*Explanation: The `h5py` library is required for handling HDF5 files, and this command ensures compatibility with Numpy 1.19.4, which works well on Jetson Nano.*) <br>
(*If error shows for `h5py` and if you don't require the HDF5 then ignore it and ensure that other all dependencies are installed except related to HDF5.*) <br>
(*Usually it takes around 30 minutes to complete.*)

## Step 6: Install OpenCV

OpenCV is crucial for image processing and computer vision tasks.

```bash
sudo apt-get install python3-opencv
```
(*Explanation: This command installs the OpenCV library for Python, enabling the Jetson Nano to process images and video streams efficiently.*)

## Step 7: MediaPipe Setup

MediaPipe is a framework that helps with building machine learning pipelines. In this step, we clone the MediaPipe repository and install required OpenCV dependencies for building from source.

```bash
git clone https://github.com/google/mediapipe.git
cd mediapipe/
sudo apt-get install -y libopencv-core-dev libopencv-highgui-dev libopencv-calib3d-dev libopencv-features2d-dev libopencv-imgproc-dev libopencv-video-dev
sudo chmod 744 setup_opencv.sh
./setup_opencv.sh  # Installation takes around 30 minutes
```
(*Explanation: MediaPipe requires specific OpenCV components, and this script installs OpenCV from source to ensure compatibility with MediaPipe on Jetson Nano. The setup process may take some time, as OpenCV needs to be built and configured.*)

## Step 8: Install OpenCV Contrib

The `opencv_contrib` module provides extra functionalities that are not included in the main OpenCV distribution but are useful for advanced tasks like gesture recognition.

```bash
sudo pip3 install opencv_contrib_python
# Installation takes around 30 minutes for building dependencies
```
(*Explanation: The `opencv_contrib` package contains additional modules that enhance OpenCV’s functionality, including extra machine learning tools and computer vision algorithms.*)

## Step 9: Install MediaPipe Binaries for Jetson Nano

To optimize MediaPipe for Jetson Nano’s hardware, pre-built binaries are available. This step downloads and installs these optimized versions.

```bash
git clone https://github.com/PINTO0309/mediapipe-bin
cd mediapipe-bin/
sudo apt install curl
./v0.8.5/numpy119x/mediapipe-0.8.5_cuda102-cp36-cp36m-linux_aarch64_numpy119x_jetsonnano_L4T32.5.1_download.sh
sudo pip3 install numpy-1.19.4-cp36-none-manylinux2014_aarch64.whl
sudo pip3 install mediapipe-0.8.5_cuda102-cp36-none-linux_aarch64.whl
```
(*Explanation: This downloads MediaPipe binaries optimized for the Jetson Nano’s ARM architecture, ensuring the hand gesture recognition pipeline runs efficiently on the device.<br>
After cloning `mediapipe-bin` if it doesn't have direct `numpy119x` folder then it will have `zip` or `tar` file which you can unzip using `unzip filename`, you will find `mediapipe-0.8.5_cuda102-cp36-cp36m-linux_aarch64_numpy119x_jetsonnano_L4T32.5.1_download.sh` file there.*)

## Step 10: Install Dataclasses (for Python 3.6)

Since JetPack 4.6 uses Python 3.6, it may not have the `dataclasses` module, which is required for certain Python features. This step installs it.

```bash
pip3 install dataclasses
```
(*Explanation: The `dataclasses` module is included in Python 3.7+ by default, but for Python 3.6, it needs to be installed separately. This module is useful for creating class-like data structures.*)
