# Ubuntu安装教学-喂养式------author:ZengYs
### 1.[一系列软件安装](https://blog.csdn.net/fuchaosz/article/details/51882935)<br>
  其中包括```更新软件源```、```搜狗输入法```、```谷歌浏览器```、```git```安装等<br>
  ```cmake```、```opencv```、```qt```等安装可参考[这里](https://blog.csdn.net/yehuohan/article/details/51327465)<br><br>
### 2.C++环境配置篇
C++很好用的IDE--[Clion](https://www.jetbrains.com/clion/)<br>
别用免费的-->[Clion破解方法](https://blog.csdn.net/zxjbeyond1986/article/details/79263529)---```tip:教程是pycharm的，clion破解同理```
```
在 License sever address 处填入 https://jetlicense.nss.im/-->这是我使用的，亲测有效
```
CLion的使用可参考[这里](https://www.jianshu.com/p/cd190dbf0435)<br><br>
### 3.python环境配置篇
python很好用的IDE--[Pycharm](https://www.jetbrains.com/pycharm/)<br>
下载完后[安装教程](https://blog.csdn.net/zhuanshu666/article/details/73554885)<br>
别用免费的-->[Pycharm破解方法](https://blog.csdn.net/zxjbeyond1986/article/details/79263529)<br>
#### python运用比较多的依赖库
* numpy 
* pandas
* matplotlib
* scipy
* sklearn<br>

```
numpy的安装： pip3 install numpy

pandas的安装：  pip3 install pandas

matplotlib的安装： pip3 install matplotlib

scipy的安装：  pip3 install scipy

sklearn的安装：  pip3 install sklearn

opencv-contrib-python的安装:  pip3 install opencv-contrib-python
```

### 4.深度学习环境配置篇
* Nvidia Driver &nbsp;&nbsp;&nbsp; ```tip: use->NVIDIA-Linux-x86_64-384.111.run```
* Cuda &nbsp;&nbsp;&nbsp; ```tip: use->cuda_9.0.176_384.81_linux.run```
* Cudnn &nbsp;&nbsp;&nbsp; ```tip: use->cudnn-9.0-linux-x64-v7.tgz```<br><br>
建议: &nbsp;&nbsp;```建议别作,本人亲测N种方案得出比较稳定的驱动方案,亲测实用,其他的可能导致boom,认识我的可以直接找我拷贝```<br><br>
Nvidia Driver安装教学点击[这里](https://blog.csdn.net/fdqw_sph/article/details/78745375)&nbsp;&nbsp;  ```建议安装完驱动就跑路,看下面的Cuda、Cudnn安装```<br>
Cuda Cudnn安装教学点击[这里](https://blog.csdn.net/zhangbo_0323/article/details/78718157)&nbsp;&nbsp;  ```注意上面已完成驱动安装,直接去安装Cuda,Cudnn,大工告成的话可以安装GPU版tensorflow```<br><br>

```
tensorflow-gpu版本的的安装:  pip3 install tensorflow-gpu
终端输入python3,输入import tensorflow as tf
若没报错，环境配置成功
```
