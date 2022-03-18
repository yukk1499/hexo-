---
 title: pip安装问题
---

ValueError: check_hostname requires server_hostname

问题 pip install opencv-python 的终端反馈（如下图一）

首先排除是否有开梯子，开了梯子要关掉梯子（这步很重要）

其次可以通过切换镜像源来解决（如下图二）

在终端中输入pip install opencv-python -i url（url是图二里的镜像源） 

清华：https://pypi.tuna.tsinghua.edu.cn/simple
阿里云：http://mirrors.aliyun.com/pypi/simple/
中国科技大学 https://pypi.mirrors.ustc.edu.cn/simple/
华中理工大学：http://pypi.hustunique.com/
山东理工大学：http://pypi.sdutlinux.org/
豆瓣：http://pypi.douban.com/simple/ 
