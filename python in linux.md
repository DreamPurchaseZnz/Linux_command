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
source activate venv
conda install tensorflow
conda list

source deactivate 
```

