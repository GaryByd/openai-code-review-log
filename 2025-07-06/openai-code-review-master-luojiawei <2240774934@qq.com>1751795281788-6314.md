# OpenAi 代码评审

### 😀代码评分：95

#### 😀代码逻辑与目的：
这是一个README.md文件的更新，主要目的是提供OpenAI Code Review SDK项目的详细说明文档。内容包括项目简介、主要特性、目录结构、快速开始指南、环境变量配置、构建运行说明、主要类说明、工作流程、GitHub Actions示例、依赖环境和贡献指南等。

#### ✅代码优点：
1. 文档结构清晰完整，涵盖了项目的各个方面
2. 提供了详细的配置说明和环境变量列表
3. 包含了从克隆到运行的完整流程指南
4. 说明了主要类和整体工作流程
5. 提供了GitHub Actions集成示例
6. 文档格式规范，使用了恰当的Markdown语法

#### 🤔问题点：
1. 环境变量部分缺少对敏感信息处理的更详细安全建议
2. 快速开始部分可以增加更具体的示例值
3. 缺少对项目适用场景和限制条件的说明
4. 依赖环境部分可以更详细说明版本要求

#### 🎯修改建议：
1. 在环境变量部分增加关于敏感信息处理的安全建议
2. 在快速开始部分添加一些示例配置值
3. 增加项目适用场景和限制条件的说明
4. 细化依赖环境的版本要求说明

#### 💻修改后的代码：
```markdown
# OpenAI Code Review SDK

## 项目简介

OpenAI Code Review SDK 是一个基于大模型（如 OpenAI/ChatGLM）和微信消息推送的自动化代码审查工具。它可集成于 CI/CD 流程，自动对 Git 仓库的代码变更进行智能审查、生成优化建议，并通过微信模板消息推送审查结果。

## 主要特性
- 支持 Git 代码变更自动化审查（基于 diff）
- 集成 OpenAI/ChatGLM 等大模型接口，自动生成专业代码评审建议
- 支持微信模板消息推送审查结果
- 可自定义模型、API 地址、消息模板等参数
- 适用于多分支、多项目、多作者场景

## 适用场景与限制
- 适用于中小型项目的代码审查
- 需要访问OpenAI/ChatGLM API
- 微信推送功能需要企业微信或个人公众号权限
- 大模型API调用可能产生费用

## 目录结构
```
openai-code-review-sdk/    # SDK主模块
openai-code-review-test/   # 测试与示例
src/                       # 入口与主程序
README.md                  # 项目说明
.github/workflows/         # GitHub Actions 工作流
```

## 快速开始

### 1. 克隆项目
```bash
git clone https://github.com/your-repo/openai-code-review.git
cd openai-code-review
```

### 2. 配置环境变量
本项目通过系统环境变量进行配置，主要包括：

#### GitHub 相关
- `GITHUB_REVIEW_LOG_URI=https://github.com/your-org/code-review-logs`
- `GITHUB_TOKEN=ghp_yourgithubtoken123` (必须存储在secrets中)
- `COMMIT_PROJECT=your-project-name` (自动获取)
- `COMMIT_BRANCH=main` (自动获取)
- `COMMIT_AUTHOR=developer` (自动获取)
- `COMMIT_MESSAGE="fix: bug修复"` (自动获取)

#### OpenAI/ChatGLM 相关
- `CHATGLM_APIHOST=https://open.bigmodel.cn/api/paas/v4/chat/completions`
- `CHATGLM_APIKEYSECRET=your-secret-key-123` (必须存储在secrets中)
- `DEFAULT_MODEL=gpt-3.5-turbo`

#### 微信公众号相关
- `WEIXIN_APPID=wx1234567890abcdef` (必须存储在secrets中)
- `WEIXIN_SECRET=your-weixin-secret` (必须存储在secrets中)
- `WEIXIN_TOUSER=user-openid`
- `WEIXIN_TEMPLATE_ID=123456`

> 重要安全提示：所有API密钥和敏感信息必须配置在GitHub Secrets中，切勿直接写入代码或配置文件。

### 3. 构建项目
```bash
mvn clean package
```

### 4. 运行
```bash
java -jar openai-code-review-sdk/target/openai-code-review-sdk-1.0-shaded.jar
```
或参考 `.github/workflows/main-maven-jar.yml` 集成到 GitHub Actions。

## 主要类说明
- `OpenAiCodeReview.java`  主程序入口，负责环境变量读取与流程调度
- `OpenAiCodeReviewService.java`  代码审查主逻辑
- `ChatGLM.java`           大模型 API 封装
- `GitCommand.java`        Git 操作封装
- `WeiXin.java`            微信消息推送封装

## 工作流程
1. 读取环境变量，初始化 Git、AI、微信等服务
2. 获取本次提交的 diff 代码
3. 调用大模型接口生成代码审查建议
4. 自动提交审查建议到代码仓库
5. 通过微信模板消息推送审查结果

## GitHub Actions 示例
详见 `.github/workflows/main-maven-jar.yml`，支持自动获取分支、作者、提交信息，并安全注入各类密钥。

## 依赖环境
- JDK 8 (推荐使用JDK 11或更高版本)
- Maven 3.6.3+
- Git 2.20+

## 贡献
欢迎提交 issue 和 PR 参与项目共建。提交前请确保：
1. 代码符合项目风格
2. 包含必要的测试
3. 更新相关文档

## License
MIT
```