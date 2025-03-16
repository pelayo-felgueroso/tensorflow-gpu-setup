# tensorflow-gpu-setup
Step-by-step guide to installing TensorFlow with GPU support on Conda.

**After days of struggling, I finally found a solution that works.**  
I've seen countless Reddit and YouTube posts from people saying that **TensorFlow won’t run on their GPU**, and that tutorials don’t work due to **version conflicts**. Many guides are outdated or miss crucial details, leading to frustration.

After experiencing the same issues, I found a solution using **Python virtual environments**. This ensures TensorFlow runs in an **isolated** setup, fully compatible with **CUDA and cuDNN**, while preventing conflicts with other projects.

**My specs:**

* **OS:** Windows 11
* **CPU:** Intel Core i7-11800H
* **GPU:** Nvidia GeForce RTX 3060 Laptop GPU
* **Driver Version:** 572.16
* **RAM:** 16GB
* **Python Version:** 3.12.6 (global) but using **Python 3.10** in Conda
* **CUDA Version:** 12.3 (global) but using **CUDA 11.2** in Conda
* **cuDNN Version:** 8.1

# Step-by-Step Installation:

# 1. Install Miniconda (if you don’t have it)

Download `.exe` file:  
[Miniconda3 Windows 64-bit](https://repo.anaconda.com/miniconda/Miniconda3-latest-Windows-x86_64.exe)  
Or Download the Miniconda installer by yourself here:  
[Miniconda installer link](https://docs.anaconda.com/miniconda/)  
During installation, DO NOT check "Add Miniconda to PATH" to avoid conflicts with other Python versions.  
Complete the installation and restart your computer.

After installing Miniconda, open **CMD** or **PowerShell** and run:

    conda --version

If you see something like:

    conda 25.1.1

Miniconda is installed correctly.

# 2. Create a Virtual Environment with Python 3.10

Open **Anaconda Prompt** or **PowerShell** and run:

    conda create --name tf-2.10 python=3.10

Once created, initiate it:

    conda init

Once initiated, close and reopen **PowerShell,** then activate it:

    conda activate tf-2.10

# 3. Fix NumPy Version to Avoid Import Errors

TensorFlow 2.10 does **not** support NumPy 2.x. If you installed it already, downgrade it:

    pip install numpy==1.23.5

# 4. Install TensorFlow 2.10 (Compatible with GPU)

    pip install tensorflow==2.10

**Note:** Newer TensorFlow versions **(2.11+) dropped support for CUDA 11**, so **2.10 is the last version that supports it!**

# 5. Install Correct CUDA and cuDNN Versions

TensorFlow 2.10 **requires CUDA 11.2 and cuDNN 8.1**. Install them inside Conda:

    conda install -c conda-forge cudatoolkit=11.2 cudnn=8.1

# 6. Verify Installation

Run this in Python:

    import tensorflow as tf
    print("TensorFlow version:", tf.__version__)
    print("GPUs available:", tf.config.list_physical_devices('GPU'))

Expected Output:

    TensorFlow version: 2.10.0
    GPUs available: [PhysicalDevice(name='/physical_device:GPU:0', device_type='GPU')]

If the **GPU list is empty (**`[]`**)**, TensorFlow is running on the **CPU**. Try restarting your terminal and running again.

# 7. (Optional) Set Up TensorFlow in PyCharm

If you're using **PyCharm**, you need to manually add the Conda environment:

1. Go to **File > Settings > Project: <YourProject> > Python Interpreter**.
2. Click **Add Interpreter > Add Local Interpreter**.
3. Select **Existing Environment** and browse to: C:\\Users\\<your\_username>\\miniconda3\\envs\\tf-2.10\\python.exe
4. Select your **Environment** : tf-2.10
5. Click **OK**.

# Done!
