# PyTorch on Apple Silicon

## Removing Conda Environment (Optional)


**Step1.** open terminal and run the following command to install `anaconda-clean` package. this package will uninstall anaconda distribution, which includes anaconda and miniconda.
```
conda install anaconda-clean
```
**Step2.** run the one of the following commands to remove miniconda/anaconda
```
anaconda-clean

# If you don't want to be asked about each file and directory
anaconda-clean --yes
```
**Step3.** there might be a few files left behind. To fix this, we can simply drag the remaining files to the trash.

**Step4.** Download and install `Miniconda3` from https://docs.conda.io/en/latest/miniconda.html. make sure to select `Miniconda3 macOS Apple M1 64-bit pkg` or `Miniconda3 macOS Apple M1 64-bit bash`. follow the steps it prompts you to go through after installation.

**Step5.** Restart Terminal.

## Setting up PyTorch environment

**Requirements:**
  - Apple Silicon Mac (M1, M1 Pro, M1 Max, M1 Ultra, M2)
  - macOS 12.3+

**Step1.** Open terminal and run the following command to create a directory to setup PyTorch environment
```
mkdir torch
cd torch
```
**Step2.** install jupyter 
```
conda install y- jupyter
```

**Step3a.** Download and save `pytorch-conda-nightly.yml` to `torch` directory and execute the following command to create an environment with pytorch-nightly (w/ MPS acceleration) and dependencies installed.
```
conda env create -f pytorch-conda-nightly.yml -n torch
```
**Step3b.** Download and save `pytorch-conda-stable.yml` to `torch` directory and execute the following command to create an environment with pytorch-stable (CPU only) and dependencies installed.
```
conda env create -f pytorch-conda-stable.yml -n torch
```
**Step4.** Activate Conda environment.
```
conda activate torch
```
**Step5.** Register Conda environment to python kernel. Make sure the environment is activated.
```
python -m ipykernel install --user --name=pytorch --display-name "Python 3.9 (pytorch)"
```
**Step6.** Start Jupyter Notebook by running the following command on the terminal.
```
jupyter notebook
```
**Step7.** Create a new notebook by "New" -> "Notebook: Python 3.9 (pytorch)". and run the following command to verify dependencies and PyTorch version/GPU access
```
import torch
import pandas as pd
import sklearn
import matplotlib.pyplot as plt

print(f"PyTorch version: {torch.__version__}")

# Check PyTorch has access to MPS (Metal Performance Shader, Apple's GPU architecture)
print(f"Is MPS (Metal Performance Shader) built? {torch.backends.mps.is_built()}")
print(f"Is MPS available? {torch.backends.mps.is_available()}")

# Set the device      
device = "mps" if torch.backends.mps.is_available() else "cpu"
print(f"Using device: {device}")
```
**Step8.** To run models with MPS (*Metal Performance Shaders*), set the device to `"mps"` with `.to(device)`
```
import torch

# Set the device
device = "mps" if torch.backends.mps.is_available() else "cpu"

# Create data and send it to the device
x = torch.rand(size=(3, 4)).to(device)
x
```


