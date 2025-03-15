# Deeply synergistic optical and SAR time series for crop dynamic monitoring

This project addresses the challenge of missing optical data—specifically NDVI—caused by heavy cloud cover in remote sensing imagery. By leveraging complementary radar data (VH from Sentinel-1) alongside optical data (NDVI from Sentinel-2), we develop a deep learning solution to impute missing optical information, enhancing our ability to monitor vegetation health in challenging environments.

# Project Overview
# Objective:
To use a fusion of radar and optical data to reconstruct missing NDVI values. Our approach capitalizes on the cloud-penetrating capabilities of radar and the rich spectral detail of optical imagery, ensuring more complete and accurate vegetation monitoring.

# Approach:
[Access the dataset on Google Drive](https://drive.google.com/drive/u/0/folders/1DznFw7cS4hcoihAspkqtyTHJYMZjL4iD)

Data Fusion:

Optical Data: NDVI is computed from Sentinel-2 imagery.
Radar Data: VH polarization data from Sentinel-1 is used to complement the optical data, particularly where cloud cover obscures the view.
Deep Learning Inpainting:
A Vision Transformer (ViT)-based model is designed and trained to inpaint missing NDVI values using the combined information from both data sources.

Pipeline Enhancements:
The workflow incorporates data normalization, augmentation, a deeper and wider transformer model architecture, extended training, and GPU-accelerated mixed precision training.

Data Retrieval from Google Earth Engine
Data is retrieved from Google Earth Engine (GEE) over a one-year period covering a portion of the Amazon forest. The key steps include:

Sentinel-2 Data Retrieval:
Acquiring cloud-masked Sentinel-2 imagery and computing NDVI from the optical bands.

Sentinel-1 Data Retrieval:
Extracting radar imagery (VH polarization) to capture surface details that remain consistent regardless of cloud cover.

Temporal Compositing:
Creating 8-day composites for both datasets to generate a temporally consistent input, which is then exported as a multi-channel GeoTIFF to Google Drive.

This fused dataset (combining NDVI and VH) forms the basis of our deep learning pipeline.
![image](https://github.com/user-attachments/assets/9a41b648-0eae-4740-84fb-2ee6966f3ed5)

# Key Components
Data Pipeline:

Retrieval & Preprocessing: Data is fetched from GEE, where NDVI is computed from Sentinel-2 and radar VH data is acquired from Sentinel-1.
Normalization & Augmentation: The dataset is normalized per channel, and data augmentation (flips, rotations) is applied to improve model generalization.
Simulation of Missing Data: Artificial gaps are introduced in the NDVI channel to mimic cloud-induced missing data.
Model Architecture:

Vision Transformer (ViT): The model splits input patches into smaller segments, embeds them, and processes them through transformer encoder layers.
Reconstruction: The transformer outputs are used to reconstruct the full patch, effectively inpainting the missing NDVI data using complementary VH information.
Training:

Extended Training: The model is trained over multiple epochs with a reconstruction loss (MSE), and hyperparameters are tuned for optimal performance.
GPU and Mixed Precision: Training leverages GPU acceleration and mixed precision (AMP) for efficiency.
<img width="538" alt="image" src="https://github.com/user-attachments/assets/ac55180b-6727-42e6-81d4-827f3c34ab2c" />

# Outcome
The model successfully reconstructs missing NDVI values by fusing radar and optical data. Visualizations of the imputed NDVI demonstrate that our approach provides a robust solution for monitoring vegetation in regions frequently obscured by clouds, such as the Amazon forest.

