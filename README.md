MANY TIMES!

This is one successful installation.

1. my env: cuda10.0 ubuntu16.04 conda 

2. steps:
  
  *  >> conda create -n enc_cu10 python=3.6.7 # create a new virtual env
  
  *  >> conda install torch==1.0.0 torchvision -c pytorch  (don't worry if the torch is built with cu90)
  
  * Install ninja::

     >> wget https://github.com/ninja-build/ninja/releases/download/v1.8.2/ninja-linux.zip

     >> sudo unzip ninja-linux.zip -d /usr/local/bin/
     
     >> sudo update-alternatives --install /usr/bin/ninja ninja /usr/local/bin/ninja 1 --force
     
   * using >> which ninja        #to locate which ninja is being installed, the author recommond ninja1.8.2
   
   #but when you install torch, the ninja 1.9.0 is installed in this env, you can remove it by >> rm ....
   
   
   * >> git clone https://github.com/zhanghang1989/PyTorch-Encoding.git
   
   * >> source activate enc_cu10
   
   * >> cd Pytorch-Encoding
   
      find the ./encoding/lib/gpu/ and change all the #include<torch/extension.h> in the .cu file to #include <torch/serialize/tensor.h>
      
   * >> python setup.py install
   
   * >> python
   
   * >> import encoding
   
   If it is ok, then you can use it. But if you get an error about operator can not be complied to operator.o, and this error is about  'PYBIND11_MODULE(TORCH_EXTENSION_NAME, m) {'
   
   I recommond you add this head file in operator.cpp : #include <pybind11/pybind11.h> #include <torch/csrc/THP_export.h> #include <torch/csrc/utils/pybind.h>
   
   Then exit python and 
   
   >> pip uninstall torch-encoding
   
   remove the build folder and torch_encoding.egg-info folder, then reinstall as
   
   >> python setup.py install
   
   Have a try for import encoding
   
   Good luck!

######################################################################################################################3




The following steps are recommonded by the author of Pytorch-encoding. I cannot install it correctly. But you can have a try!

* install steps::

* requirements::
    using the source code from Hang Zhang
    
    using cuda>9.2
    
    using pytorch>=1.0
    
  * Install Anaconda and install python 3.6.5::
     
     conda create -n encnet
     
     source activate encnet
     
     conda install python==3.6.5

  * Install ninja::

     wget https://github.com/ninja-build/ninja/releases/download/v1.8.2/ninja-linux.zip

     sudo unzip ninja-linux.zip -d /usr/local/bin/
     
     sudo update-alternatives --install /usr/bin/ninja ninja /usr/local/bin/ninja 1 --force

  * Install PyTorch::

     conda install pytorch torchvision cudatoolkit=10.0 -c pytorch

  * Install this package::

     pip install torch-encoding
     
  * test::
  
    python
    
    import encoding
    
  If import success, then you can use it. The most common issue is about the ninja. Make sure you have cuda>9.0, cuda9.2 or 10.0 may help solve the problem.

    



# PyTorch-Encoding

created by [Hang Zhang](http://hangzh.com/)

## [Documentation](http://hangzh.com/PyTorch-Encoding/)

- Please visit the [**Docs**](http://hangzh.com/PyTorch-Encoding/) for detail instructions of installation and usage. 

- Please visit the [link](http://hangzh.com/PyTorch-Encoding/experiments/segmentation.html) to examples of semantic segmentation.

## Citations

**Context Encoding for Semantic Segmentation** [[arXiv]](https://arxiv.org/pdf/1803.08904.pdf)  
 [Hang Zhang](http://hangzh.com/), [Kristin Dana](http://eceweb1.rutgers.edu/vision/dana.html), [Jianping Shi](http://shijianping.me/), [Zhongyue Zhang](http://zhongyuezhang.com/), [Xiaogang Wang](http://www.ee.cuhk.edu.hk/~xgwang/), [Ambrish Tyagi](https://scholar.google.com/citations?user=GaSWCoUAAAAJ&hl=en), [Amit Agrawal](http://www.amitkagrawal.com/)
```
@InProceedings{Zhang_2018_CVPR,
author = {Zhang, Hang and Dana, Kristin and Shi, Jianping and Zhang, Zhongyue and Wang, Xiaogang and Tyagi, Ambrish and Agrawal, Amit},
title = {Context Encoding for Semantic Segmentation},
booktitle = {The IEEE Conference on Computer Vision and Pattern Recognition (CVPR)},
month = {June},
year = {2018}
}
```

**Deep TEN: Texture Encoding Network** [[arXiv]](https://arxiv.org/pdf/1612.02844.pdf)  
  [Hang Zhang](http://hangzh.com/), [Jia Xue](http://jiaxueweb.com/), [Kristin Dana](http://eceweb1.rutgers.edu/vision/dana.html)
```
@InProceedings{Zhang_2017_CVPR,
author = {Zhang, Hang and Xue, Jia and Dana, Kristin},
title = {Deep TEN: Texture Encoding Network},
booktitle = {The IEEE Conference on Computer Vision and Pattern Recognition (CVPR)},
month = {July},
year = {2017}
}
```
