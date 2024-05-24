> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [brew.idayer.com](https://brew.idayer.com/install/stable-diffusion-webui/)

> 本文介绍的安装教程不需要魔法，能够让你快速在 mac 上安装 stable diffusion webui，并且支持 m1、m2、intel 所有芯片平台运行，让我们赶紧享受吧！

本文介绍的安装教程不需要魔法，能够让你快速在`mac`上安装`stable diffusion webui`，并且支持`m1`、`m2`、`intel`所有芯片平台运行，让我们赶紧享受吧！

注意：涉及到命令的执行请在终端执行。

[](https://brew.idayer.com/install/stable-diffusion-webui#%E5%AE%89%E8%A3%85-homebrew)安装 Homebrew
-------------------------------------------------------------------------------------------------

使用`Homebrew`一键安装命令：

```
/bin/bash -c "$(curl -fsSL https://gitee.com/ineo6/homebrew-install/raw/master/install.sh)"

```

请认准`Homebrew`快速安装教程：[https://brew.idayer.com](https://brew.idayer.com/)。

安装完成后，在终端输入`brew -v`执行，如果返回版本号信息（如下），那恭喜你，完成万里长征最重要的一步。

[](https://brew.idayer.com/install/stable-diffusion-webui#%E5%AE%89%E8%A3%85-stable-diffusion-webui-%E7%9A%84%E4%BE%9D%E8%B5%96)安装 stable diffusion webui 的依赖
-------------------------------------------------------------------------------------------------------------------------------------------------------------

在终端执行下面命令安装相关依赖。

```
brew install cmake protobuf rust python@3.10 wget

```

[](https://brew.idayer.com/install/stable-diffusion-webui#pip%E8%AE%BE%E7%BD%AE%E9%95%9C%E5%83%8F)pip 设置镜像
----------------------------------------------------------------------------------------------------------

这里一定要使用阿里云的源，清华大学的源存在问题，不能安装`GFPGAN`。

```
pip config set global.index-url https://mirrors.aliyun.com/pypi/simple/

```

如果`pip`找不到，请把`pip`替换为`pip3`再执行。

[](https://brew.idayer.com/install/stable-diffusion-webui#%E4%B8%8B%E8%BD%BD-stable-diffusion-webui-%E4%BB%A3%E7%A0%81)下载 stable diffusion webui 代码
---------------------------------------------------------------------------------------------------------------------------------------------------

```
cd ~

git clone https://gitee.com/ineo6/stable-diffusion-webui.git

```

[](https://brew.idayer.com/install/stable-diffusion-webui#%E4%B8%8B%E8%BD%BD%E6%A8%A1%E5%9E%8B)下载模型
---------------------------------------------------------------------------------------------------

代码克隆下来后，还需要下载模型，一般模型文件后缀为`.ckpt`或者`.safetensors`，而且都比较大，是以`G`为单位。我们可以参照 [Wiki](https://github.com/AUTOMATIC1111/stable-diffusion-webui/wiki/Installation-on-Apple-Silicon#downloading-stable-diffusion-models) 说明上的链接在 [Hugging Face](https://huggingface.co/) 上进行下载，这里一般下载 1.4 或者 1.5 版本的就行。

注意：请点击括号内链接下载，如果无法访问可以尝试把链接复制到迅雷中下载。

*   [Stable DIffusion 1.4](https://huggingface.co/CompVis/stable-diffusion-v-1-4-original) ([sd-v1-4.ckpt](https://huggingface.co/CompVis/stable-diffusion-v-1-4-original/resolve/main/sd-v1-4.ckpt))
*   [Stable Diffusion 1.5](https://huggingface.co/runwayml/stable-diffusion-v1-5) ([v1-5-pruned-emaonly.ckpt](https://huggingface.co/runwayml/stable-diffusion-v1-5/resolve/main/v1-5-pruned-emaonly.ckpt))
*   [Stable Diffusion 1.5 Inpainting](https://huggingface.co/runwayml/stable-diffusion-inpainting) ([sd-v1-5-inpainting.ckpt](https://huggingface.co/runwayml/stable-diffusion-inpainting/resolve/main/sd-v1-5-inpainting.ckpt))
*   [Stable Diffusion 2.0](https://huggingface.co/stabilityai/stable-diffusion-2) ([768-v-ema.ckpt](https://huggingface.co/stabilityai/stable-diffusion-2/resolve/main/768-v-ema.ckpt))
*   [Stable Diffusion 2.1](https://huggingface.co/stabilityai/stable-diffusion-2-1) ([v2-1_768-ema-pruned.ckpt](https://huggingface.co/stabilityai/stable-diffusion-2-1/resolve/main/v2-1_768-ema-pruned.ckpt))

也可以尝试使用备用百度网盘，里面只有`1.4`和`1.5`:

[https://pan.baidu.com/s/10QCfqv26jAKQags4Aa8ZEw?pwd=vw5n](https://pan.baidu.com/s/10QCfqv26jAKQags4Aa8ZEw?pwd=vw5n) 提取码: vw5n

不过如果你想要下面这些很好看的图片，就要在 [Civitai](https://civitai.com/) 下载各种模型了。

![](https://brew.idayer.com/images/16910608535268/16912211144978.jpg)

比如模型 [ChilloutMix](https://civitai.com/models/6424/chilloutmix)，抖音 AI 小姐姐大多数都是基于这个模型生成的。

点击页面上的`Download`按钮进行下载。

![](https://brew.idayer.com/images/16910608535268/16912212998388.jpg)

由于是`SafeTensor`类型的模型，所以下载的文件后缀为`.safetensors`，下载完成后，将该模型文件复制到下面的目录：

```
stable-diffusion-webui/models/Stable-diffusion

```

[](https://brew.idayer.com/install/stable-diffusion-webui#%E5%90%AF%E5%8A%A8-stable-diffusion-webui-%E6%9C%AC%E4%BD%93)启动 stable diffusion webui 本体
---------------------------------------------------------------------------------------------------------------------------------------------------

我提供的`stable-diffusion-webui`内部已经预设了加速处理，不需要使用加速工具。

执行下面命令启动：

```
cd ~/stable-diffusion-webui

./webui.sh

```

注意：每次启动都需要这样执行。

当你看到有如下内容时，大概率是成功了：

```
Running on local URL:  http://127.0.0.1:7860

```

### [](https://brew.idayer.com/install/stable-diffusion-webui#%E5%88%87%E6%8D%A2%E5%8A%A0%E9%80%9F%E6%BA%90)切换加速源

注意：`GitHub`加速使用的是第三方免费的加速服务，稳定性难以保证，所以额外配置了一些备用线路。

如果执行`./webui.sh`后卡住很久或速度很慢，可以尝试切换加速源（在`stable-diffusion-webui`目录下执行）：

```
/bin/bash -c "$(curl -fsSL https://gitee.com/ineo6/stable-diffusion-webui/raw/master/super-gh.sh)"

```

执行后会显示如下内容，输入要选择的数字即可。

```
请选择一个加速源：

1) ghproxy.com      3) ghps.cc            5)hub.gitmirror.com

2) 自营加速源         4) gh.ddlc.top        6) gh.con.sh

```

### [](https://brew.idayer.com/install/stable-diffusion-webui#%E9%92%88%E5%AF%B9intel)针对 intel

如果你的`mac`是`intel`芯片，打开`webui-user.sh`文件，把`export COMMANDLINE_ARGS`前面的`#`删掉。

```
# for intel

# export COMMANDLINE_ARGS="--skip-torch-cuda-test --upcast-sampling --no-half-vae  --use-cpu interrogate --precision full --no-half"

```

[](https://brew.idayer.com/install/stable-diffusion-webui#%E8%AE%BE%E7%BD%AE%E4%B8%AD%E6%96%87)设置中文
---------------------------------------------------------------------------------------------------

默认页面是全英文的，如果你想设置中文，可以根据如下步骤操作。

点开`Extensions`菜单，找到`Available`中的`localization`，默认是勾选上的，将勾选去掉，然后点击`Load from`按钮。

![](https://brew.idayer.com/images/16910608535268/16913325458458.jpg)

此时一直往下拉或者搜索`zh_CN`找到`zh_CN Localization`，点击右侧的`Install`按钮安装。

![](https://brew.idayer.com/images/16910608535268/16913325689866.jpg)

安装完成后点击上面的`Settings`菜单进入设置页面。

![](https://brew.idayer.com/images/16910608535268/16913325817555.jpg)

点击左侧`User interface`，往下拉，找到`Localization (requires restart)`，点击选择刚下载的`zh_CN`语言，如果看不到`zh_CN`，点击右侧的刷新图标。

![](https://brew.idayer.com/images/16910608535268/16913326115608.jpg)

选择完`zh_CN`后页面拉到最上面点击`Apply settings`按钮保存设置，最后点击`Reload Ul`按钮。

![](https://brew.idayer.com/images/16910608535268/16913326271948.jpg)

页面会重新加载，中文界面就显示出来了。

[](https://brew.idayer.com/install/stable-diffusion-webui#%E6%8F%90%E7%A4%BA)提示
-------------------------------------------------------------------------------

如果你苦于不知道`Prompt`怎么写，可以参考 [Civitai](https://civitai.com/) 上网友是怎么写的，找到你喜欢的风格后，复制图片上的提示词

![](https://brew.idayer.com/images/16910608535268/16913368869821.jpg)