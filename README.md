# News_QA

News_QA (新闻问答小助手) 是由 ykuang 开发的会话语言模型, 旨在帮助人们查找相关新闻信息。
News_QA (新闻问答小助手) 可以理解用户选择的语言，如中文和英文，并能流畅地与用户交流。

## 数据集

数据集保存在data目录下, 
默认包含此仓库 `https://gitee.com/Amos698/TuFaShiJianGongKaiShuJuJi/tree/master` 中的1000条新闻信息,
如果需要增加新闻数据, 只需要在data目录下添加csv文件即可, 注意要使用UTF-8编码, 用GBK不知道会不会乱码。

## 代码结构

```
├─News_QA
│  ├─README.md                    # 本项目说明文档
│  ├─requirements.txt             # 安装运行所需要的 Python 库依赖（pip 安装）
│  ├─app.py                       # 应用的默认启动脚本, 会自动调用`download_model.py`、`create_db.py`和`LLM.py`
│  ├─create_db.py                 # 读取数据集数据生成向量数据库
│  ├─download_model.py            # 下载sentence-transformer和internlm-chat-7b
│  ├─LLM.py                       # langchain自定义模型
│  ├─data                         # 数据集
│  │  ├─news_1000_utf8.csv        # 默认数据文件
│  └─... 
```

## 应用部署

在本机部署的操作步骤:

```
mkdir /home/xlab-app-center
cd /home/xlab-app-center

conda create --name news_qa python=3.10 -y
conda activate news_qa

# 下载news_qa
git clone https://github.com/ykuang/News_QA.git news_qa
cd news_qa

# 安装依赖
pip install -r requirements.txt -i https://pypi.tuna.tsinghua.edu.cn/simple

# 运行
python app.py
# app.py中会自动下载模型和创建数据库
# python download_model.py
# python create_db.py

```

在openXlab上部署和运行, 可以参考官方文档(默认算力不够, 需要申请):

https://openxlab.org.cn/docs/apps/Gradio%E5%BA%94%E7%94%A8.html

1. 应用会强制在 `7860` 端口启动，请您不要占用或改写个人 `gradio` 应用的启动端口
2. 应用平台应用代码默认存储的位置为 `/home/xlab-app-center`

## 问题

### 运行`python app.py`报`Killed`

查看系统日志`egrep -i 'killed process' /var/log/syslog`, 如果有 Out of memory 字样, 就是内存不足了。

