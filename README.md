# Event-Based Inference Pipeline

## Overview

This repository provides a comprehensive framework for gesture recognition and object detection using event-based cameras. Follow the guidelines to set up the environment and run the inference pipelines efficiently. The model uses the Metavision SDK


## Prerequisites
Follow the installation guid to install Metavision SDK and all other dependencies:
- [Metavision SDK](https://docs.prophesee.ai/stable/installation/index.html), for event-based vision processing

## Pre-trained Models

Download the pre-trained model for classification from the link below:

- [Pre-trained Models](https://docs.prophesee.ai/stable/guides/pre-trained_models.html?highlight=mobilenetv2_chifoumi%20zip), for inference.

Place the downloaded model in the `models/` directory of the project.

## Running the Inference for Gesture Recognition

To run the inference pipeline, use the following command [Doc](https://docs.prophesee.ai/stable/samples/modules/ml/classification_inference.html#chapter-samples-ml-classification-inference):

```bash
python3 classification_inference.py /path/to/model_directory -p "/path/to/event_data.raw" --delta-t 10000 --cpu --height-width 720 1280

Input Parameters
- torchscript_dir: Path to the directory containing the TorchScript model and its JSON description.
- -p / --path: Specify the RAW, HDF5, or DAT filename for the event data. Leave this blank to use a camera.
- -w /path/to/output: to generate a mp4 video
- --delta-t: Duration of the time slice (in microseconds) in which events are accumulated to compute features. 
Normally you should set the accumulation time interval (--delta-t) the same value as the one during the training. 
But if there is bandwidth constraint to run it live, you can try to increase the value accordingly, at a potential loss of accuracy.
- --cpu: Use this flag to run the inference on the CPU instead of the GPU.
- --height-width: The height and width of the input images. This should be provided as two integers. The dimensions must be negative powers of two relative to the original input size captured (720/1280).

1- Valid Height Options: Start with the original height (720) and divide by 2𝑛 (where 𝑛 is a non-negative integer) until the value is no longer positive:
- 720 (720 / 2^0)
- 360 (720 / 2^1)
- 180 (720 / 2^2)
- 90 (720 / 2^3)
- 45 (720 / 2^4)

2- Valid Width Options: Start with the original width (1280) and follow the same division:
- 1280 (1280 / 2^0)
- 640 (1280 / 2^1)
- 320 (1280 / 2^2)
- 160 (1280 / 2^3)
- 80 (1280 / 2^4)   
```

## Running the Inference for Detection and Tracking

To run the inference pipeline, use the following command [Doc](https://docs.prophesee.ai/stable/samples/modules/ml/detection_and_tracking_inference_py.html#chapter-samples-ml-detection-and-tracking-inference-python):

```bash
python3 detection_and_tracking_pipeline.py --object_detector_dir /path/to/model_directory --record_file "/path/to/event_data.raw/driving_sample.raw" --display cpu --network_input_width 640 --network_input_height 480


Input Parameters
- --object_detector_dir: Path to the directory containing the object detection model.
- --record_file: Specify the RAW file containing the ego dash cam event data.
- --display: Flag to display the output in real-time.
- --cpu: Use this flag to run the inference on the CPU instead of the GPU.
- --network_input_width: Width of the input images. Options can be 640, 320, 160, or 80.
- --network_input_height: Height of the input images. Options can be 480, 240, 120, or 60.
```

## Notes
- Ensure you have the necessary pre-trained models in the models/ directory.
- Adjust the input dimensions based on your requirements for performance versus accuracy.
