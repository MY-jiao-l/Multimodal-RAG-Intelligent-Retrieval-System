多模态文档检索 RAG 系统

项目简介

多模态文档检索 RAG（Retrieval-Augended Generation）系统是一款基于人工智能技术的智能文档分析与问答平台。系统能够对图像、CAD图纸、PDF文档等多种格式的文件进行深度分析，提取结构化信息，并支持基于自然语言的智能问答功能。

功能特性

多格式支持：支持上传 PNG、JPG、PDF、DWG、DXF 等多种文档格式

智能图像分析：自动识别户型图、CAD图纸、建筑平面图等技术图纸

结构化信息提取：从图像中提取房间数量、面积、尺寸等结构化数据

语义检索：基于向量数据库的语义相似度检索，超越传统关键词匹配

智能问答：支持自然语言提问，系统直接返回准确答案

来源追溯：每个答案都附带来源文档列表，确保回答可追溯

技术栈

后端技术

框架：FastAPI + Python 3.11

向量数据库：ChromaDB

嵌入模型：Qwen text-embedding-v4（1024维向量）

视觉语言模型：Qwen2.5-omni-7b

异步处理：asyncio + uvicorn

前端技术

框架：React 18 + TypeScript

构建工具：Vite

UI组件：shadcn/ui + Radix UI

样式：TailwindCSS

HTTP客户端：Axios

系统架构

前端页面通过HTTP请求与FastAPI后端服务通信，后端服务调用向量数据库ChromaDB进行语义检索，VLM分析器Qwen2.5负责图像理解和结构化信息提取。

快速启动

环境要求：Python 3.11以上、Node.js 18以上、Windows/Linux/macOS操作系统

克隆项目：git clone 项目地址，然后cd multimodal_rag进入项目目录

配置后端：进入backend目录，创建Python虚拟环境，Windows系统运行python -m venv multimodal_rag创建虚拟环境，然后cd multimodal_rag\Scripts && .\activate激活虚拟环境。Linux或macOS系统运行python -m venv multimodal_rag创建虚拟环境，然后source multimodal_rag/bin/activate激活虚拟环境

安装依赖：激活虚拟环境后，运行pip install -r requirements.txt安装所有Python依赖

配置环境变量：在backend目录创建.env文件，内容为DASHSCOPE_API_KEY=你的API密钥。API密钥需要到 https://dashscope.console.aliyun.com/申请通义千问的API服务

启动后端服务：cd backend进入后端目录，然后运行python main_service.py启动服务。启动成功后会显示Uvicorn running on http://0.0.0.0:8000

启动前端服务：打开新的终端窗口，cd frontend进入前端目录，运行npm install安装前端依赖，然后运行npm run dev启动前端服务。启动成功后会显示Local: http://localhost:3000/

访问系统：打开浏览器，访问 http://localhost:3000即可使用系统

使用指南

智能问答是系统的核心功能，支持三种查询类型。

精确查询直接提取图像元数据中的答案，适用于简单问题。示例问题包括这张图中有几个卧室、总面积是多少、主卧的面积是多少等。

过滤查询根据条件筛选符合条件的文档。示例问题包括找出3个卧室的户型、面积大于100平方米的图纸等。

一般查询结合向量检索与大语言模型生成答案，处理复杂问题。示例问题包括这个户型的优缺点是什么、厨房的设计是否合理等。

文件上传时，点击上传区域或拖拽文件到上传区域，选择文件后输入问题，点击提问按钮，系统会自动上传文件并分析，然后返回答案。支持的格式包括图像PNG、JPG、JPEG，文档PDF，CAD图纸DWG、DXF。

搜索功能使用时，在搜索页面输入自然语言查询，选择检索策略包括向量检索、关键词检索、混合检索，选择使用的模型，点击搜索获取相关文档列表。

项目结构

项目根目录下包含backend和frontend两个主要目录。backend目录包含main_service.py主服务文件、image_analysis图像分析模块、knowledge-base-api知识库API、Information-Extraction信息提取模块、uploads上传文件存储目录。frontend目录包含src文件夹，其中components是React组件目录、hooks是自定义Hooks目录、services是API服务目录、types是TypeScript类型定义目录。

常见问题

启动时报错ModuleNotFoundError的原因是未激活虚拟环境或未安装依赖，解决方法是cd backend进入后端目录，然后运行.\multimodal_rag\Scripts\activate激活虚拟环境，再运行pip install -r requirements.txt安装依赖。

上传文件失败的原因可能是文件格式不支持或文件过大，解决方法是检查文件格式是否在支持列表中，确保文件大小在合理范围内建议小于10MB。

智能问答返回错误的原因可能是API Key配置错误或网络问题，解决方法是检查.env文件中的API Key是否正确，检查网络连接是否正常，查看后端日志获取详细错误信息。

答案不准确的原因可能是图像质量不高或问题表述不清晰，解决方法是上传更高质量的图像，尽量使用清晰具体的问题表述，检查图像是否包含所询问的信息。
