# 对于pip和requirements.txt的一些实验——为什么我的requirements.txt安装会冲突？

python项目协同开发，配置环境都是一个很痛头的事情。在我的电脑上能跑，但是到了别人那就run不起来，导致大部分时间都在和环境配置斗智斗勇，非常得不偿失。

一种常见的情况是pip导出的requirements到一个同样的平台上重装却会发现conflits，网上搜索发现这个问题鲜有答案（或者是我眼力不好），于是记录下自己的实验和思考。

## 实验

环境：vscode 系列编辑器内置powershell + miniconda环境

在项目[Anionex/ItineraryAgent: Use LLMs based agents to generate itinerary | 使用基于大语言模型的智能体定制旅游行程](https://github.com/Anionex/ItineraryAgent)上进行实验

实验1：原版freeze得出依赖直装

```sh
pip freeze > requirements.txt
conda create -n tmp1 python=3.9 -y
conda activate tmp1
pip install -r requirements.txt
python planner_checker_system.py
```

![image-shkk.png](/upload/image-shkk.png)

![image-wcud.png](/upload/image-wcud.png)

实验结果：依赖冲突。
**具体��突来源：**

- 来自 `langchain-google-genai 0.0.4`，它要求的 `langchain-core` 版本是 `>=0.1` 且 `<0.2`，这与 `langchain-core==0.2.34` 冲突。因为它需要的版本范围低于 `0.2`，而req指定的 `langchain-core` 版本是 `0.2.34`。
  **我们期望pip freeze导出一个互不冲突的依赖解决方案，但是它却辜负了我们的期望**，这是为什么？

实验2：freeze去掉版本限制

```sh
pip freeze | ForEach-Object { $_ -replace '==.*', '' } > requirements.txt
conda create -n tmp2 python=3.9 -y
conda activate tmp2
pip install -r requirements.txt
python planner_checker_system.py
```

![image-hmvq.png](/upload/image-hmvq.png)

实验结果：去掉版本限制后可以装上。

实验3：使用pip-chill工具，不限制版本
这个工具只会记录你手动安装的包。

```sh
pip install pip-chill
pip-chill --no-version > requirements.txt
conda create -n tmp3 python=3.9 -y
conda activate tmp3
pip install -r requirements.txt
python planner_checker_system.py
```

![image-iynt.png](/upload/image-iynt.png)

实验结果：pass

实验4：使用pip-chill工具，限制版本

```sh
pip install pip-chill
pip-chill > requirements.txt
conda create -n tmp4 python=3.9 -y
conda activate tmp4
pip install -r requirements.txt
python planner_checker_system.py
```

![image-exxj.png](/upload/image-exxj.png)

实验结果：依赖冲突。
还是那个核心的冲突，langchain-google-genai 和 langchain-core的冲突。
