# deeplearningingenomics_spring2026

**Project Overview:**
Hi there! Thank you so much for checking out my final project: Predicting Clinvar pathogenicity using CNNs

This repository contains a pipeline for the binary classification of pathogenic vs benign variants from the ClinVar database. 

The Clinvar dataset may be accessed here: https://huggingface.co/datasets/songlab/clinvar 
The Human Hg38 fasta may be accessed from here: https://hgdownload.soe.ucsc.edu/goldenPath/hg38/bigZips/hg38.fa.gz

I evaluate four different 1D CNN architectures, trained on 512bp serquence wndows, and benchmark them against state of the art (SOTA) zero-shot models (like GPN-STAR, ESM-1b, etc). 

The purpose of this project is to ascertain the degree to which simpler, sequence-only CNN models compete with SOTA models for variant effect prediction, given the intense data and resources necessary to run these more advanced models. 
The project is not broken up into separate distinct blocks (but can easily be run and converted into a .ipynb/.py, either or). 

I first perform downloading of the hg38 reference FASTA and HuggingFace Clinvar dataset. Next, I extract a 512bp window centerd on a variant, producing two separate tensors (ref and alt) for both forward and reverse-complement strand. I then perform hyperparameter optiization using Weights & Biases (WandB) to find the best configuration for each architecture. The final evaluation uses stratified boostrapping to calculate AUROC, AUPRC, standard errors, and outputting a log-likelihood ratio. 

**Architectures:**
-Standard CNN
-Residual CNN
-Dilated CNN
-Inception CNN

**Installation + Requirements:**
To run, execute the cells sequentially in the .ipynb –– that's it! The notebook may show that it is invalid when you initially enter the window. Just download it, and it should run fine. For whatever reason, the preview is showing up incorrectly in some cases. 

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

**Before running, log into Weights and biases in your relevant directory:**
––––––––––
wandb login
––––––––––

**To run the pipeline, execute the script:**
––––––––––
python clinvar_cnn_task.py
––––––––––

**Key Findings:**
-Inception CNN outperforms Standard CNN, Residual CNN and Convolutional CNN in the initial hyperparameter tuning + validation auprc/auroc
-After further hyperparameter tuning on the inception CNN, the model outperforms **some** model implementations, but falls short across the board as compared to zero-shot predictions. Notably, it outperforms Nucleotide Transformer (~2.5B) in AUPRC and AUROC, despite having a fraction of the parameters (~42k) and resources necessary to train the model (1hr on x1 A100 GPU). 
-Evolutionary information can be very beneficial when originally training for masked-nucleotide-prediction, allowing for models to perform well on zero-shot clinvar pathogenicity classification!










