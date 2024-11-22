# Google Workspace  
## Background  
Our Google workspace has computing environments (i.e., workstations) and a storage bucket. These have been set up by Josh Lee (joshua.lee@noaa.gov) and Ed Rodgers (ed.rodgers@noaa.gov). Our intitial workstations were "test" stations and we are in the process of building our "permanent" stations. This document provides details on how to set up the workstation and connect to the storage bucket.  
  
## Create a TEST Workstation  
1. Contact Josh Lee (joshua.lee@noaa.gov) and request a workstation.
2. He will send you a link to directions to set up a workstation.
3. We are using the Linux base 32 workstation for now. This is a very basic linux configuration, with not much installed. You will need to install software and packages.

## Launch a Workstation
1. In your web browser, go to link that was used to create the workstation.
2. The Google Cloud, Cloud Workstations page will open and your workstation will be under **My workstations**
3. Click on the **Start** icon
4. After the workstation starts, click on the cloud shell icon in the upper right, it looks like box with ">_" in it.
   1. A terminal window will open on the lower part of the browser page. This is your "cloud shell" window.
   2. You can make that a separate window by clicking on the box-with-arrow-pointing-to-NE icon in the upper right of the cloud-shell window.
6. You still need to open/launch the workstation.
7. Click on the down arrow to the right of "LAUNCH" in the **My workstations** box
   1. Select **Connect using SSH...**
   2. Copy the code by either highlighting all the code with your mouse or clicking on the two-overlayed-squares in the upper right corner.
9. Paste the code in the cloud shell.
10. If you get a prompt with user@..., then you are in your workstation!
    1. You will need to authorize each time by clicking on the "Authorize" icon when it appears.
12. If not, then most likely your home directory was not set correctly.
    1. \> pwd. IF it is "/", the your home directory did not get set correctly.
    2. \> sudo chmod -R 777 /home/user
    3. Exit the cloud shell by clicking on the "X" in the upper right corner of the cloud shell.
    4. Stop the workstation by clicking on the solid square icon to the right of the "LAUNCH" icon
    5. Restart the workstation and connect via SSH (step 7)
    6. Now when you type "pwd", you should get "/home/user".
    7. If not, contact Josh Lee.

## Install Conda
It seems you need to install conda before you can install other programs and packages.
1. **In the cloud shell** follow these instructions: [conda install](https://conda.io/projects/conda/en/latest/user-guide/install/linux.html)
2. \> sudo wget https://repo.anaconda.com/archive/Anaconda3-2024.06-1-Linux-x86_64.sh, where the https://... is from the conda website
3. \> bash Anaconda3-2024.06-1-Linux-x86_64.sh
4. \> cd anaconda3/bin
5. \> ./conda init
6. You will need to stop the cloudshell and restart it

## Install pipx
After you have conda installed, install pipx
1. The instructions are in [pipx install]( https://anaconda.org/conda-forge/pipx)
2. \> conda install conda-forge::pipx

## ipython
ipython and ipython3 come with the conda environment. ipython3 is an interactive python kernel. It is the basis for Jupyter.

## Jupyter Lab
TBD: I have not been successful at running this

## Install Google Cloud packages
You will need a series of Google Cloud packages to interact with the workstations and storage.
1. \> sudo apt-get update
2. gcloud CLI
  1. \> sudo apt-get install google-cloud-cli
  2. This can take a while
  3. I first tried using the [instructions](https://cloud.google.com/sdk/docs/install-sdk) but ran into errors. One problem was adding different repositories to the /etc/apt/sources.list.d/sources.list file (in Installation steps 1 and 2).
4. Install these as well:
  1. \> pip install --upgrade google-cloud-vision
  2. \> pip install --upgrade google-api-python-client
  3. \> pip install --upgrade google-cloud-storage
  4. \> pip install gcsfs
  5. \> pip install --upgrade google-cloud-bigquery



