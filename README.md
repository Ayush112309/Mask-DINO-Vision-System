Mask-DINO Vision System

An end-to-end computer vision system for industrial visual inspection using the Mask-DINO transformer architecture for object detection and instance segmentation.

The system is designed to identify and localize surface defects such as cracks and corrosion while simultaneously generating pixel-level instance masks. The pipeline combines dataset preprocessing, spatial augmentation, transformer-based detection and segmentation, GPU inference optimization, and quantitative evaluation.

Overview

Automated visual inspection is a critical component of modern manufacturing, where reliable detection of surface defects is required for quality assurance and process monitoring.

This project implements a transformer-based vision pipeline capable of performing:

Object detection
Instance segmentation
Surface-defect localization
Pixel-level defect segmentation
Real-time GPU inference
Quantitative detection and segmentation evaluation

The system is built around Mask-DINO, a transformer-based architecture that performs object detection and instance segmentation using query-based prediction rather than traditional anchor-based detection.

Key Results
Metric	Performance
mAP	46.8
Inference throughput	38 FPS
Evaluation range	IoU 0.50–0.95
Task	Detection + Instance Segmentation
Deployment target	Real-time industrial inspection

The optimized GPU inference pipeline achieves approximately:

38
 
F
P
S

with a detection performance of:

46.8
 
m
A
P

Key Features
End-to-end Mask-DINO transformer pipeline
Object detection and instance segmentation
Fine-tuning on annotated industrial datasets
Surface-defect detection
Crack and corrosion segmentation
OpenCV-based preprocessing
Spatial data augmentation
Query-based, anchor-free prediction
GPU-optimized inference
Real-time processing
Bounding-box evaluation
Pixel-level segmentation evaluation
IoU-based performance analysis
Automated visual inspection workflow
System Architecture
                    Input Image
                         │
                         ▼
                ┌─────────────────┐
                │ OpenCV           │
                │ Preprocessing    │
                └────────┬────────┘
                         │
                         ▼
                ┌─────────────────┐
                │ Spatial         │
                │ Augmentation    │
                └────────┬────────┘
                         │
                         ▼
                ┌─────────────────┐
                │ Mask-DINO       │
                │ Transformer     │
                └────────┬────────┘
                         │
                ┌────────┴─────────┐
                ▼                  ▼
        Object Detection    Instance Segmentation
                │                  │
                ▼                  ▼
         Bounding Boxes       Instance Masks
                │                  │
                └────────┬─────────┘
                         ▼
                 Visual Inspection
                         │
                         ▼
                 Quality Assessment

Mask-DINO Architecture

The system uses Mask-DINO, a transformer-based architecture designed for unified object detection and segmentation.

The model processes an input image and generates object-level predictions through learned queries.

The overall prediction process can be represented as:

𝐼
→
Backbone
→
Feature Representation
→
Transformer Encoder/Decoder
→
Object Queries
→
{
Bounding Boxes


Class Labels


Instance Masks

Unlike conventional anchor-based object detectors, the query-based formulation directly predicts object instances through transformer queries.

Dataset Preparation

The model is fine-tuned using annotated surface-defect datasets.

Each training sample consists of an image and corresponding annotations for defect instances.

Typical annotation information includes:

Defect class
Bounding-box coordinates
Instance segmentation mask

The dataset can be used for detecting defects such as:

Cracks
Corrosion
Surface damage
Manufacturing defects
Image Preprocessing

OpenCV is used for image preprocessing and data preparation.

Typical preprocessing operations include:

Image resizing
Normalization
Color-space processing
Image formatting
Annotation transformation
Dataset validation

The preprocessing pipeline ensures that images and corresponding annotations remain spatially consistent throughout training.

Data Augmentation

Extensive spatial augmentation is used to improve model generalization.

Augmentation strategies may include:

Horizontal flipping
Vertical flipping
Random scaling
Random cropping
Rotation
Translation
Resizing
Spatial transformations

For segmentation tasks, augmentation is applied consistently to both:

Image
↔
Segmentation Mask

to preserve pixel-level correspondence.

Model Fine-Tuning

The pretrained Mask-DINO model is fine-tuned on the target industrial defect dataset.

The training workflow consists of:

Pretrained Mask-DINO
        ↓
Dataset Preparation
        ↓
OpenCV Preprocessing
        ↓
Spatial Augmentation
        ↓
Model Fine-Tuning
        ↓
Validation
        ↓
Performance Evaluation


Fine-tuning allows the pretrained transformer representation to adapt to the visual characteristics of industrial surface defects.

Anchor-Free Query Matching

Mask-DINO uses a query-based detection formulation rather than relying on traditional predefined anchor boxes.

The transformer predicts a set of object queries:

𝑄
=
{
𝑞
1
,
𝑞
2
,
…
,
𝑞
𝑁
}

Each query can correspond to a detected object instance.

The prediction includes:

𝑞
𝑖
→
{
class
,
bounding box
,
mask
}

This provides a unified representation for both detection and instance segmentation.

Instance Segmentation

For each detected defect instance, the model generates a pixel-level mask.

The segmentation output can be represented as:

𝑀
𝑖
(
𝑥
,
𝑦
)
∈
[
0
,
1
]

where $M_i(x,y)$ represents the predicted probability that pixel $(x,y)$ belongs to instance $i$.

This allows the system to determine not only where a defect is located, but also which pixels belong to that defect.

Industrial Visual Inspection

The trained model can be integrated into an automated inspection pipeline:

Manufacturing Line
        │
        ▼
    Camera Feed
        │
        ▼
   Image Capture
        │
        ▼
   Preprocessing
        │
        ▼
   Mask-DINO GPU
      Inference
        │
        ├───────────────┐
        ▼               ▼
  Defect Detection   Defect Mask
        │               │
        └───────┬───────┘
                ▼
        Quality Assessment
                │
                ▼
        Inspection Decision


This architecture enables automated detection of surface abnormalities in manufacturing environments.

Evaluation

The model is evaluated using standard object-detection and instance-segmentation metrics.

Mean Average Precision

The primary detection metric is:

m
A
P

with evaluation performed across multiple IoU thresholds.

The reported performance is:

46.8
 
m
A
P

Intersection over Union

Detection and segmentation quality are evaluated using Intersection over Union:

𝐼
𝑜
𝑈
=
∣
𝐴
∩
𝐵
∣
∣
𝐴
∪
𝐵
∣

where:

$A$ = predicted region
$B$ = ground-truth region

Higher IoU indicates stronger spatial agreement between prediction and ground truth.

IoU Evaluation

The model is evaluated across the standard:

𝐼
𝑜
𝑈
=
0.50
:
0.95

range.

This provides a more rigorous assessment than evaluating at a single IoU threshold.

The evaluation considers increasingly strict overlap requirements between predicted and ground-truth regions.

Performance

The optimized inference pipeline achieves:

Detection Performance

46.8
 
m
A
P

Real-Time Throughput

38
 
F
P
S

This corresponds to approximately:

1
38
≈
26.3
 
m
s
/
f
r
a
m
e

of average processing time at the reported throughput.

The combination of detection accuracy and inference speed makes the system suitable for investigating real-time industrial inspection applications.

GPU Inference Optimization

The inference pipeline is optimized for GPU execution to achieve real-time throughput.

Optimization focuses on:

GPU-based model execution
Efficient tensor processing
Batched operations where applicable
Reduced preprocessing overhead
Efficient image-to-tensor conversion
Optimized post-processing
Memory-efficient inference

The resulting pipeline reaches approximately:

38
 
F
P
S

under the reported evaluation configuration.

Detection vs. Segmentation

The system provides two complementary outputs.

Capability	Output
Object Detection	Bounding boxes
Classification	Defect classes
Instance Segmentation	Pixel-level masks
Localization	Defect position
Inspection	Defect presence and extent

Bounding boxes provide coarse localization, while instance masks provide detailed information about the actual defect region.

Technology Stack
Technology	Purpose
Python	Core implementation
PyTorch	Deep-learning framework
Mask-DINO	Detection + segmentation architecture
OpenCV	Image processing and augmentation
CUDA	GPU acceleration
NumPy	Numerical operations
End-to-End Pipeline

The complete workflow is:

Dataset
   │
   ▼
Annotation Validation
   │
   ▼
OpenCV Preprocessing
   │
   ▼
Spatial Augmentation
   │
   ▼
Mask-DINO Fine-Tuning
   │
   ▼
Validation
   │
   ▼
GPU Inference Optimization
   │
   ▼
Bounding Boxes + Instance Masks
   │
   ▼
IoU / mAP Evaluation
   │
   ▼
Real-Time Visual Inspection

Applications

The system can be adapted for automated inspection tasks including:

Surface crack detection
Corrosion detection
Metal-surface inspection
Manufacturing defect detection
Structural inspection
Component quality control
Automated production-line inspection
Infrastructure monitoring
Future Development

Potential extensions include:

Multi-camera inspection
Video-based defect tracking
Temporal consistency for segmentation
Model quantization
TensorRT deployment
Edge-GPU deployment
Model pruning
Knowledge distillation
Defect severity estimation
Defect-area quantification
Automated quality scoring
Active-learning-based dataset expansion
Uncertainty estimation
Real-time manufacturing-line integration
Project Impact

This project demonstrates the application of modern transformer-based computer vision to an industrial inspection problem.

The combination of:

Transformer Vision + Instance Segmentation + GPU Optimization + Quantitative Evaluation

provides a foundation for developing automated quality-control systems capable of detecting and precisely localizing manufacturing defects.

Performance Summary
Metric	Result
Architecture	Mask-DINO
Task	Object Detection + Instance Segmentation
mAP	46.8
Throughput	38 FPS
Evaluation	IoU 0.50–0.95
Application	Industrial Visual Inspection
Target Defects	Cracks / Corrosion
Author

Ayush

Computer vision and machine-learning project focused on transformer-based object detection, instance segmentation, and automated industrial quality inspection.

License

This project may be distributed under an appropriate open-source license such as the MIT License.

Keywords

Mask-DINO · Computer Vision · Object Detection · Instance Segmentation · Transformers · PyTorch · OpenCV · GPU Inference · Industrial Inspection · Defect Detection · Quality Control · Deep Learning