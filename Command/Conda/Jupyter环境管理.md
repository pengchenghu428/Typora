---
typora-root-url: images
---

# Conda 与 Jupyter 相关命令

## 1. 将Conda环境添加进Jupyter

1. 进入需要添加的环境

   `conda activate test_env`

2. 安装ipykernel 

   `conda install ipykernel`

3. 添加环境至jupyter 

   `python -m ipykernel install --user --name test_env --display-name "test_env"`

![jupyter成功安装环境](/jupyter成功安装环境.png)



## 2. 删除Jupyter环境

1. 列出所有的Jupyter环境 `jupyter kernelspec list`

   ![jupyter列出所有环境](/jupyter列出所有环境.png)

2. 删除环境 `jupyter kernelspec remove test_env`





