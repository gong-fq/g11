# AI英语语法学习助手 | English Grammar Coach

龚凤乾教授开发的智能英语语法学习应用程序

## 功能特点

✅ **双语支持**：完整的中英文双语界面
✅ **AI智能对话**：采用 DeepSeek 大语言模型提供专业语法讲解
✅ **语音交互**：支持语音输入和语音输出（文字转语音）
✅ **文字输入**：传统文字输入方式
✅ **语法主题**：预设8大常见语法主题快速学习
✅ **响应式设计**：完美支持手机、平板、电脑

## 部署到 Netlify

### 方法一：通过 Netlify 网站部署（推荐）

1. 注册/登录 [Netlify](https://app.netlify.com/)
2. 点击 "Add new site" -> "Deploy manually"
3. 将以下所有文件和文件夹拖拽到部署区域：
   - `index.html`
   - `netlify.toml`
   - `netlify/` 文件夹（包含 functions 子文件夹）
4. 等待部署完成
5. **重要：** 配置环境变量（见下方"使用说明"）
6. 重新部署站点以使环境变量生效
7. 您会获得一个类似 `https://your-app-name.netlify.app` 的网址

### 方法二：通过 GitHub 自动部署

1. 创建 GitHub 仓库
2. 上传 `index.html` 和 `netlify.toml` 到仓库
3. 在 Netlify 中选择 "Import from Git"
4. 连接您的 GitHub 仓库
5. Netlify 会自动检测配置并部署

### 方法三：使用 Netlify CLI

```bash
# 安装 Netlify CLI
npm install -g netlify-cli

# 登录
netlify login

# 在项目目录中部署
netlify deploy --prod
```

## 使用说明

### 1. 获取 DeepSeek API Key

1. 访问 [DeepSeek Platform](https://platform.deepseek.com/)
2. 注册并登录账户
3. 在 API Keys 页面创建新的 API Key
4. 复制 API Key（格式：sk-...）

### 2. 配置 Netlify 环境变量（重要！）

**为了安全起见，API Key 不再在前端输入，而是通过 Netlify 环境变量配置：**

1. 登录 Netlify 后台
2. 选择您的站点
3. 进入 **Site settings** → **Environment variables**
4. 添加变量：
   - **Key**: `DEEPSEEK_API_KEY`
   - **Value**: 您的 DeepSeek API Key
5. 保存并重新部署站点

📖 **详细配置步骤：** 请查看 [NETLIFY_ENV_SETUP.md](NETLIFY_ENV_SETUP.md)

### 3. 开始使用

**文字输入模式：**
- 在输入框中输入您的语法问题
- 点击发送按钮或按 Enter 键

**语音输入模式：**
- 点击"Voice"切换到语音模式
- 点击麦克风按钮开始录音
- 说完后自动识别并发送

**快速主题：**
- 点击左侧栏的语法主题按钮快速开始学习

**语音播放：**
- AI 回复会自动朗读
- 也可以点击消息旁的🔊图标重新播放

## 技术特点

- **纯前端应用**：无需后端服务器，直接部署即可使用
- **响应式设计**：移动端和桌面端完美适配
- **现代化界面**：采用渐变色、动画效果和专业排版
- **本地存储**：API Key 安全存储在用户浏览器中
- **会话记忆**：保持对话上下文，提供连贯的学习体验

## 浏览器兼容性

- ✅ Chrome 60+
- ✅ Edge 79+
- ✅ Safari 14+
- ✅ Firefox 60+

**注意**：语音识别功能在 Chrome 和 Edge 上表现最佳

## API 费用说明

DeepSeek API 按使用量计费：
- 非常经济实惠的定价
- 新用户通常有免费额度
- 详情请查看 [DeepSeek 定价页面](https://platform.deepseek.com/pricing)

## 安全提示

⚠️ **重要安全改进**：
- ✅ API Key 现在通过 Netlify 环境变量安全存储
- ✅ 用户无法在浏览器中看到 API Key
- ✅ 前端代码不包含任何敏感信息
- ✅ 符合安全最佳实践
- 请妥善保管您的 DeepSeek API Key
- 定期更换 API Key（建议每月一次）
- 如果 API Key 泄露，请立即在 DeepSeek 平台删除并创建新的
- 在 Netlify 中更新环境变量后重新部署

## 自定义与扩展

您可以根据需要修改 `index.html` 中的以下内容：

### 修改语法主题
在 HTML 中找到 `.topic-list` 部分，添加或修改主题按钮

### 调整 AI 系统提示词
在 JavaScript 中找到 `systemPrompt` 变量，修改 AI 的教学风格

### 更改界面颜色
在 CSS `:root` 部分修改颜色变量

### 添加更多语言
扩展语言切换功能，添加更多语言支持

## 故障排除

**📖 完整故障排查指南：请查看 [TROUBLESHOOTING.md](TROUBLESHOOTING.md)**

### 快速诊断步骤

1. **使用内置测试功能**
   - 滚动到设置区域
   - 点击"🧪 Test API Connection / 测试 API 连接"按钮
   - 查看测试结果

2. **检查浏览器控制台**
   - 按 F12 打开开发者工具
   - 查看 Console 标签中的错误信息
   - 应用会显示详细的调试日志

3. **确认基本设置**
   - API Key 格式正确（以 sk- 开头）
   - 网络连接正常
   - 使用 HTTPS 访问（Netlify 自动提供）

### 常见问题快速解决

### API 错误
- 检查 API Key 是否正确
- 确认 DeepSeek 账户有足够额度
- 检查网络连接
- 查看控制台中的详细错误信息

### 语音识别不工作
- 确保使用 Chrome 或 Edge 浏览器
- 检查麦克风权限
- 确认浏览器支持 Web Speech API

### 语音播放没有声音
- 检查设备音量
- 确认浏览器允许自动播放音频
- 尝试手动点击🔊图标

## 联系方式

开发者：龚凤乾教授（Mr. Gong Fengqian）
用途：帮助中国学生扎实掌握英语语法

## 许可证

本项目为教育用途开发，请遵守相关使用规范。

---

**祝您学习愉快！Happy Learning!** 🎓
