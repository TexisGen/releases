# AI文章助手

一个基于Python的AI文章助手应用程序，提供智能文章生成与编辑功能。

## 功能特点

- 智能文章生成
- 文章编辑与优化
- 多种AI模型支持
- 授权系统管理

## 技术栈

- Python
- Tkinter (GUI)
- 第三方AI API集成

## 安装与使用

1. 克隆仓库
   ```
   git clone https://gitee.com/monst/article.git
   ```

2. 安装依赖
   ```
   pip install -r requirements.txt
   ```

3. 运行应用
   ```
   python main.py
   ```

## 授权说明

本软件需要授权才能使用全部功能，详情请联系开发者

## 目录结构

```
article-generator/
├── README.md                 # 项目说明文档
├── requirements.txt          # 项目依赖
├── .env.example              # 环境变量示例
├── main.py                   # 程序入口点
├── src/                      # 源代码目录
│   ├── __init__.py           # 包初始化文件
│   ├── gui/                  # GUI相关代码
│   │   ├── __init__.py
│   │   ├── app.py            # 主应用类
│   │   └── components.py     # UI组件
│   ├── services/             # AI服务相关代码
│   │   ├── __init__.py
│   │   ├── base.py           # 基础服务类
│   │   ├── openai_service.py # OpenAI服务
│   │   ├── gemini_service.py # Google Gemini服务
│   │   ├── zhipu_service.py  # 智谱AI服务
│   │   └── mock_service.py   # 模拟服务
│   └── utils/                # 工具函数
│       ├── __init__.py
│       ├── file_utils.py     # 文件处理相关
│       └── thread_utils.py   # 线程相关
├── data/                     # 数据文件夹
│   ├── keywords/             # 关键词文件
│   │   └── keywords_example.txt  # 示例关键词文件
│   ├── prompts/              # 提示词模板文件
│   │   └── example_prompt.txt    # 示例提示词模板
│   ├── output/               # 默认输出文件夹
│   └── config/               # 配置文件目录
│       └── paths.json        # 路径配置持久化文件
├── logs/                     # 日志文件夹
└── docs/                     # 文档
    └── images/               # 文档图片
```

## 安装步骤

1. 克隆或下载本项目
2. 安装依赖：
   ```
   pip install -r requirements.txt
   ```
3. 配置API密钥：
    - 复制`.env.example`文件为`.env`
    - 在`.env`文件中填入您的API密钥
    - 对于所有AI服务，您都可以配置多个API密钥以轮询使用：
      ```
      # OpenAI示例
      OPENAI_API_KEY=your_api_key_here
      # 或多个密钥
      OPENAI_API_KEY_1=your_first_api_key_here
      OPENAI_API_KEY_2=your_second_api_key_here
      
      # Gemini示例
      GEMINI_API_KEY=your_api_key_here
      # 或多个密钥
      GEMINI_API_KEY_1=your_first_api_key_here
      GEMINI_API_KEY_2=your_second_api_key_here
      
      # 智谱AI示例 (格式为API_ID.API_SECRET)
      ZHIPU_API_KEY=your_api_id.your_api_secret
      # 或多个密钥
      ZHIPU_API_KEY_1=your_first_api_id.your_first_api_secret
      ZHIPU_API_KEY_2=your_second_api_id.your_second_api_secret
      ```

## 使用方法

1. 运行程序：
   ```
   python main.py
   ```

2. 在界面中：
    - 选择包含关键词的文本文件（参考`data/keywords/keywords_example.txt`格式）
    - 选择提示词模板文件（可选，参考`data/prompts/example_prompt.txt`格式）
    - 选择保存生成文章的目录（默认为`data/output`）
    - 选择AI服务（OpenAI、Gemini、智谱AI或模拟AI）
    - 设置最大线程数（建议3-10）
    - 点击"开始生成"按钮

3. 程序将开始生成文章，可以在界面上查看进度和日志
4. 生成完成后，可以在指定的输出目录找到生成的文章文件（HTML格式内容的.txt文件）

## 提示词模板

提示词模板允许您自定义AI生成文章的指令。在模板中使用 `{keyword}` 作为占位符，程序会在生成时将其替换为实际的关键词。

提示词文件中的每一行都是一个独立的提示词模板，程序在生成每篇文章时会从中随机选择一个使用，这可以让批量生成的文章风格更加多样化。

示例提示词文件内容：

```
请以'{keyword}'为主题，写一篇专业性强的文章，包含介绍、特点和应用，返回HTML格式，使用h1、h3、p等标签。
请以'{keyword}'为主题，写一篇科普文章，通俗易懂，适合大众阅读，返回HTML格式，使用h1、h3、p等标签。
请以'{keyword}'为主题，写一篇历史分析文章，探讨其发展历程和重要事件，返回HTML格式，使用h1、h3、p等标签。
```

## HTML格式说明

本程序会生成HTML格式内容的TXT文件。这意味着：

1. 文件扩展名为`.txt`，但内容包含HTML标记（如`<h1>`, `<h3>`, `<p>`, `<strong>`等）。
2. 您可以将这些文件直接用于网站内容，只需将内容复制粘贴到您的CMS或HTML编辑器中。
3. 文件名是基于AI生成的标题创建的，更易于管理和识别。

## 智谱AI集成

智谱AI是新增的中文大语言模型服务选项，具有以下特点：

1. 使用GLM-4-Flash模型，擅长中文内容生成
2. 适合生成中文文章、教程和说明文档
3. API密钥格式为`API_ID.API_SECRET`的组合
4. 支持多API密钥轮询，与其他服务一致

## 自动保存路径配置

程序会自动记住上次使用的：

- 关键词文件路径
- 提示词模板文件路径
- 输出目录路径

这些路径配置保存在`data/config/paths.json`文件中，重启程序后将自动加载上次的配置。

## 界面特点

- 简洁直观的AI服务选择下拉框
- 提示词模板选择功能
- 线程数设置输入框
- 进度实时显示
- 文件路径记忆功能

## 扩展新的AI服务

如需添加其他AI服务，可以参考以下步骤：

1. 在`src/services`目录中创建一个新的服务类文件，继承自`AIService`基类
2. 实现`generate_article`方法
3. 在`src/gui/app.py`中的`ArticleGeneratorApp.__init__`方法中将新服务添加到`self.ai_services`字典中

示例：

```python
# src/services/new_service.py
from .base import AIService

class NewAIService(AIService):
    def __init__(self):
        super().__init__("新AI服务名称")
        # 初始化API密钥等
        
    def generate_article(self, keyword, prompt_template=None):
        # 实现文章生成逻辑
        pass
```

然后在`src/gui/app.py`中添加：

```python
from ..services.new_service import NewAIService

# 在__init__方法中：
self.ai_services = {
    # 已有服务...
    "新AI服务名称": NewAIService()
}
```

## 注意事项

- 使用OpenAI/Gemini/智谱AI服务需要有效的API密钥和足够的额度
- 使用API服务生成文章可能产生费用，请注意控制生成数量
- 多KEY轮询功能在多线程环境下是安全的，使用了线程锁确保在并发请求时API密钥正确轮询
- 当使用较多线程时，建议配置多个API密钥以避免请求速率限制
- 如遇到网络问题，请检查网络连接或代理设置

## 更新日志

### 版本 1.0.0 (2025-04-07)

#### 核心功能
- 支持多种AI服务：OpenAI、Google Gemini、智谱AI和模拟AI服务
- 集成智谱AI服务，支持GLM-4-Flash模型生成中文内容
- 实现文章智能生成系统，支持批量处理关键词
- 所有AI服务统一输出HTML格式，获得结构化的文章内容

#### 高级功能
- 提示词模板系统，支持自定义生成指令和随机选择
- 自动文件命名，从文章标题智能提取文件名
- 文件路径自动保存功能，记住上次选择的位置
- 实现任务状态持久化和自动恢复功能

#### 性能优化
- 高并发处理引擎，支持500+线程并行生成
- 高级API密钥管理系统，支持多KEY轮询和健康监测
- 所有API请求支持智能节流和自动重试机制
- 实现线程安全的密钥轮询，确保在高并发环境下密钥使用均衡

#### 用户体验
- 重构UI更新逻辑，实现完全异步的界面更新，消除卡顿
- 添加日志缓冲和UI更新节流，保证高负载下响应流畅
- 优化界面布局和输入控件，提高用户友好度
- 改进错误处理机制，提供更明确的反馈

#### 系统架构
- 任务优先级队列和动态调度机制
- 任务监控系统，自动处理超时任务
- 日志系统优化，实现批量处理和消息压缩
- 模块化设计，便于扩展新的AI服务 