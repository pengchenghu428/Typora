---
typora-root-url: images
---

# PyCharm配置远程python解释器

## 使用场景及简介

虽然对于个人日常使用来说，Windows更加友好，但深度学习工作常需要在服务端（linux）环境中跑模型代码。对于新手来说，在学习ML/DL时，常常需要将本地写的代码传到GPU服务器中，然后在服务器上运行。这种方式需要先在本地写好代码，然后通过WinSCP这样的文件传输工具将写好的代码文件传到服务器，再通过ssh工具（如Xshell）远程连接服务器，执行相应的python脚本。这样的方式十分繁琐，效率很低。下面来介绍一下如何为本地PyCharm配置远程解释器，这样就可以直接在本地的PyCharm中利用远程服务器的python解释器运行代码啦！再也不用忍受在黑框框中调试代码的痛苦了。（手动捂脸笑）

PyCharm配置远程python解释器可以实现：

可以指定本地某目录和服务器某工作目录对应起来，可以直接在本地机子上修改服务器工作目录下面的代码文件，即可以直接在IDE（如PyCharm）中修改服务端的代码，保持两处的代码同步修改。
为PyCharm配置远程python解释器，可以在本地的IDE中运行服务端的代码，并且可以在IDE中查看运行结果，不再需要shh连接到远程服务器执行代码。
为PyCharm配置远程python解释器时，同样可以指定某一conda虚拟环境，很方便呀。

## 配置过程

### 本地及服务器环境

- 本地：Windows 7 + PyCharm 2019专业版
- 服务器：Ubuntu 16.04 + Conda + 可以使用ssh进行远程登陆



### 配置Deployment

 首先，在pycharm的菜单栏依次找到:`Tools > Deployment > Configuration.` 

![deployment](/deployment.png)

 点击左上角的加号，选择SFTP，新建一个server，例如这里我们取名为“dogVScat”。 

![dogVScat](/dogVScat.png)

 然后可以看到如下的配置页面，具体各配置在图片中有说明： 

![configuration_explaination](/configuration_explaination.png)

 然后打开Deployment的Mapping选项卡： 

![mapping](/mapping.png)

注：上面两张图画橘黄色下划线的地方，我想表达的是：我是将本地的`E:\workspace\PyCharm\Dogs_VS_Cats`目录和远程服务器的`/home/user_name/CV/img_classification/Dogs_VS_Cats`目录连接起来，要实现这两个目录下的代码同步。两个路径下的内容如下所示：
![dir](/dir.png)![dir2](/dir2.png)![dir2](/dir2.png)

这样，Deployment的配置就完成了。这个配置完成了之后，其实是相当于配置了一个ftp工具可以连接到服务器上，从而可以查看和修改服务器上的文件。你可以通过`Tools > Deplotment > Browse Remote Host`来打开相应的RemoteHost面板，这个面板显示的就是服务器上的文件，显示的范围是你在Deployment中的Connection选项卡下配置的Root path路径下的文件及文件夹。如下图右侧所示。

你可以直接在RemoteHost面板里双击某个文件并且直接进行编辑。双击某个文件后你可以看到编辑区域的顶部有一个横条，并且横条的右边有三各按钮，分别是比较，撤销和上传操作。你在这里面编辑文件之后，可以直接点击上传按钮，就会提交到服务器了。但是其实不推荐直接在这里修改代码，后面的使用流程会说到。
![remotehost](/remotehost.png)

 配置完上面的操作之后，就可以直接在PyCharm里看到服务器上的文件了，我感觉就像是直接在IDE里集成了一个FTP传输工具。 

### 配置远程python解释器

 这里主要讲的是如何配置远程python解释器。 

首先，通过`File > Settings`,打开设置选项卡。

在设置选项卡里，点击"Project:项目名"这个按钮，在展开的小项里再点击`Project Interpreter`，右边就会变成Interpreter的配置页面。

点击Interpreter配置页面的小此轮按钮，然后再选择Add或Add Remote（我这个版本的PyCharm没有）。

![add](/add.png)

 在`Add Python Interpretr`窗口选择`SHH Interpreter`，选中`Existing server configuration`，在下拉框中选择我们刚才新建的`dogVScat` server。 

![dogVScat server](/dogVScat server.png)

 点击next之后，出现如下对话框，按图示填写。 

![sync_dir](/sync_dir.png)

 写无误后，点Finish，大功告成，如下所示： 

![over](/over.png)

 经过以上步骤，你的远程解释器就配置好了。这时，你就可以直接点击小三角按钮，调用远程服务器上的python解释器来运行代码了。 



## 总结

通过上面的配置进行远程调试的话，我认为大致流程应该是下面这样：

1. 在RemoteHost面板中，选中想要修改的代码，然后右键点击Download from here将内容下载至本地(这个本地是你在配置Deployment时设置的本地文件夹)。这一步一般没啥用。

2. 在本地(这个本地是你在配置Deployment时设置的本地文件夹)修改你的代码，修改完成后在编辑区域或者文件名上右键，选择Deployment，再选择upload to…来上传到服务器。（其实经过上面的配置后，在ctrl+s保存本地代码的时候会自动同步上传代码）

3. 在提交之后，你可以像普通调用本地解释器一样的直接运行本地的这个文件(但其实运行的是服务器的文件)
   在这里，虽然RemoteHost里的文件可以直接编辑，但是并不建议这么做，因为这里编辑之后并不能直接运行。









