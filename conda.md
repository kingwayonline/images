### conda常用命令

* conda env list 列出目前虚拟环境
* conda activate xxx 进入某个环境
* conda deactivate 推出当前环境
* conda --version 查看conda版本
* conda create -n flowers(目标) --clone snowflakes(源) 复制一个环境
* conda create -n tfjs python=3.6.8 创建环境，指定python版本，如不指定为最新版
* conda remove -n flowers --all 删除flowers环境
* conda list 查看conda环境已经安装得包
* conda list -n python3 指定环境中已经安装的包
* pip list 查看当前环境安装的包
* pip install xxx 安装包
* conda search py     查找包，模糊查找，即模糊匹配，只要含py字符串的包名就能匹配到
* conda search --full-name python  精确查找

* pip search tensorflowjs 查找包



1. 安装conda软件，清华源
2. 通过conda安装虚拟环境

