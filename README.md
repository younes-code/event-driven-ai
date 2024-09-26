# Event-Based Inference Pipeline

## Overview

This repository contains an event-based deep learning inference pipeline for gesture recognition using event-based cameras. The model uses the Metavision SDK and TorchScript for inference. 

## Prerequisites

Follow the installation guid to install Metavision SDK and all other dependencies:
- [Metavision SDK](https://docs.prophesee.ai/stable/installation/index.html), for event-based vision processing

## Pre-trained Models

Download the pre-trained model for classification from the link below:

- [Pre-trained Models](https://docs.prophesee.ai/stable/guides/pre-trained_models.html?highlight=mobilenetv2_chifoumi%20zip), for inference

## Running the Inference

To run the inference pipeline, use the following command:

```bash
python3 classification_inference.py /path/to/model_directory -p "/path/to/event_data.raw" --delta-t 10000 --cpu --height-width 720 1280
