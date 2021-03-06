# AlexNet_TF2.2 Implementation with tensorflow_datasets

An implementation of AlexNet (Krizhevsky et al.(2010)) written in TensorFlow 2.0 and splite the original code
into both the client the AlexNet model in the OOP style.

This code preloads the Oxford_Flowers102 dataset from TensorFlows datasets API. To change which dataset to use
change data_set variable to one from here: https://www.tensorflow.org/datasets/catalog/overview

Author: Henry Powell

Institution: Institute of Neuroscience, Glasgow University, Scotland.
Implementation of AlexNet using Keras with Tensorflow backend. Code will preload the Oxford_Flowers102 dataset.
Learning tracks the model's accuracy, loss, and top 5 error rate. For true comparision of performance to the 
original model (Krizhevsky et al. 2010) this implementation will need to be trained on Imagenet2010.

Editor: Mike Chen

It is a good practice for the author to adopt the tensorflow_datasets library. Mike splits the client application 
from the AlexNet model for better readibility, accessibiliuty and usability.In addition, Mike corrects the logical 
and runtime errors of the original scripts. In addition, the script is changed to comply with TendorFlow 2.2 and 
Keras 2.4.3. Please notice that TensorFlow 2.1 has a bug with CUPTI in the dev. environment of CUDA 11.0 and cuDNN 
8.0.1, so the editor has to migrate from the old versions to TensorFlow 2.2 and Keras 2.4.3.

Set up the GPU in the condition of allocation exceeds system memory with the reminding message: Could not create 
cuDNN handle... The following lines of code can avoid the sudden stop of the runtime. 

It is necessary that RAM is larger than or equal to 16G. If RAM is 16G, users need to set Virtual Memory to 16G 
with vm.swappiness=60 to avoid the error: could not create cudnn handle:CUDNN STATUS_INTERNAL ERROR. 

Swap reference: 
https://www.digitalocean.com/community/tutorials/how-to-add-swap-space-on-ubuntu-18-04

To enable the runtime, users need to install the following libraries. 


# tensorflow_datasets

Normally speaking, we only need to install tensorflow_datasets

$ pip install tensorflow_datasets

or 

$ pip3 install tensorflow_datasets

While running the script of main.py, it builds a directory "/home/user/tensorflow_datasets". It has two sub-directories 
including downloads, oxford_flowers102. I assume that developers uses Ubuntu 18.04. 


# Install tfds-nightly

If it raises NonMatchingChecksumError(resource.url, tmp_path) duruing the runtime, please make the following changes to 
adapt to Oxford which owns the 102flowers data. 

## Remove the downloaded files

rm -rf ~/tensorflow_datasets/oxford_flowers102/

rm -rf ~/tensorflow_datasets/downloads

## Install tfds-nightly

$ pip --no-cache-dir install tfds-nightly

or 

$ pip3 --no-cache-dir install tfds-nightly

And then, we enter into the following sector. 


# Install google-cloud-storage and google-auth

Install the compatible google-cloud-storage and google-auth versions

## Install google-cloud-storage v1.29.0

$ pip install google-cloud-storage

## Install google -auth v1.18.0 

Need to install the newer version due to the conflict of internal components of google-cloud-storage v1.29.0

$ pip install google-auth==1.18.0

It will remind users of uninstall the old google-auth version during installing the update google-auth. That is what we want.


# How to execute the client

Please execute the client with the command with the CUPTI parameter as follows. 

$ python client.py --cap-add=CAP_SYS_ADMIN

or 

$ python client_simple.py --cap-add=CAP_SYS_ADMIN



