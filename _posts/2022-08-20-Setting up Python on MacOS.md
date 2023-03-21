---
title:  "Python on MacOS for Data Science"
layout: post
---

It’s August 2022 and I spent an unreasonable amount of time trying to set up a nice sealed Python environment on MacOS, so I decided to share the process that finally worked for me. 





I have previously set up multiple Python 2 & 3 versions via pip, homebrew, conda, etc etc… Which was pretty messy and always confusing when I was setting up an environment yet again.

So my goal here was to create an isolated enviroment where I could install any packages I want to work with, as well as the Python version of which I could easily control. This guide is based on the [1st chapter](https://wesmckinney.com/book/preliminaries.html#installation_mac) of the McKinney’s Python for Data Analysis book, as well as on [this StackOverflow post](https://stackoverflow.com/questions/58068818/how-to-use-jupyter-notebooks-in-a-conda-environment).

### Algorithm

1 - First, install [Anaconda](https://www.anaconda.com/) on your MacOS system.

2 - Next, configure conda-forge as your default package channel

```shell
(base) $ conda config --add channels conda-forge
(base) $ conda config --set channel_priority strict
```



3 - Further, create a new conda environment (named here as `my-new-environment`) with desired version of Python (we will use 3.10 version):

```shell
(base) $ conda create -y -n my-new-environment python=3.10
```



4 - Activate the environment

```shell
(base) $ conda activate my-new-environment
(my-new-environment) $
```



5 - Install any packages you want **inside** the activated environment. Also, prefer `conda` to `pip` command while installing them, it’s easier to maintain this way going forward.

```shell
(my-new-environment) $ conda install -y pandas jupyter matplotlib
```



6 - Update conda or selected packages with:

```shell
conda update conda
conda update anaconda 
conda update package_name
```



7 - Launch Jupyter Lab notebook if you already installed `jupyter` in your environment:

```shell
jupyter lab
```



Seems all nice and good except one thing: when I launched the app via `jupyter lab` and checked Python version used by its kernel with `import sys; sys.version` I have suddenly discovered the kernel was using the wrong Python version — the one completely outside of the environment! So what should we do in this situation? Well, here is the tip that finally worked for me: inside your activated environment’s terminal window, type:

```shell
(my-new-environment) $ ipython kernel install --user --name=my-conda-env-kernel
```



### Conclusion

And that’s it! This command creates a new kernel for your environment’s Jupyter notebooks, which you can then pick to be used in your notebooks and which shows the correct Python version with `import sys; sys.version`. By the way, the `!jupyter-troubleshoot` command used within a Jupyter notebook or `jupyter-troubleshoot` in the environment’s terminal would print out a lot of useful information about Python paths the environment is using, which might also help a lot. 

Please [let me know](https://docs.google.com/forms/d/e/1FAIpQLSew1RoP25e-oMoSCbqkKta9mxYJcwb2amqofNpDGtRYrxR8WA/viewform) if you have further questions with setting up Python with Conda on your MacOS system!