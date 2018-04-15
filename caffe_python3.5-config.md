# Ubuntu16.04-caffe及python接口配置
你可以参考的链接[web1](https://blog.csdn.net/g11d111/article/details/78141202)和[web2](https://blog.csdn.net/yhaolpz/article/details/71375762)
### 1.环境准备
```
# python3 modules (numpy, protobuf, skimage)
sudo pip3 install numpy
sudo apt-get install python3-skimage
sudo apt-get install python3-protobuf

# build essential
sudo apt-get install build-essential cmake git pkg-config

# gflags, glog, lmdb
sudo apt-get install libgflags-dev libgoogle-glog-dev liblmdb-dev

# boost
sudo apt-get install libboost-all-dev

# hdf5
sudo apt-get install libhdf5-dev

# protobuf
sudo apt-get install protobuf-compiler libprotobuf-dev

# blas
sudo apt-get install libblas-dev libcblas-dev libatlas-base-dev libopenblas-dev

# leveldb
sudo apt-get install libleveldb-dev

# snappy
sudo apt-get install libsnappy-dev
```
### 2.安装opencv3版本的最新版
```
git clone https://github.com/opencv/opencv
cd opencv
mkdir build
cd build
cmake ..
make
sudo make install
```
###3.下载caffe
```
cd ~/Dev # 我的开发环境目录
git clone https://github.com/BVLC/caffe
cd caffe
cp Makefile.config.example Makefile.config
```
###3.GPU版配置-主要修改Makefile.config,Makefile两处
```
Makefile.config的修改
1.注释第8行CPU_ONLY :=1(第8行） USE_CUDNN :=1
2.取消对OPENCV_VERSION :=3的注释 （第21行)
3.使用python接口。将#WITH_PYTHON_LAYER := 1修改为WITH_PYTHON_LAYER := 1
4.修改python路径 ：INCLUDE_DIRS := $(PYTHON_INCLUDE) /usr/local/include改为INCLUDE_DIRS := $(PYTHON_INCLUDE) /usr/local/include /usr/include/hdf5/serial<br>
LIBRARY_DIRS := $(PYTHON_LIB) /usr/local/lib /usr/lib 改为LIBRARY_DIRS := $(PYTHON_LIB) /usr/local/lib /usr/lib /usr/lib/x86_64-linux-gnu /usr/lib/x86_64-linux-gnu/hdf5/serial 
```
<br>

```
Makefile的修改:

1.将：NVCCFLAGS +=-ccbin=$(CXX) -Xcompiler-fPIC $(COMMON_FLAGS)
替换为：NVCCFLAGS += -D_FORCE_INLINES -ccbin=$(CXX) -Xcompiler -fPIC $(COMMON_FLAGS)
2.将：LIBRARIES += glog gflags protobuf boost_system boost_filesystem m hdf5_hl hdf5
改为：LIBRARIES += glog gflags protobuf boost_system boost_filesystem m hdf5_serial_hl hdf5_serial
```
<br>

```
修改 /usr/local/cuda/include/host_config.h 文件

将#error-- unsupported GNU version! gcc versions later than 4.9 are not supported!
改为//#error-- unsupported GNU version! gcc versions later than 4.9 are not supported!
```
###4.GPU版配置-对于一些出错的修改
**1.出现错误:**  ld cannot find lboost_python3<br>
参考[这里](https://github.com/BVLC/caffe/issues/4843)<br>

```
cd /usr/lib/x86_64-linux-gnu
sudo ln -s libboost_python-py35.so libboost_python3.so

```
**2.出现错误:** libopencv_core.so.3.3: cannot open shared object: ….<br>
参考[这里](https://github.com/GaoHongchen/DIPDemo/issues/1)<br>

```
解决方法为：在/etc/ld.so.conf里面加入一行: /usr/local/lib
Create: /etc/ld.so.conf.d/opencv.conf
wrote /usr/local/lib/ to my opencv.conf file.
sudo ldconfig -v  
```
### 5.生成Caffe
```
sudo make all -j8
sudo make test -j8
sudo make runtest -j8
```
### 6.生成caffe的python接口
```
sudo make pycaffe -j8
若报错：python/caffe/_caffe.cpp:10:31: fatal error: numpy/arrayobject.h: 没有那个文件或目录
解决办法：sudo apt-get install python-numpy
```
**此时caffe的python接口已正确编译，需把环境加入**

```
sudo echo export PYTHONPATH="~/(yourpath)/caffe/python" >> ~/.bashrc
source  ~/.bashrc
```
<br>
**检验接口**

```
python3
import caffe
若无报错，成功
```
