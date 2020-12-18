# Setting-Up-MSI-Laptop-With-Ubuntu-NVIDIA-CUDA-TENSORFLOW_GPU

## System Specification : NVIDIA GRAPHICS 1650 MAXQ , Laptop : MSI GF-63 THIN SCXR

### Tips for those who have already tried to setup But Failed (NOT MSI specific ,generally this happens)
    1) You should remove every existing files created By NVIDIA Driver.
        sudo apt-get purge nvidia*
        sudo apt-get autoremove
        sudo apt-get autoclean
        sudo rm -rf /usr/local/cuda*
        reboot
    2) In case you can afford to reinstall the ubuntu then please do this. The reason is that there are some files that still
        hang on and may create problems.
    3) If you are facing with black screen problem just after the "nvidia driver setup" reboot then you have two options
        i) On the GRUB menu , select the ubuntu and Don't Press Enter, Press e
            you will see a line where 'quiet splash' is written , add 'nouveau.modeset=0' or 'modprobe.blacklist=nouveau' just after
            'quiet splash'. Press ctrl-x or F10 To save the settings.
            a) To check if the nvidia-driver is successfully installed or not , open the terminal and write 'nvidia-smi'. It
               will show you a table if the driver is installed correctly. Check System configuration , whether the default 
               graphic card is Nvidia or not.
            
        ii) if the above fails, remove the nvidia driver by going into the terminal(press ctrl+alt+F2) and then follow the tip 1.
        iii) There is always a new way.
     4) If you cannot still reach the login option, try to login through recovery mode and back up the data. You can find articles on it.
        

## The whole set up is divided in 4 steps
### Step 1 --> Bootable Pendrive , Step 2 --> Installing , Step 3 --> Setting Up Nvidia drivers , Step 4 --> Anaconda Set up
#### Bootable Pendrive
    1) Download the ubuntu 18.04 (LTS).
    2) Use rufus software or any other software to make the pendrive bootable.

#### Installing
    1) If you want dual boot then install Windows first and then ubuntu.
    2) Make the partition drive for ubuntu.
    3) make sure that fast boot is disable.(If Windows is there)
      go to Control Panel -> All Control Panel Items -> Power Options -> System Settings, and under title "Shutdown settings", 
      uncheck "Turn on fast startup (recommended)".
    3) Security boot disable (change this in BIOS, for MSI Laptops, reboot the system and press 'delete' a couple of times before the OS is loaded).
    4) reboot the system
    5) attach the pendrive
    6) Press f11(for msi laptop) repeatedly to go into boot menu. It may not be required if the fast-boot is disable.
    7) choose install ubuntu and do the installation.
    
#### Setting Up Nvidia drivers
    1) First of all You must know what drivers support your graphic card, for example GTX 1650 MAX-Q is supported by nvidia-driver-430 onwards.
    2) open the terminal in ubuntu and do the following :- (i will be installing nvidia-driver-440-server because it has cuda version 10.2)
       sudo add-apt-repository ppa:graphics-drivers/ppa
       sudo apt update
       sudo ubuntu-drivers list
       ---this will show you a list of softwares---
       sudo apt install nvidia-driver-440-server
       sudo reboot
    3) after rebooting check the installation by pressing ctrl+alt+T and write 'nvidia-smi' & also check the system configuration.
 
 #### Anaconda Set up and Tensorflow-gpu
    1) Install the anaconda
    2) Use the 'conda' command to install the tensorflow-gpu in the 'base' environment. Cuda version installed by anaconda is 10.1 and
        tensorflow version is 2.2. The version might change in future.
    3) Now You can check whether the anaconda is using the GPU or not
        https://www.tensorflow.org/api_docs/python/tf/test/is_gpu_available
        https://intellipaat.com/community/33459/how-to-tell-if-tensorflow-is-using-gpu-acceleration-from-inside-python-shell
        
  ### Personal tips
      In my case the 440 driver worked with the above configurations and was detecting and using the GPU in anaconda. I would have prefered nvidia-430 
      but this is no longer present. Try to download the lower driver version (w.r.t your graphic card support) because of the forward compatibility of
      the drivers with cuda version. And Try not to update the softwares that pops up frequently as one of my friend messed up due to this. Though you
      can use sudo apt-get update command.
        
 ### One can use the below link to check the compatibilty of different cuda version with nvidia drivers
  https://docs.nvidia.com/deploy/cuda-compatibility/index.html
  
 #### One can also take the help from here
 https://gist.github.com/mari-linhares/cef4cb3440408e44963d1447a7db5ae0
 
 
