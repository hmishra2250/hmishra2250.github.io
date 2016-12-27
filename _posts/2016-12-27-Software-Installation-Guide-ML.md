---
layout: post
title: Machine Learning Software Installation CheatSheet
---
<p>
Tags: CUDA, Tensorflow, Theano, Keras, XGBoost, GPU
</p>
<p>
When I began Expreimenting in Machine Learning with my GPU (GTX-940MX), I had to struggle a lot figuring out installation procedures and suitable versions of Softwares. So in this blog post, I'm gonna share my experience in the form of, according to me, the best possible way of getting the tools needed to begin working with GPUs, mainly through Theano, Tensorflow, Keras and XGBoost.
</p>
###Pre-Requesites:  
<ol>
	<li>A [CUDA capable GPU](http://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html#verify-you-have-cuda-enabled-system) with  compute capablitlity greater than or equal to 3.5 </li>
	<li>Anaconda or Any other Virtual Environment Manager, so that we don't screw up with system playing with installations (Recommended although not Required) </li>
</ol>
</p>
<p>

</p>
This Blog was created using [Jekyll Now repository](https://github.com/barryclark/jekyll-now) on Github, as starting point. It is a very good point to get started with personal blogs. Using only static pages in the blog makes it comparatively faster than other Micro Blogging sites which uses Databases. <br>
The best way to get started with a personal blog is to fork the [above](https://github.com/barryclark/jekyll-now) repository or one of the custom themes as mentioned [Here](https://github.com/barryclark/jekyll-now#other-forkable-themes). Next one can update their site name, avatar and other options using the _config.yml file in the root of the repository (shown below).

![_config.yml]({{ site.baseurl }}/images/config.png)

The easiest way to make your first post is to go into /_posts/ and update the Hello World markdown file. For more instructions head over to the [Jekyll Now repository](https://github.com/barryclark/jekyll-now) on GitHub.
