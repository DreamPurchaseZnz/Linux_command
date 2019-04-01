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


## install tensorflow
```
conda config --set proxy_servers.http http://xxxx:huawei@10.61.34.138:3128
conda config --set proxy_servers.https http://xxxx:huawei@10.61.34.138:3128
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

## install tensorflow with gpu

### find out the GPU exists in your computer
```
cat /proc/cpuinfo
```
```
lspci | grep -i --color 'vga\|3d\|2d'
lshw -C display
nvidia-smi
```
### Installation

Different Versions of Tensorflow support different cuDNN and CUDA Verisons 
(In this table CUDA has an integer value but when you go to download it is actually a float which makes numbering and compatibility more difficult). 
Also cuDNN and conda were not a part of conda.

SO USE CONDA
```
conda create --name tf_gpu tensorflow-gpu 
```












