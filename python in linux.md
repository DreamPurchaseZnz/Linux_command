# Python in linux

check the version of python
```
python --version
python3 --version
```

check the installed packages
```
pydoc modules
```
```
pip list
```
```
python:
import sys
sys.modules.keys()
```

## install anaconda

1. download the anaconda.sh

2. bash anaconda.sh

3. install completely

4. install anthor lib
```
matplotlib, scipy, numpy， sklearn, pandas, scikit-learn
```






## install tensorflow
```
conda config --set proxy_servers.http http://xxxx:huawei@10.61.34.138:3128
conda config --set proxy_servers.https http://xxxx:huawei@10.61.34.138:3128
```
When you face the problem-"condahttperror http 000 connection failed for url", Try running following command: 
```
conda config --set ssl_verify no
```


```
conda create -n venv pip python=3.6
source activate venv or conda activate venv

conda install tensorflow
conda list

source deactivate   or conda deactivate venv
```
To see all the environments
```
conda info --envs
```
To reset a conda environment
```
conda list --revisions and conda install --rev REV_NUM.
```

## Remove the env in conda
```
conda env remove -n ENV_NAME
```
conda env remove -n ENV_NAME
to remove the environment with that name. (--name is equivalent to -n)

## install pycharm
download pycharm community version
```
tar -xf pycharm-professional-2018.2.tar.gz         # without installation
```
```
cd pycharm-2018.2/bin
./pycharm.sh
```
## theano
```
theano 1.4 is compatible with numpy 1.6
```


## find out the GPU exists in your computer
```
cat /proc/cpuinfo
```
```
lspci | grep -i --color 'vga\|3d\|2d'
lshw -C display
nvidia-smi
hwinfo --gfxcard --short
nvidia-smi -l 3
```
## Install tensorflow with gpu
### Installation of tensorlfow

Different Versions of Tensorflow support different cuDNN and CUDA Verisons 
(In this table CUDA has an integer value but when you go to download it is actually a float which makes numbering and compatibility more difficult). 
Also cuDNN and conda were not a part of conda.

SO USE CONDA, the [package lib](https://repo.anaconda.com/pkgs/main/linux-64/)
```
conda create --name tf_gpu tensorflow-gpu 
conda create --name tf_gpu tensorflow-gpu==1.4.1              # the version needs to be found in the library
```
```
tensorflow_gpu-1.11.0	3.5-3.6	MSVC 2015 update 3	Bazel 0.15.0	7	9
tensorflow_gpu-1.10.0	3.5-3.6	MSVC 2015 update 3	Cmake v3.6.3	7	9
tensorflow_gpu-1.9.0	3.5-3.6	MSVC 2015 update 3	Cmake v3.6.3	7	9
tensorflow_gpu-1.8.0	3.5-3.6	MSVC 2015 update 3	Cmake v3.6.3	7	9
tensorflow_gpu-1.7.0	3.5-3.6	MSVC 2015 update 3	Cmake v3.6.3	7	9
tensorflow_gpu-1.6.0	3.5-3.6	MSVC 2015 update 3	Cmake v3.6.3	7	9
tensorflow_gpu-1.5.0	3.5-3.6	MSVC 2015 update 3	Cmake v3.6.3	7	9
tensorflow_gpu-1.4.0	3.5-3.6	MSVC 2015 update 3	Cmake v3.6.3	6	8
tensorflow_gpu-1.3.0	3.5-3.6	MSVC 2015 update 3	Cmake v3.6.3	6	8
tensorflow_gpu-1.2.0	3.5-3.6	MSVC 2015 update 3	Cmake v3.6.3	5.1	8
tensorflow_gpu-1.1.0	3.5	MSVC 2015 update 3	Cmake v3.6.3	5.1	8
tensorflow_gpu-1.0.0	3.5	MSVC 2015 update 3	Cmake v3.6.3	5.1	8
```

NOTE: solve the status: CUDA diriver version is insufficient for CUDA runtime version

First check the driver version
```
cat /proc/driver/nvidia/version
```
Then according the compatible version, download the driver and install.
```
./NVIDA.run             # cuda 9.2     ->  driver 396.26
```
```
CUDA Toolkit	Linux x86_64 Driver Version
CUDA 10.1 (10.1.105)	>= 418.39
CUDA 10.0 (10.0.130)	>= 410.48
CUDA 9.2 (9.2.88)	>= 396.26
CUDA 9.1 (9.1.85)	>= 390.46
CUDA 9.0 (9.0.76)	>= 384.81
CUDA 8.0 (8.0.61 GA2)	>= 375.26
CUDA 8.0 (8.0.44)	>= 367.48
CUDA 7.5 (7.5.16)	>= 352.31
CUDA 7.0 (7.0.28)	>= 346.46
```

### Tensorflow Testing
```
import tensorflow as tf
sess = tf.Session(config=tf.ConfigProto(log_device_placement=True))
```

### install sonnet
There may be some mistakes when the pip meets the conda install command

Use conda to install offline package and then run this command with the path to the tar file:
```
conda install --offline C:\pymc-2.3.5-np110py35_0.tar.bz2
```

Testing
```
$ cd ~/
$ python
>>> import tensorflow as tf
>>> import sonnet as snt
>>> input_ = tf.zeros((3, 5))
>>> output = snt.Linear(10)(input_)
```



