# 3D Object Detection for Autonomous Vehicles 🚗

## Project Overview

This project focuses on developing a computer vision system for autonomous vehicles by integrating depth estimation and object detection capabilities. Our goal was to build a perception system that can accurately detect and localize objects in 3D space, enabling safer autonomous navigation. The system combines models including DepthAnything for depth estimation and Detectron2 for object detection, resulting in accurate 3D scene understanding.

## Data Preparation and Validation

### Dataset Description
We utilized the nuScenes dataset, a large-scale dataset specifically designed for autonomous driving applications. The dataset provides rich sensor data including camera images, LiDAR scans, and detailed calibration information. For our development and testing, we primarily worked with the nuScenes mini dataset, which provides a representative subset of the full dataset while being more manageable for rapid development and validation.

### Data Processing Pipeline
Our processing pipeline consists of several key stages. First, we obtain camera images from the nuScenes dataset and process them through our depth estimation model, DepthAnything V2. The resulting depth maps are then combined with 2D object detections from Detectron2's Mask R-CNN model. We utilized the camera calibration data provided by nuScenes to accurately project our 2D detections into 3D space.

## Approach

### Selected Models
We implemented these models in our project:

1. DepthAnything V2: We selected this model for depth estimation because it provides highly accurate depth maps from single images without requiring stereo pairs or additional sensor data. The model uses a VITS encoder architecture and has been proven effective for autonomous driving scenarios.

2. Detectron2 with Mask R-CNN: Our object detection pipeline uses Detectron2's implementation of Mask R-CNN, pre-trained on the COCO dataset. This model provides detection capabilities across a wide range of object classes, with particular strength in detecting vehicles and other road users.


### Camera Calibration and Coordinate Transformation
One of the key technical challenges we addressed was the accurate transformation between 2D image space and 3D world coordinates. We leveraged the detailed calibration information provided by nuScenes, including both intrinsic and extrinsic camera parameters. This allowed us to accurately project our detections into 3D space and create reliable bird's eye view representations.

### Visualization Strategy
We used multiple visualization approaches, including:
- 3D cuboid visualization showing detected objects in three-dimensional space
- Bird's eye view projections for strategic planning and navigation
- Depth map visualizations using color mapping for intuitive depth understanding
- Integration with LiDAR point cloud data for validation and enhanced visualization

## Technical Implementation

### Model Integration
The integration of our different models required careful attention to coordinate systems and scale factors. For example, we needed to ensure that the depth maps from DepthAnything aligned properly with the object detections from Detectron2. 

### Feature Engineering
We developed several key features to enhance our system's capabilities:
- Integration of vehicle orientation estimation using map priors
- Depth aware object positioning with accurate scale estimation

## Results and Key Findings

Our system demonstrates the ability to create accurate 3D scene representations from single camera images. 

## Future Work

We've identified several areas for future improvement:
- In the future, we’d like to work on the accuracy of the model and work on detecting more objects in the scene.

## Setup Instructions

## Option 1: Google Colab (Recommended) 🚀

We recommend using Google Colab as it provides a pre configured environment with GPU support and all necessary dependencies.

1. Open the project notebook in Google Colab
2. All installation commands are included in the notebook
3. Run the cells in sequence to install dependencies and set up the environment

## Option 2: Local Setup 💻

If you prefer to run this project locally, follow these steps:

### Prerequisites
- Python 3.8 or higher
- CUDA-capable GPU (recommended)
- Git

### Installation Steps

First, clone the repository and set up your environment:

```bash
# Clone the repository
git clone [your-repo-url]
cd [your-repo-name]

# Create and activate a virtual environment
python -m venv venv

# On Windows:
venv\Scripts\activate

# On macOS/Linux:
source venv/bin/activate
```

Install the required packages:

```bash
# Install core dependencies
pip install -q "openvino>=2024.2.0" "datasets>=2.14.6" "nncf>=2.11.0" 
pip install -q "typing-extensions>=4.9.0" eval-type-backport "gradio>=4.19"

# Install machine learning frameworks
pip install -q "torch" "detectron2" "open3d" "plotly"

# Install dataset utilities
pip install -q "nuscenes-devkit"
```

Download and extract the nuScenes mini dataset:

```bash
# Download the dataset
wget https://www.nuscenes.org/data/v1.0-mini.tgz

# Create directory and extract
mkdir -p /data/sets/nuscenes
tar -xf v1.0-mini.tgz -C /data/sets/nuscenes
```

## Additional Notes

- GPU memory requirements: At least 8GB VRAM recommended
- Disk space: ~4GB required for the nuScenes mini dataset

## Acknowledgements

We would like to thank the teams behind DepthAnything and Detectron2 for their excellent models and documentation. Additionally, we're grateful to the nuScenes team for providing such a comprehensive dataset for autonomous driving research. 
 
A special thank you to our challenge advisors from Latitude AI and Breakthrough Tech for giving us the opportunity to work on this project!
