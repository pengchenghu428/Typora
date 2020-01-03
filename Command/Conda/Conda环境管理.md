---
typora-root-url: images
---

# Conda 虚拟环境管理

## 1. 创建与删除环境

​	1. 创建虚拟环境 `conda create -n 环境名称 python=xx.xx`

![创建环境](/创建环境.png)

2. 删除环境 `conda remove -n env_name --all`



## 2. 激活与退出环境

1. 激活环境 

   `conda activate 环境名称`

2. 退出环境

   `conda deactivate 环境名称`



## 3. 安装与卸载软件包

1. 安装工具包

   不指定版本安装`conda install package_name`

   指定版本安装 `conda install package_name=xx.xx`

2. 卸载工具包

   `conda uninstall package_name`



## 4. 导出、导入环境

1. 导出  `conda env export > env_info_file.yml` 

2. 导入 ` conda env create -f env_info_file.yml `



## 5. 复制环境

1. 复制  `conda create --name env_name --clone exist_env_name` 











