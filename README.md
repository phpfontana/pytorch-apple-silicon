# PyTorch on Apple Silicon

This Repo is a step-by-step guide on how to install and run PyTorch on Apple Silicon Devices using Conda Package Manager.

**Requirements:**
  - Apple Silicon Mac (M1, M1 Pro, M1 Max, M1 Ultra, M2)
  - macOS 12.3+

## Setting up Miniconda3
**Step1.** Download and install `Miniconda3` from https://docs.conda.io/en/latest/miniconda.html. make sure to select `Miniconda3 macOS Apple M1 64-bit pkg` or `Miniconda3 macOS Apple M1 64-bit bash`. 

**Step2.** Restart Terminal.

## Setting up PyTorch environment
**Step1.** Open terminal and run the following command to create a directory to setup a PyTorch environment
```
mkdir pytorch-apple-silicon
cd pytorch-apple-silicon
```
### For the PyTorch Nightly build (w/ MPS Acceleration)
**Step2a.** Download and save `torch-nightly.yml` to `pytorch-apple-silicon` directory and execute the following command on the terminal to create an environment with `PyTorch Nightly` build and dependencies installed. Make sure to `cd` into the `pytorch-apple-silicon` directory before running the command.
```
conda env create -f torch-nightly.yml -n torch-nightly
```

### For the PyTorch Stable build (w/ CPU only)
**Step2b.** Download and save `torch-stable.yml` to `pytorch-apple-silicon` directory and execute the following command to create an environment with `PyTorch Stable` build and dependencies installed. Make sure to `cd` into the `pytorch-apple-silicon` directory before running the command.

```
conda env create -f torch-stable.yml -n torch-stable
```

**Step3.** Activate the chosen Conda environment.
```
conda activate torch-nightly

#or

conda activate torch-stable
```
**Step4.** Register Conda environment to python kernel. Make sure the environment is activated.
```
python -m ipykernel install --user --name=torch-nightly --display-name "Python 3.9 (torch-nightly)"

#or

python -m ipykernel install --user --name=torch-stable --display-name "Python 3.9 (torch-stable)"
```
**Step5.** Start Jupyter Notebook by running the following command on the terminal.
```
jupyter notebook
```
**Step6.** Create a new notebook by "New" -> "Notebook: Python 3.9(torch-nightly)" or "Notebook: Python 3.9(torch-stable)". and run the following command to verify dependencies and PyTorch version/GPU access
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
**Step7.** To run models with MPS (*Metal Performance Shaders*), set the device to `"mps"` with `.to(device)` (For PyTorch Nightly only)
```
import torch

# Set the device
device = "mps" if torch.backends.mps.is_available() else "cpu"

# Create data and send it to the device
x = torch.rand(size=(3, 4)).to(device)
x
```


