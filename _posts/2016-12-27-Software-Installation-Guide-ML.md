---
layout: post
title: Machine Learning Software Installation CheatSheet
---

Tags: CUDA, Tensorflow, Theano, Keras, XGBoost, GPU


When I began Expreimenting in Machine Learning with my GPU (GTX-940MX), I had to struggle a lot figuring out installation procedures and suitable versions of Softwares. So in this blog post, I'm gonna share my experience in the form of, according to me, the best possible way of getting the tools needed to begin working with GPUs, mainly through Theano, Tensorflow, Keras and XGBoost.


### Pre-Requesites:  
1. A [CUDA capable GPU](http://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html#verify-you-have-cuda-enabled-system) with  compute capablitlity greater than or equal to 3.5
2. Anaconda or Any other Virtual Environment Manager, so that we don't screw up with system playing with installations (Recommended although not Required)


## Installation Guide:  

1. ### Nvidia CUDA for Linux
  CUDA® is a parallel computing platform and programming model invented by NVIDIA. It enables dramatic increases in computing performance by harnessing the power of the graphics processing unit (GPU). To install latest CUDA (v8.0 latest as of the time of writing this) on your device, follow these steps:
  * Open Linux Dash and search for Additional Drivers. Choose latest “Open Source” driver and install it.
  * Now that Nvidia Driver is installed, Goto [Nvidia Cuda website](https://developer.nvidia.com/cuda-downloads) and download the latest Cuda toolkit “runfile” for Linux and the specific architecture (x86-64 generally for 64 bits system). Run the runfile with root priviledges, and follow along the onscreen instruction for configurations. Thus CUDA toolkit will thus be installed.
  * Open the ~/.bashrc file in and set the following filepath:  
    ``` shell
    export CUDA_HOME=path-to-latest-cuda  
	export PATH=path-to-latest-cuda/bin${PATH:+:${PATH}}  
    export LD_LIBRARY_PATH=path-to-latest-cuda/lib64${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}  
	export CPATH=path-to-latest-cuda/include:$CPATH  
	export LIBRARY_PATH=path-to-latest-cuda/:$LIBRARY_PATH  
	```  
	*Note that the default cuda path is /usr/local/cuda-v.0 until and unless customised during installation*  
  * Download and Install latest CuDNN from the official page (CuDNN v5.1 latest as of writing this). If you are installing cuda from sources, follow below path, else find first the cuda installation path using "*which nvcc*".
    Extract the Archive and follow the following commands:
	``` shell
	cd <installpath>
	sudo cp cuda/include/cudnn.h /usr/local/cuda/include
	sudo cp cuda/lib64/libcudnn* /usr/local/cuda/lib64
	sudo chmod a+r /usr/local/cuda/include/cudnn.h /usr/local/cuda/lib64/libcudnn*
	```
  * That’s All. latest version of CUDA will be installed now along with CuDNN!

2. ### Tensorflow for Linux (Edit: with version r0.12, TF can also be installed on windows using pip)
  * Create another environment in Anaconda to avoid any problems in existing libs. There ain't any reported problems, still its a good practice to not let theano and tensorflow interact in same environment.
  * After creating separate env, pip installation is very simple as mentioned [here](https://www.tensorflow.org/get_started/os_setup#pip_installation). Make sure to choose GPU enabled version through pip if you have GPU enabled device and you have setup CUDA as described above.

This Blog was created using [Jekyll Now repository](https://github.com/barryclark/jekyll-now) on Github, as starting point. It is a very good point to get started with personal blogs. Using only static pages in the blog makes it comparatively faster than other Micro Blogging sites which uses Databases. 
The best way to get started with a personal blog is to fork the [above](https://github.com/barryclark/jekyll-now) repository or one of the custom themes as mentioned [Here](https://github.com/barryclark/jekyll-now#other-forkable-themes). Next one can update their site name, avatar and other options using the _config.yml file in the root of the repository (shown below).

![_config.yml]({{ site.baseurl }}/images/config.png)

The easiest way to make your first post is to go into /_posts/ and update the Hello World markdown file. For more instructions head over to the [Jekyll Now repository](https://github.com/barryclark/jekyll-now) on GitHub.
