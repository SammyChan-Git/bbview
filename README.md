# bilibili刷播放量
b站利用github action启动firefox刷播放量。无需任何环境，所有环境firefox,python,selenium均在Github Action临时配置。**仅供学习之用，勿用于非法用途!**

## 如何使用？
把本仓库fork到自己仓库(顺便**star**一下)，然后任意修改后```git commit```触发```.github/run.yml```下的脚本即可。教程见[此处](#傻瓜教程)。**不再使用后请及时删除，避免个人信息泄露**
## 如何配置？
在```0_bilibili_playcount_up.py```中
```
videos=['https://bilibili.com/video/BV1SK411F73F','https://bilibili.com/video/BV1SK411F73F']
counter=0
while counter<2:
    r = quick_firefox.run_sync(work=work, args=(videos[counter%2]))
```
```videos```位置修改为自己的视频地址，并把 ```while counter<2```中的2改成自己希望的轮数，它决定一次action运行的时间，注意本github action启动比较耗时，可适当设置为50~100

**注意**: ```videos```数组长度和```counter<?``` 的```?```无必然联系，越界时会循环提取链接

## 速度如何？
b站同一个ip观看视频约1分钟只能涨1播放量，单个视频全天无休运行大约 500/天，但是你的github Action每月2000 min额度肯定会提前到期。本库其实也可以在自己的vps上跑，见[本仓库](https://github.com/kuro7766/Seleniums1)(环境配置较麻烦)，没有时间限制，但是跑Firefox浏览器会很费机子，低端机vps cpu基本全满甚至不够，我个人用过，经常死机，挤占其他服务。

## 如何现有基础上提速?

为了提高速度可以在```videos```数组中同时写入5~6个视频链接，在1分钟无效期刷别的视频，这样就可以减少github action时间浪费。注意单个视频全天无休单ip上限还是500。

## 傻瓜教程

### 1.fork 本仓库

![](http://kuroweb.cf/picture/1629089293307.jpg)

### 2.在自己的仓库里启动github action，点击启用

![](http://kuroweb.cf/picture/1629089996266.jpg)

### 3.Bilibili-Task就是将要执行的github workflow

![](http://kuroweb.cf/picture/1629090026945.jpg)

其中Bilibili-Task触发条件为任意提交或pr

![](http://kuroweb.cf/picture/1629090099953.jpg)

### 4.任意修改一个无关文件后提交

![](http://kuroweb.cf/picture/1629090151919.jpg)

直接提交或者命令行提交

![](http://kuroweb.cf/picture/1629090172977.jpg)

此时Action栏里会出现一个正在执行的任务

![](http://kuroweb.cf/picture/1629090395075.jpg)

**恭喜你配置完成！**

播放量不增加时，后续错误日志去这里找

![](http://kuroweb.cf/picture/1629091434982.jpg)

## 更多
Github Action历史详细日志可以[查看此处](https://github.com/kuro7766/BilibiliUp/actions)


## 旧教程

下载并解压本仓库，放到自己的github上(下载下来新建仓库或者fork，如果是fork的不要提交到本仓库，提交到自己仓库就行)。

- 1.修改任意文件并提交，可以是每天```echo `date`>tmp.txt```这种脚本，这里我新建一个test.txt文本，此时它是未提交状态

![](http://kuroweb.cf/picture/1629003179382.jpg)

- 2.git commit -m "auto push xxx" 此时已经提交到本地仓库

![](http://kuroweb.cf/picture/1629003297872.jpg)

- 3.git push -origin main 把本地仓库推送到github上去 （如果是fork的不要提交到本仓库）

![](http://kuroweb.cf/picture/1629003412692.jpg)

- 4.此时github action栏中就会出现一个正在执行的任务

![](http://kuroweb.cf/picture/1629003438876.jpg)

此任务是在github action临时分配的主机上启动浏览器刷b站播放量