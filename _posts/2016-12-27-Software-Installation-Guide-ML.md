---
layout: post
title: Machine Learning Software Installation Cheatsheet
---
<p>
Tags: CUDA, Tensorflow, Theano, Keras, XGBoost, GPU
</p>
When I began Expreimenting in Machine Learning with my GPU (GTX-940MX), I had to struggle a lot figuring out installation procedures and suitable versions of Softwares. So in this blog post, I'm gonna share my experience in the form of, according to me, the best possible way of getting the tools needed to begin working in ML, preferably with GPUs, mainly through Theano, Tensorflow, Keras and XGBoost.


### Pre-Requesites:  
1. Any [CUDA capable GPU](http://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html#verify-you-have-cuda-enabled-system) with  compute capablitlity greater than or equal to 3.5
2. Anaconda or Any other Virtual Environment Manager, so that we don't screw up with system playing with installations (Recommended although not Required)


## Installation Guide:  

* ### Nvidia CUDA for Linux

    CUDA® is a parallel computing platform and programming model invented by NVIDIA. It enables dramatic increases in computing performance by harnessing the power of the graphics processing unit (GPU). To install latest CUDA (v8.0 latest as of the time of writing this) on your device, follow these steps:

    * Open Linux Dash and search for Additional Drivers. Choose latest “Open Source” driver and install it.

    * Now that Nvidia Driver is installed, Goto [Nvidia Cuda website](https://developer.nvidia.com/cuda-downloads) and download the latest Cuda toolkit “runfile” for Linux and the specific architecture (x86-64 generally for 64 bits system). Run the runfile with root priviledges, and follow along the onscreen instruction for configurations. Thus CUDA toolkit will thus be installed.

    * Open the ~/.bashrc file in and set the following filepath:  
    _Note that the default cuda path is /usr/local/cuda-v.0 until and unless customised during installation_

```shell
export CUDA_HOME=path-to-latest-cuda  
export PATH=path-to-latest-cuda/bin${PATH:+:${PATH}}  
export LD_LIBRARY_PATH=path-to-latest-cuda/lib64${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}  
export CPATH=path-to-latest-cuda/include:$CPATH  
export LIBRARY_PATH=path-to-latest-cuda/:$LIBRARY_PATH  
```

Download and Install latest CuDNN from the official page (CuDNN v5.1 latest as of writing this). If you are installing cuda from sources, follow below path, else find first the cuda installation path using "_which nvcc_".  

Extract the Archive and follow the following commands:

```shell
cd <installpath>
sudo cp cuda/include/cudnn.h /usr/local/cuda/include
sudo cp cuda/lib64/libcudnn* /usr/local/cuda/lib64
sudo chmod a+r /usr/local/cuda/include/cudnn.h /usr/local/cuda/lib64/libcudnn*
```

That’s All. latest version of CUDA will be installed now along with CuDNN!

* ### Tensorflow for Linux

  *Note: with version r0.12, TF can also be installed on windows using pip*

  * Create another environment in Anaconda to avoid any problems in existing libs. There ain't any reported problems, still its a good practice to not let theano and tensorflow interact in same environment.
  
  * After creating separate env, pip installation is very simple as mentioned [here](https://www.tensorflow.org/get_started/os_setup#pip_installation). Make sure to choose GPU enabled version through pip if you have GPU enabled device and you have setup CUDA as described above.

* ### Install OpenBLAS:

OpenBLAS OpenBLAS is an open source implementation of the BLAS (Basic Linear Algebra Subprograms) API with many hand-crafted optimizations for specific processor types. Its main competitor is MKL by intel. However it's normally seen that OpenBLAS outperforms MKL, thus we use OpenBLAS in our installation.

```bash
git clone https://github.com/xianyi/OpenBLAS
cd OpenBLAS
make FC=gfortran
sudo make PREFIX=/opt/openblas install
#This will help in getting out of way of apt-get installed things
gedit /etc/ld.so.conf.d/openblas.conf
#Type inside gedit window directory to new library, i.e: /opt/openblas/lib and exit
sudo ldconfig
```
_Note: Instead of OpenBLAS, we can also install mkl, which is very simple to install as `conda install mkl` via Anaconda._

* ### Installing Theano

	Theano is a Python library that allows you to define, optimize, and evaluate mathematical expressions involving multi-dimensional arrays efficiently. [source](http://deeplearning.net/software/theano/)  
	There are two different versions of Theano available for installation : Release candidate and Bleeding Edge version.  
	Installation of Development version is not recommended as it may contain a lot of bugs.  
	Release candidate is generally the stable version, but it tends to have problem with the latest CUDA or CuDNN. Hence it is recommended that we install Bleeding Edge version of theano along with latest softwares.

	* Installing Theano Release i.e optimized theano (v0.8 latest by the time of writing) Candidate:  
		
	
	```pip install theano```  
	(As simple as that ;) )  

	* Installing Theano Bleeding-Edge (or Dev, its procedure is similar) version  :

```bash
pip install --user git+https://github.com/Theano/Theano.git#egg=Theano
#Install libgpuarray, required for Bleeding Edge and dev Version 
git clone https://github.com/Theano/libgpuarray.git
cd libgpuarray
mkdir Build
cd Build
# you can pass -DCMAKE_INSTALL_PREFIX=/path/to/somewhere to install to an alternate location
cmake .. -DCMAKE_BUILD_TYPE=Release # or Debug if you are investigating a crash
make
make install
cd ..
# This must be done after libgpuarray is installed as per instructions above.
python setup.py build
python setup.py install
```
* ### Installing Keras:

```bash
pip install keras
gedit ~/.keras/keras.json 
#change backend to tensorflow or theano as required. Also change image_dim_flag accordingly and save 
#Also look forward to change .theanorc file as and when required (for theano cofig mainly)
```
* ### Install XGBoost :

	XGBoost is short for “Extreme Gradient Boosting”, where the term “Gradient Boosting” is proposed in the paper Greedy Function Approximation: A Gradient Boosting Machine, by Friedman.  
	Initially XGBoost was only available to run on CPU's and was comparatively intensive.  
	However with advent of its GPU version, XGBoost is now able to achieve speedup of 2X on a normal personal computer GPU and as high as 6X with high end Pascal TitanX GPU.

	* Installing CPU version:  
	
	```
	pip install xgboost
	```

	* Installing GPU version:  

```bash  
#Download CUB header and put anywhere, link: https://nvlabs.github.io/cub/
git clone --recursive https://github.com/dmlc/xgboost
cd  xgboost
mkdir build
cd build
cmake .. -DPLUGIN_UPDATER_GPU=ON -DCUB_DIRECTORY=<CUB_DIRECTORY>
cd ../python-package
python setup.py develop --user
```

