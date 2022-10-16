# PyTorch on Apple Silicon

This Repo is a step-by-step guide on how to install and run PyTorch on Apple Silicon Devices using Conda Package Manager.

**Requirements:**
  - Apple Silicon Mac (M1, M1 Pro, M1 Max, M1 Ultra, M2)
  - macOS 12.3+

## Setting up Miniconda3
**Step1.** Download and install `Miniconda3` from https://docs.conda.io/en/latest/miniconda.html. Make sure to select `Miniconda3 macOS Apple M1 64-bit pkg` or `Miniconda3 macOS Apple M1 64-bit bash`. Execute and follow installation prompts.

**Step2.** Open terminal and install `xcode-select` by using the following command. It is also possible to install Xcode from the App Store.
```
xcode-select --install
```

## Setting up PyTorch environment
**Step1.** Open terminal and run the following command to create a directory to setup a PyTorch environment
```
mkdir torch
cd torch
```
### PyTorch Nightly build (MPS Acceleration)
**Step2a.** Download and save `torch-nightly.yml` to `torch` directory and execute the following command on the terminal to create an environment with `PyTorch Nightly` build and dependencies installed. Make sure to `cd` into the `torch` directory before running the command.
```
conda env create -f torch-nightly.yml -n torch
```

### PyTorch Stable build (CPU only)
**Step2b.** Download and save `torch-stable.yml` to `torch` directory and execute the following command to create an environment with `PyTorch Stable` build and dependencies installed. Make sure to `cd` into the `torch` directory before running the command.

```
conda env create -f torch-stable.yml -n torch
```

**Step3.** Activate the Conda environment.
```
conda activate torch
```
**Step4.** Register Conda environment to python kernel. Make sure the environment is activated.
```
python -m ipykernel install --user --name=torch --display-name "Python 3.9 (torch)"

```
**Step5.** Start Jupyter Notebook by running the following command on the terminal.
```
jupyter notebook
```
**Step6.** Create a new notebook with "Python 3.9 (torch)" kernel. 

**Step7.** Run the following command to verify dependencies and PyTorch version/GPU access
```
import sys
import torch
import sklearn 
import pandas as pd

# Verifying python version | package manager | 
print(f"Python {sys.version}\n")

print(f"PyTorch Version: {torch.__version__}")
print("MPS (Apple Metal) AVAILABLE" if torch.backends.mps.is_available() else "CPU ONLY")

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

