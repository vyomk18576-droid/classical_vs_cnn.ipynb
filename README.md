# Classical image processing techniques used for preprocessing before passing into CNN compared to normal images
## This project investigates the question: can classical image processing techniques improve deep learning performance.
## We combine:
### Classical preprocessing ( Histogram Equalization, CLAHE)
### Deep Learning (Custom Resnet in Tensorflow)

# Dataset
## Source: Kaggle Intel Image Classification dataset
## Classes:
## Buildings 
## Forest
## Glacier
## Mountain
## Sea 
## Street

# Total Images:
## Train: 14034 images
## Validation: 3000 images

# Pipeline

## Data loading
## tf.keras.utils.image_dataset_from_directory
## Image size: 128 x 128
## Batch Size: 32

## Preprocessing Variants
### We compare three pipelines:
| Method | Description                              |
| ------ | ---------------------------------------- |
| Raw    | No preprocessing                         |
| HE     | Histogram Equalization (global contrast) |
| CLAHE  | Adaptive histogram equalization          |

### Implemented using OpenCV inside Tensorflow pipelines

## Model Architecture
### Custom Resnet-style CNN
### Conv → BN → ReLU
### Residual Blocks with skip connections
### Downsampling via stride
### Global Average Pooling
### Dense (128) + Dropout (0.3)
### Softmax output

| Train | Validation | Accuracy          |
| ----- | ---------- | ----------------- |
| Raw   | Raw        | 70%               |
| HE    | HE         | 72%               |
| CLAHE | CLAHE      | 87% (Best)        |
| CLAHE | Raw        | 78%               |
| HE    | Raw        | 61%               |

# Key Insights
## 1. CLAHE dominates
### Best performance: 87% accuracy
### Improves contrast locally
### Helps model focus on fine textures

## 2. Domain Mismatch Hurts
### Training on CLAHE but validation on Raw --> performance drop
### Same for HE
### Conclusion: train and validation distributions must match or we need to fine tune accordingly

## 3. Classical + Deep Learning Combo is powerful
### Raw CNN: ~70%
### With CLAHE: + 17% improvement

### This is a huge gain, rarely achieved just by tuning architecture

## 4. HE is Unstable
### Over-enhances brightness
### Destroys natural image distribution
### Leads to poor generalization

# Evaluation Metrics
## Accuracy
## Confusion Matrix
## Precision/Recall/F1-score
### Example(HE):
### Accuracy: 0.72
### Balanced performance across all classes

# Tech Stack
## Tensorflow/ Keras
## OpenCV
## Numpy
## Matplotlib
## Scikit-learn


# How to run
## Install dependencies
## pip install tensorflow opencv-python matplotlib scikit-learn kaggle

## Download dataset via Kaggle API
## kaggle datasets download -d puneet6060/intel-image-classification
## unzip intel-image-classification.zip

# Future Work
## Add data augmentation vs CLAHE comparison
## Try EfficientNet/Vision Transformers
## Apply to:
### Medical imaging
### Industrial Inspection
## Combine CLAHE + augmentation

# Takeaway
## CLAHE is a high-impact, low-cost improvement
## Data preprocessing is as important as architecture
## Matching train/test distributions is critical

# Contributions
## Contributions and pull up requests are welcome








