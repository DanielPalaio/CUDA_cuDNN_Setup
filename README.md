# NVIDIA CUDA and cudNN - Step by step tutorial to install NVIDIA GPU drivers and libraries in Ubuntu  
**To setup Pycharm + Anaconda + GPU in Windows, consult its respective setup file [here](Conda + CUDA Setup (Windows).txt)**.

## Ubuntu 

To install Ubuntu (desktop version), consult the following repository:  
https://github.com/DanielPalaio/Ubuntu_Setup  

## GPU drivers

**1.** In Ubuntu, search in the **Show Application** for **Software Updater** 
   
**2.** Select **Settings...**, and then the **Additional Drivers** tab

**3.** On the **NVIDIA Corporation** choose the latest **(proprietary, tested) NVIDIA metapackage**  

## CUDA and cudNN

**1.** Verify the Kernel headers and dev packages, by running in the Ubuntu Terminal:  
> sudo apt-get install linux-headers-$(uname -r)  

**2.** Install CUDA  
> **2.1** In https://developer.nvidia.com/cuda-downloads, select the target platform (Linux -> x86_64 -> Ubuntu -> 20.04 -> runfile (local)) 
>> **2.1.1** Follow the base installation instrutions, **overriding the executable**. For example:
>>> wget https://developer.download.nvidia.com/compute/cuda/11.2.1/local_installers/cuda_11.2.1_460.32.03_linux.run
>>> sudo sh cuda_11.2.1_460.32.03_linux.run --override  

>> **2.1.2** Select only to install the **CUDA toolkit**   

> **2.2** Update the user login config file. Type in the Ubuntu Terminal:  
>> nano ~/.bashrc, add:  

>> **2.2.1** Add to the file the following command lines:  
>>> export PATH=$PATH:usr/local/cuda-11.2/bin  
>>> export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/localcuda-11.2/lib64  
>>> export CUDADIR=/usr/local/cuda-11.2  

>> **2.2.2** Close the file, and source it in the Ubuntu Terminal:  
>>> source ~/.bashrc  

**3.** Install cudNN  
> **3.1** In https://developer.nvidia.com/rdp/cudnn-download#, download the **cuDNN Library** for **Linux (x86_64)**  
> **3.2** Alocate the libraries. In the Ubuntu Terminal:  
>> cd Downloads/  
>> tar -xzvf cudnn-11.2-linux-x64-v8.1.1.33.tgz  
>> sudo cp cuda/include/cudnn*.h /usr/local/cuda/include  
>> sudo cp -P cuda/lib64/libcudnn* /usr/local/cuda/lib64   
>> sudo chmod a+r /usr/local/cuda/include/cudnn*.h /usr/local/cuda/lib64/libcudnn*  

**4.** Reboot PC  

**5.** Install the required NVIDIA additional libraries. In the Ubuntu Terminal:  
> sudo apt install nvidia-cuda-toolkit  

**6.** Verify the CUDA version and GPU status. In the Ubuntu Terminal:  
> nvcc -V  
> nvidia-smi  

**7.** Test if the GPU is detected, and if CUDA is correctly installed. In a python IDE, run the following script:
> import tensorflow as tf  
> print(tf.config.list_physical_devices('GPU'))  
> print(tf.test.is_built_with_cuda())  


  
	

