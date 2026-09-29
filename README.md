# Low-SNR Spectrum Sensing using Graph Neural Networks
We did this research as a part of course ECE310- Wireless Communications under the guidance of Professor Dhaval Patel and TA Prapti Patel. 
ECE 310- Wireless Communication
                        SET OF INSTRUCTIONS AND EXECUTION


This repository contains code and a report for the SCM-GNN system, implementing a GNN pipeline for signal detection in wireless communication experiments. The files are organized as follows.
* GNN_dataset_Group8.ipynb- Dataset and .dat file generator for SCM-GNN.
* GNN_Patch_Group8.ipynb - Main SCM-GNN, PatchGNN, and PatchGNN+ model pipelines.
* SCM-GNN Pipeline Code - SCM-GNN standalone pipeline script.

## GNN_dataset_Generation.ipynb (Dataset Generator)
**Functionality**
Generates the simulation-based .dat datasets to be used with model pipelines; signal and noise, antenna, QPSK modulation, SNR level, and pulse shaping parameters mirror the published paper settings.
**Requirements**
1. Python 3.x, Jupyter/Colab
2. Required modules are Numpy, Scipy, torch , Os, Json ,matplotlib


**Setup & Installation**
      Install libraries as follows (in a Jupyter/Colab cell):
!pip install numpy scipy torch matplotlib
**Running**
1. Open the notebook in Jupyter/Colab.
2. Run each block in sequence to generate simulated multi-antenna IQ signals using the given parameters.
3. Save generated datasets as .dat binary files.
4. Visualize and verify sample waveforms to ensure proper signal generation.
5. Download all generated files as a zip if running in Colab.


Output files will be written into the current directory, or made available for download from Colab (e.g. Final-5dB.dat, etc.). 
## GNN_Patch_Group8.ipynb (SCM-GNN, PatchGNN, PatchGNN+ Models)
**Functionality**
Runs the SCM-GNN element-wise model and two versions of PatchGNN: Patch-based and Patch-based + Attention. Provides consistent train/test splits for fair comparisons and allows visualization of both results and comparisons.
**Requirements**
1. Python 3.x
2.  Jupyter/Colab (preferably with GPU)
3.  Required modules are Torch, Torchvision, torchaudio, Torch-geometric, Scikit-learn, matplotlib, For PyG (PyTorch Geometric) dependencies like Pyg_lib, torch_scatter, Torch_sparse, torch_cluster


**Setup & Installation**
1. Install main dependencies (Colab cell):
!pip install torch torchvision torchaudio torch-geometric scikit-learn matplotlib -q
2. For PyG (Colab):
!pip install -q pyg_lib torch_scatter torch_sparse torch_cluster torch_spline_conv torch_geometric -f https://data.pyg.org/whl/torch-2.1.0+cu121.html

**Running**
1. Place the .dat files generated in the previous step (.dat files with IQ data) in an accessible location (Colab/file path).
2. Specify the .dat file path at the top (dat_path = "/content/Final5dB.dat" for Colab).
3. Run notebook cells sequentially:
   * Parameter settings
   * Data loading & preprocessing (fromfile, SNR, windowing, etc.)
   * Feature and graph construction
   * Dataset creation and splitting
   * Model definition (SCM-GNN, PatchGNN, PatchGNN+)
   * Training/validation routines
   * Plotting ROC/Pd/Pf curves and comparisons
4. Adjust model parameters or architectures as desired in the code cells.
**Output**
Prints training/validation losses and AUC per epoch. Generates performance plots (AUC, ROC, Pd vs. SNR) comparing the performances of models.


  ## SCM-GNN Standalone Pipeline 
**Functionality**
This script is an end-to-end SCM-GNN runner: it loads IQ signals from .dat, frames the data, builds sample windows, adds noise, computes time-delay covariances, builds graphs, trains SCM-GNN, and evaluates ROC, accuracy, and Pd vs. SNR curves.


**Requirements**
1. Python 3.x
2. Required modules are Numpy, Torch, Torch_geometric, Matplotlib, sklearn


**Setup & Installation**
1. Install requirements:
pip install torch torch-geometric matplotlib scikit-learn numpy
2. For PyTorch Geometric (on CPU):
pip install torch-scatter torch-sparse torch-cluster torch-spline-conv torch-geometric

**Running**
1. Make sure your .dat file (e.g. ReadyMade_Dataset(FM).dat) is located in a path specified in the script as dat_path.
2. Edit the parameter variables at the top to change the sample size, SNR, number of windows, or graphing parameters.
3. Run the script, for example: python SCM_GNN_Pipeline.py. 


**Output**
It will show training progress, AUCs, accuracy, and plots will display ROC and performance curves. The script will save model results and can be further adapted to batch inference or other detection scenarios.
