# deeplearningingenomics_spring2026
Hi there! Thank you so much for checking out my final project: Predicting Clinvar pathogenicity using CNNs

This repository contains a pipeline for the binary classification of pathogenic vs benign variants from the ClinVar database. I evaluate four different 1D CNN architectures, trained on 512bp serquence wndows, and benchmark them against state of the art (SOTA) zero-shot models (like GPN-STAR, ESM-1b, etc). 

Project Overview:
The project is not broken up into separate distinct blocks (but can easily be run and converted into a .ipynb/.py, either or). 

I first perform downloading of the hg38 reference FASTA and HuggingFace Clinvar dataset. Next, I extract a 512bp window centerd on a variant, producing two separate tensors (ref and alt) for both forward and reverse-complement strand. I then perform hyperparameter optiization using Weights & Biases (WandB) to find the best configuration for each architecture. The final evaluation uses stratified boostrapping to calculate AUROC, AUPRC, standard errors, and outputting a log-likelihood ratio. 

Architectures:
-Standard CNN
-Residual CNN
-Dilated CNN
-Inception CNN

Installation + Requirements:
To run, execute the cells sequentially in the .ipynb –– that's it! The notebook will show that it is invalid when you click on it. Just download it, and it should run fine. For whatever reason, the preview is showing up incorrectly. 

If not running in a .ipynb Jupyter notebook, download as a .py and create/activate a conda environment:
–––––––––––––
# create conda env and activate it 
conda create -n clinvar_env python=3.11 -y
conda activate clinvar_env

# install packages
conda install pytorch torchvision torchaudio pytorch-cuda=11.8 -c pytorch -c nvidia

# install other dependencies
pip install pyfaidx wandb datasets huggingface_hub pandas numpy scikit-learn matplotlib seaborn tqdm 
––––––––––––––

Before running, log into Weights and biases in your relevant directory: 
––––––––––
wandb login
––––––––––

To run the pipeline, execute the script:
––––––––––
python clinvar_cnn_task.py
––––––––––



