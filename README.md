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
import sys
import torch
import sklearn 
import pandas as pd

# Verifying python version | package manager | 
print(f"Python {sys.version}\n")

print(f"PyTorch Version: {torch.__version__}")
print("MPS (Apple Metal) is AVAILABLE" if torch.backends.mps.is_available() else "CPU ONLY")

# Set the device      
device = "mps" if torch.backends.mps.is_available() else "cpu"
print(f"Target device is {device}")

print(f"\nScikit-Learn Version: {sklearn.__version__}")
print(f"Pandas Version: {pd.__version__}")
```
Output should be something like this:
```
Python 3.9.13 | packaged by conda-forge | [Clang 13.0.1 ]

PyTorch Version: 1.13.0.dev20220926
MPS (Apple Metal) is AVAILABLE
Target device is mps

Scikit-Learn Version: 1.1.2
Pandas Version: 1.5.0
```

