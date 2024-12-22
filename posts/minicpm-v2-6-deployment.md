# MiniCPM-V2.6本地部署教程（附windows N卡一键部署整合包）

## 简介：

MiniCPM-V是面壁智能发布的文字-图像多模态大模型系列。它支持文本和图像输入，并提供文本输出。

**MiniCPM-V 2.6是** MiniCPM-V系列的最新、性能最佳模型。总参数量 8B，单图、多图和视频理解性能**超越了 GPT-4V**。在单图理解上，它取得了优于 **GPT-4o mini、Gemini 1.5 Pro 和 Claude 3.5 Sonnet**等商用闭源模型的表现。

更牛逼的是，由于参数量小、token密度大，MiniCPM-V 2.6 成为了**首个**支持在 iPad 等端侧设备上进行实时视频理解的多模态大模型。托模型的福，**我们可以在手机、平板、笔记本电脑上部署并体验它的强大能力。**

原项目地址：https://github.com/OpenBMB/MiniCPM-V/

**使用场景**

1. 文字OCR提取（特别是含复杂公式、图标的）
2. 看图识别物体，再也不用问别人了
3. 视频理解和总结
4. 更多用途欢迎评论区指出

## 使用效果

不会调整自行车座椅？给它拍张图就能搞定，复杂的说明书也能看懂。

![image-ojvx.png](/upload/image-ojvx.png)

也能正确识别照片中cos的角色并给出原因。

![image-uyte.png](/upload/image-uyte.png)

## 一键部署包

UP为windowsN卡用户打包好了一键部署整合包，不用关注公众号，不用三连加关注，点击网盘链接即可下载，下载解压后双击.bat文件就能使用，链接会挂在评论区

如果下载速度过慢，也可以UP的工具交流q群下载。

## 自己动手

1. 克隆仓库并跳转到相应目录

```bash
git clone https://github.com/OpenBMB/MiniCPM-V.git
cd MiniCPM-V
```

2. 安装依赖
   将requirements.txt的内容手动改为如下内容，可以在大部分windows机器安装成功，非windows机器无需修改（大概）：
   ```
   --extra-index-url https://download.pytorch.org/whl/cu118
   packaging==23.2
   addict==2.4.0
   editdistance==0.6.2
   einops==0.7.0
   fairscale==0.4.0
   jsonlines==4.0.0
   markdown2==2.4.10
   matplotlib==3.7.4
   more_itertools==10.1.0
   nltk==3.8.1
   numpy==1.24.4
   opencv_python_headless==4.5.5.64
   openpyxl==3.1.2
   Pillow==10.1.0
   sacrebleu==2.3.2
   seaborn==0.13.0
   shortuuid==1.0.11
   spacy==3.7.2
   timm==0.9.10
   torch==2.1.2+cu118
   torchvision==0.16.2
   tqdm==4.66.1
   protobuf==4.25.0
   transformers==4.40.0
   typing_extensions==4.8.0
   uvicorn==0.24.0.post1
   #xformers==0.0.22.post7
   flash_attn==1.0.4
   sentencepiece==0.1.99
   accelerate==0.30.1
   socksio==1.0.0
   gradio
   gradio_client
   http://thunlp.oss-cn-qingdao.aliyuncs.com/multi_modal/never_delete/modelscope_studio-0.4.0.9-py3-none-any.whl
   decord
   ```

然后运行指令安装依赖

```bash
pip install -r requirements.txt
```

3. 运行demo
   对于 NVIDIA GPU，请运行：

```bash
python web_demo_2.6.py --device cuda
```

对于 `Apple silicon 或AMD GPUs`
运行

```bash
python web_demo_2.6.py --device mps
```

**常见问题**

1. 识别效果不是很好？
   1. 可以更换一种编码模式。左边"Decode Type"切换到另一个选项，再点击"Regenerate"重试
   2. 可以调整输入，比如在问句后面问一句"为什么？"，会提供精确度。

**写在最后**

如果有用，欢迎点赞/投币

如果有其他需求，欢迎在评论区提出😁

博主是个喜欢编程的萌新UP，以后时不时分享一些使用工具的部署教程，或者打包一些好用的应用给朋友们，现在关注，以后就是老粉了（doge
