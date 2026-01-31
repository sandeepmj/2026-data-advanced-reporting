# Installing Miniforge and Course Environment - Mac Instructions

This guide will walk you through setting up your Python environment for the Data Journalism course.

## What Are We Installing?

- **Miniforge:** A lightweight Python package manager
- **Python 3.11:** The programming language
- **Jupyter Notebook:** Interactive coding environment
- **Core data science packages:**
  - NumPy (numerical computing)
  - Pandas (data manipulation)
  - Matplotlib (visualization)
  - Seaborn (statistical visualization)
  - Plotly (interactive visualization)
  - Openpyxl (Excel file handling)

---

**Time required:** 30-45 minutes  
**What you'll install:** Miniforge (Python package manager) + dataj-installs environment

---

## Prerequisites

- Mac computer (Intel or Apple Silicon)
- xCode Command Line Tools installed ([instructions here](https://www.freecodecamp.org/news/install-xcode-command-line-tools/))
- The `environment.yml` file found at [this link](https://drive.google.com/file/d/1eAriTzDrTi4Ctw_NMiPbgvf8C35h0aEj/view?usp=sharing). These are prepacked instructions I created to make sure we all have the same environment.
- Removing Anaconda environment if you have it. Having both Anaconda and Miniforge will cause conflicts.

---

## Part 1: Check for Existing Anaconda Installation

### Step 1: Open Terminal
- Press `Cmd + Space` → type "Terminal" → press Enter

### Step 2: Check if you have Anaconda/Miniconda
Type this command and press Enter:
```bash
which conda
```

**If you see:**
- `conda not found` → **Skip to Part 2** (you're good to go!)
- `/opt/anaconda3/bin/conda` → **Continue to Uninstall Steps below**
- `/Users/yourname/anaconda3/bin/conda` → **Continue to Uninstall Steps below**

---

## Uninstall Anaconda/Miniconda (If Present)

**IMPORTANT:** Having both Anaconda and Miniforge will cause conflicts. You must uninstall Anaconda first.

### Step 1: Install anaconda-clean
```bash
conda install anaconda-clean
```
Press `y` when prompted.

### Step 2: Run the cleaner
```bash
anaconda-clean --yes
```

### Step 3: Remove the Anaconda directory
```bash
sudo rm -rf /opt/anaconda3
```
You'll be asked for your Mac password (you won't see characters as you type - this is normal).

If your Anaconda is in a different location, use:
```bash
sudo rm -rf ~/anaconda3
# or
sudo rm -rf ~/miniconda3
```

### Step 4: Remove hidden conda files
```bash
rm -rf ~/.conda
rm -rf ~/.condarc
```

### Step 5: Clean up shell configuration
Open your shell configuration file:
```bash
nano ~/.zshrc
```

Look for and **DELETE** the entire block that looks like this:
```bash
# >>> conda initialize >>>
# ... multiple lines ...
# <<< conda initialize <<<
```

Save and exit:
- Press `Ctrl+X`
- Press `Y`
- Press `Enter`

### Step 6: Restart Terminal
Close Terminal completely and open a new Terminal window.

### Step 7: Verify removal
```bash
which conda
```

Should show: `conda not found` 

---

## Part 2: Install Miniforge

### Step 1: Download Miniforge
In Terminal, run this command:
```bash
curl -L -O "https://github.com/conda-forge/miniforge/releases/latest/download/Miniforge3-$(uname)-$(uname -m).sh"
```

This downloads the correct installer for your Mac automatically.

### Step 2: Run the installer
```bash
bash Miniforge3-$(uname)-$(uname -m).sh
```

**During installation:**

1. **License agreement:** Press `Enter` to scroll through, then type `yes`

2. **Installation location:** Press `Enter` to accept the default location

3. **Initialize Miniforge?** Type `yes` (IMPORTANT!)

### Step 3: Restart Terminal
Close Terminal completely and open a new Terminal window.

### Step 4: Verify installation
```bash
conda --version
```
Should show something like: `conda 25.11.0` 

```bash
mamba --version
```
Should show something like: `mamba 2.4.0` 

---

## Part 3: Configure Conda

### Step 1: Set conda-forge as default channel
```bash
conda config --add channels conda-forge
conda config --set channel_priority strict
```

### Step 2: Disable auto-activation (optional but recommended)
```bash
conda config --set auto_activate_base false
```

### Step 3: Restart Terminal
Close and reopen Terminal. Your prompt should no longer show `(base)`.

---

## Part 4: Check for Python Alias Issues

### Step 1: Check if python is aliased
```bash
which python
```

**If you see:**
- `python not found` or `/Users/yourname/miniforge3/...` → **You're good! Skip to Part 5**
- `python: aliased to /usr/bin/python3` → **Continue to fix it below**

### Step 2: Remove the python alias
```bash
nano ~/.zshrc
```

Look for and **DELETE** or comment out (add `#` at the beginning) any line like:
```bash
alias python=/usr/bin/python3
```

Save and exit:
- Press `Ctrl+X`
- Press `Y`
- Press `Enter`

### Step 3: Reload configuration
```bash
source ~/.zshrc
```

---

## Part 5: Create Your Course Environment

### Step 1: Navigate to where you saved environment.yml
If it's in Downloads:
```bash
cd ~/Downloads
```

If it's on Desktop:
```bash
cd ~/Desktop
```

### Step 2: Create the environment
```bash
mamba env create -f environment.yml
```

**This will take 2-3 minutes.** You'll see packages downloading and installing.

When prompted with `Confirm changes: [Y/n]`, type `Y` and press Enter.

### Step 3: Activate the environment
```bash
conda activate dataj-installs
```

Your prompt should change to:
```
(dataj-installs) ➜  ~
```

---

## Part 6: Test Your Installation

### Step 1: Check Python version
```bash
python --version
```
Should show: `Python 3.11.14` 

### Step 2: Launch Jupyter
```bash
jupyter notebook
```

Your browser should open with Jupyter.

### Step 3: Test packages
Create a new notebook (New → Python 3) and run this code:

```python
import sys
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
import plotly.express as px
import matplotlib
from openpyxl import Workbook

print(f"Python: {sys.version}")
print(f"NumPy: {np.__version__}")
print(f"Pandas: {pd.__version__}")
print(f"Matplotlib: {matplotlib.__version__}")
print(f"Seaborn: {sns.__version__}")
print(f"Plotly: {px.__version__}")
print("\n All packages loaded successfully!")
```

**If all packages load without errors, you're done!** 

### Step 4: Stop Jupyter
In Terminal, press `Ctrl+C` (press twice if needed)

### Step 5: Deactivate environment
```bash
conda deactivate
```

---

## Setup Verification Checklist

Before submitting your setup verification, confirm:

-  `which conda` shows miniforge path (NOT anaconda)
-  `conda activate dataj-installs` changes your prompt to `(dataj-installs)`
-  `which python` shows miniforge path (NOT `/usr/bin/python` or aliased)
-  `python --version` shows `Python 3.11.14`
-  Jupyter launches successfully
-  All packages import without errors

---

## Daily Usage (After Installation)

To use Jupyter for coursework:

```bash
# 1. Open Terminal
# 2. Activate environment
conda activate dataj-installs

# 3. Navigate to your work folder
cd ~/Desktop

# 4. Launch Jupyter
jupyter notebook

# ... do your work ...

# 5. Stop Jupyter: Ctrl+C
# 6. Deactivate: 
conda deactivate
```

---

## Troubleshooting

### "conda: command not found"
**Solution:** Restart Terminal or run:
```bash
source ~/.zshrc
```

### "python --version" shows wrong version (like 3.9.6)
**Solution:** You have a python alias. Follow Part 4 instructions.

### Packages not found in Jupyter
**Solution:** Make sure you:
1. Activated the environment BEFORE launching Jupyter
2. Selected "Python 3 (ipykernel)" kernel in Jupyter

### "Environment already exists"
**Solution:** Delete and recreate:
```bash
conda env remove -n dataj-installs
mamba env create -f environment.yml
```

### Installation taking forever
**Solution:** Use `mamba` instead of `conda` - it's much faster:
```bash
mamba env create -f environment.yml
```

---

## Getting Help

If you encounter issues not covered here:
1. Take a screenshot of the error
2. Note what command you ran
3. Come to office hours or post on the course discussion board

---



**Congratulations! Your Python environment is ready for the course!** 
