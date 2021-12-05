# colab

### 1.首先需要一个谷歌账号

* 注册的时候可能会遇到号码无法进行验证的情况
![](https://note.youdao.com/yws/api/personal/file/WEBa0668ffc1ca2c15b97f9f9ca83bb29d1?method=download&shareKey=8059a359abd1456eb147a7ce3ca3da7e)
* 因为Google现在不怎么支持中文，所以我们需要把谷歌的英文上移，同时使用英文并且删除中文，只保留英文语言。

### 2.查看基本配置
* 查看pytorch的版本、cuda是否可用
* 查看需要的工具版本
```
import torch
print(torch.__version__)
```
```
print(torch.cuda.is_available)
```

### 3.挂载
##### 因为colab只是一个远程的、可以无偿给我们提供GPU支持的主机，而不是本地的存储支持。所以我们需要把我们要运行的代码（谷歌云盘）挂载到远程主机上。
* 挂载远程主机
```
from google.colab import drive
drive.mount("/content/drive)
```
* 这一步我们需要登录谷歌账号复制链接
![](https://note.youdao.com/yws/api/personal/file/WEB298e801d0a3acba2667fe7ba8c3e6b8c?method=download&shareKey=49b1dbf0ab5675af3b63016127b1f7db)
* 更改运行目录
* 因为程序的运行需要在相同的目录下才能相互使用和运行，所以需要把要运行的程序放到同一个目录下。在这一步最好都运行一次，有时候看着是在一个目录下，但事实上在不同的地方。
![](https://note.youdao.com/yws/api/personal/file/WEB4769a1f4d67bdd6fa62e8c71a896ccab?method=download&shareKey=adfef04bbd9d574cc7ac43aadc1674c7)
### 4.同级文件调用
##### 当我们在运行一个程序时，有时候需要调用模型模块儿来进行训练，我们只在谷歌云盘上更改后缀，单纯地把.ipynb文件更改成.py文件，从表面上看确实已经成为python文件了。但是事实上colab只能更改.ipynb文件的内容，所以更改后的文件仍然是.ipynb文件。
##### 要想把.ipynb文件真正变成.py文件，可以先把文件下载到本地，在本地上更改后缀，然后在挂到谷歌云盘当中，这样就可以调用了。
### 5.将kaggle的数据集下载到colab上使用
##### kaggle上有很多竞赛数据集，但是kaggle的GPU使用时间是有限的，但是colab没有时间限制。如果从本地上传就很慢，所以我们可以把kaggle上的数据集传到（下载）到colab上去使用。
* 首先需要一个kaggle账号
* 下载并更新kaggle 
```
!pip install kaggle
```
```
!pip install --upgrade --force-reinstall --no-deps kaggle
```
* 进入kaggle，进入你的账号信息
* 往下拖，在API的位置有个Create New API Token，点击后会自动下载一个json文件，打开会出现username和key信息。
![](https://img-blog.csdnimg.cn/20200419131732836.png)
![](https://note.youdao.com/yws/api/personal/file/WEBfb25bde78e6f9c3aef09e8e2a7d0fc9c?method=download&shareKey=e9d444d9a3d9d5829e7aa62b41b2a767)
* 输入以下代码
```
import json
token = {"username":"xxxxx","key":"xxxxx"}
with open('/content/kaggle.json', 'w') as file:
  json.dump(token, file)
```
*然后再依次输入一下代码
```
!mkdir -p ~/.kaggle
```
```
!cp /content/kaggle.json ~/.kaggle/
```
```
!chmod 600 ~/.kaggle/kaggle.json
```
```
!kaggle config set -n path -v /content
```
* 最后从kaggle上找出自己的数据集,点击Copy API command后进入colab下载即可。
![](https://note.youdao.com/yws/api/personal/file/WEBf34a4d51c6fa1e40b34b6ae821752509?method=download&shareKey=8100dc1c387dc1500f436a85f7c9a479)
* 我这里找了个比较小的数据集，下载速度还可以。我还测试过一个大的数据集，下载速度差不多可以达到90MB/s
![](https://note.youdao.com/yws/api/personal/file/WEBb6313496d36d2da249e897fc00588881?method=download&shareKey=7c07a70f4b8cb8d1c6a30bee58324f97)
### 模型测试【resnet101】+【CIFAR10】
* 使用GPU
![](https://note.youdao.com/yws/api/personal/file/WEB513ff4229077d747bf3e605c1fdd00b4?method=download&shareKey=41de0a54704bde7e2a37a9000ce1a3ea)
![](https://note.youdao.com/yws/api/personal/file/WEBec1bab9cceb85c16ce76ae81931b2465?method=download&shareKey=6eec973d892c8cece45aab04a4f77fe7)
```
import os
os.environ['CUDA_VISIBLE_DEVICES'] = '0'
```
* 模型测试
![](https://note.youdao.com/yws/api/personal/file/WEB60e4930efc965989d27d6dfa8ff18e67?method=download&shareKey=445ee61c848f3768e95af7744229c230)
![](https://note.youdao.com/yws/api/personal/file/WEBbb8925e46e1f00dd8a38c4c164545f29?method=download&shareKey=519bf7b1faef901fde7ba2d78ab7d4a1)
![](https://note.youdao.com/yws/api/personal/file/WEB2403f1cc4b962d761189f3f225a6686c?method=download&shareKey=0d6aa4fd22927bd36b165f086d3af7f5)
![](https://note.youdao.com/yws/api/personal/file/WEB1c5a74ca03d7eb939a18719674aa31e3?method=download&shareKey=c779c67e4ef52a1e9eae10065bcd1cc1)