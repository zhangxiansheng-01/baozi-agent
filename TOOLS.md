# TOOLS.md - 工具配置与笔记

> 工具特定配置、注意事项和凭证。参考pdf技能的Quick Reference表格格式。

---

## 快速命令参考表

| 任务 | 工具 | 命令/操作 |
|------|------|-----------|
| 搜索记忆 | memory_search | memory_search("query") |
| 网络搜索 | web_search | web_search(query="关键词") |
| 读取网页 | web_fetch | web_fetch(url="网址") |
| 浏览器自动化 | browser | browser(action="open", url="...") |
| 发送消息 | message | message(action="send", message="...") |
| 读写文件 | read/write | read(path="..."), write(content="...") |
| 执行命令 | exec | exec(command="...") |
| 创建子代理 | sessions_spawn | sessions_spawn(task="...") |
| 飞书文档 | feishu_doc | feishu_doc(action="read", doc_token="...") |
| 飞书Wiki | feishu_wiki | feishu_wiki(action="get", token="...") |

---

## 凭证位置

凭证存储在 `.credentials/`（已gitignore）：
- `example-api.txt` — API密钥示例

---

## 已安装工具配置

### browser-use
- **安装**: `npm install -g browser-use`
- **状态**: ✅ 已安装
- **用途**: 浏览器自动化

### agent-browser
- **安装**: `npm install -g agent-browser`
- **状态**: ✅ 已安装
- **用途**: 浏览器自动化（Rust版）

### PDF 处理
- **依赖**: Python 3.10 + pypdf/pdfplumber/reportlab
- **状态**: ✅ 已安装
- **用途**: PDF读取、提取、合并、创建

### Tavily搜索
- **需要**: TAVILY_API_KEY 环境变量
- **状态**: ✅ 已配置 (tvly-dev-***)
- **申请**: https://tavily.com

---

## 搜索任务参考（参考exa分类）

| 任务类型 | 推荐方式 | 说明 |
|----------|----------|------|
| **查最新新闻** | web_search | tavily擅长实时信息 |
| **找代码示例** | web_search + 浏览器 | 搜索 + 打开详情页 |
| **查公司信息** | web_search | tavily可搜索公司新闻 |
| **深度研究** | web_search + 浏览器 | 多次搜索 + 整合 |
| **技术文档** | web_fetch | 直接读取文档 |

---

## 常见工作流

### 1. 搜索 → 浏览器 → 读取
```python
# 1. 先搜索
results = web_search("关键词")

# 2. 用户选择后打开浏览器
browser(action="open", url=results[0].url)

# 3. 读取详情
page_content = web_fetch(url=results[0].url)
```

### 2. 检测异常 → 自动修复 → 记录
```python
# 1. 检测异常
if detect_anomaly():
    # 2. 尝试修复
    result = auto_repair()
    # 3. 记录到.learnings/
    log_to_learnings(result)
```

---

## 故障排除

| 问题 | 可能原因 | 解决方案 |
|------|----------|----------|
| web_search失败 | Rate limit | 等待后重试 |
| 浏览器打不开 | 端口占用 | browser(action="close") |
| 文件读取失败 | 路径错误 | 检查绝对路径 |
| 子代理无响应 | 超时 | 增加timeoutSeconds |

---

## 写作偏好

[记录写作风格偏好]

---

## 注意事项

- 技能定义工具的*工作方式*
- 本文件记录*你的特定*配置
- 凭证只存位置，不存实际内容
