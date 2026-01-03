# Netlify 环境变量配置指南 | Environment Variables Setup Guide

## 为什么使用环境变量？| Why Use Environment Variables?

将 API Key 存储在环境变量中可以：
- ✅ **保护隐私**：API Key 不会暴露在前端代码中
- ✅ **防止泄露**：用户无法在浏览器中看到您的 API Key
- ✅ **集中管理**：在 Netlify 后台统一管理密钥
- ✅ **安全性高**：符合最佳安全实践

## 配置步骤 | Setup Steps

### 第一步：获取 DeepSeek API Key

1. 访问 https://platform.deepseek.com/
2. 注册并登录账户
3. 进入 "API Keys" 页面
4. 点击 "Create API Key"
5. 复制生成的 API Key（格式：sk-xxxxxxxxxxxxxxxx）
6. **妥善保存** - API Key 只显示一次！

### 第二步：在 Netlify 中配置环境变量

#### 通过 Netlify 网站配置（推荐）

1. 登录 https://app.netlify.com/
2. 选择您的站点
3. 进入 **Site settings**（站点设置）
4. 在左侧菜单中选择 **Environment variables**（环境变量）
5. 点击 **Add a variable**（添加变量）
6. 设置以下内容：
   - **Key (变量名)**：`DEEPSEEK_API_KEY`
   - **Value (值)**：粘贴您的 DeepSeek API Key（sk-...）
   - **Scopes**：选择所有环境（Production, Deploy Previews, Branch Deploys）
7. 点击 **Create variable**（创建变量）
8. **重新部署站点**以使更改生效

#### 重新部署站点

配置环境变量后，您需要触发重新部署：

**方法 1：在 Netlify 界面**
1. 进入 **Deploys** 标签
2. 点击 **Trigger deploy** → **Deploy site**

**方法 2：推送代码更新**
如果您使用 Git 部署，推送任何更改都会触发重新部署

### 第三步：验证配置

1. 等待部署完成
2. 访问您的应用网址
3. 查看设置区域的 "API Key Status"
4. 应该显示：✅ API Key 已配置 / API Key Configured
5. 点击"测试 API 连接"按钮验证

## 文件结构 | File Structure

确保您的项目包含以下文件结构：

```
your-project/
├── index.html              # 主应用文件
├── netlify.toml            # Netlify 配置
└── netlify/
    └── functions/
        └── get-api-key.js  # 获取 API Key 的函数
```

## 部署清单 | Deployment Checklist

- [ ] 已获取 DeepSeek API Key
- [ ] 文件结构正确（包含 netlify/functions/ 目录）
- [ ] 已上传所有文件到 Netlify
- [ ] 已在 Netlify 中配置 `DEEPSEEK_API_KEY` 环境变量
- [ ] 已重新部署站点
- [ ] API Key 状态显示为"已配置"
- [ ] 测试 API 连接成功

## 常见问题 | FAQ

### Q1: 配置环境变量后应用仍显示"API Key 未配置"？

**A:** 环境变量更改后需要重新部署站点：
1. 进入 Netlify → Deploys
2. 点击 Trigger deploy → Deploy site
3. 等待部署完成后再次检查

### Q2: 如何验证环境变量是否正确设置？

**A:** 在 Netlify 中：
1. Site settings → Environment variables
2. 找到 `DEEPSEEK_API_KEY`
3. 值应该以 `sk-` 开头
4. 如果不对，编辑并重新部署

### Q3: 可以在本地测试吗？

**A:** 可以，使用 Netlify CLI：

```bash
# 安装 Netlify CLI
npm install -g netlify-cli

# 在项目目录中创建 .env 文件
echo "DEEPSEEK_API_KEY=sk-your-key-here" > .env

# 本地运行
netlify dev
```

### Q4: 环境变量安全吗？

**A:** 是的，非常安全：
- 环境变量只在服务器端可见
- 前端代码中看不到实际的 API Key
- Netlify Functions 在服务器上运行
- 用户无法通过浏览器获取 API Key

### Q5: 如果 API Key 泄露怎么办？

**A:** 立即采取以下措施：
1. 登录 DeepSeek 平台
2. 删除泄露的 API Key
3. 创建新的 API Key
4. 在 Netlify 中更新环境变量
5. 重新部署站点

### Q6: 可以使用其他环境变量名吗？

**A:** 可以，但需要同步修改：
1. 在 `netlify/functions/get-api-key.js` 中修改 `process.env.DEEPSEEK_API_KEY`
2. 在 Netlify 中使用相同的变量名

## 故障排除 | Troubleshooting

### 问题：Functions 无法访问

**解决方案：**
1. 确认 `netlify.toml` 中设置了 `functions = "netlify/functions"`
2. 确认 `get-api-key.js` 文件存在于正确位置
3. 重新部署站点

### 问题：CORS 错误

**解决方案：**
`get-api-key.js` 中已包含 CORS 头，如果仍有问题：
1. 确认使用 HTTPS 访问（Netlify 自动提供）
2. 检查浏览器控制台的具体错误
3. 确认 Netlify Function 正常部署

### 问题：API 调用失败

**解决方案：**
1. 打开浏览器控制台（F12）
2. 检查网络请求到 `/.netlify/functions/get-api-key`
3. 查看返回的响应
4. 确认 API Key 格式正确（以 sk- 开头）

## 最佳实践 | Best Practices

1. **定期更换 API Key**：建议每月更换一次
2. **监控使用量**：在 DeepSeek 平台查看 API 使用情况
3. **设置预算限制**：在 DeepSeek 中设置月度预算
4. **备份配置**：记录环境变量配置（但不包括实际 Key）
5. **使用不同的 Key**：为开发和生产环境使用不同的 API Key

## 安全提示 | Security Tips

⚠️ **切勿这样做：**
- ❌ 在前端代码中硬编码 API Key
- ❌ 将 API Key 提交到公开的 Git 仓库
- ❌ 在浏览器 localStorage 中存储 API Key
- ❌ 通过 URL 参数传递 API Key
- ❌ 在客户端 JavaScript 中直接调用 DeepSeek API

✅ **应该这样做：**
- ✅ 使用 Netlify 环境变量存储 API Key
- ✅ 通过服务器端 Functions 访问 API Key
- ✅ 定期更换 API Key
- ✅ 监控 API 使用情况
- ✅ 为不同环境使用不同的 Key

## 技术说明 | Technical Details

### Netlify Functions 工作原理

1. 用户访问应用
2. 前端 JavaScript 调用 `/.netlify/functions/get-api-key`
3. Netlify Function 在服务器端运行
4. Function 从环境变量读取 API Key
5. 返回 API Key 给前端
6. 前端使用 API Key 调用 DeepSeek API

### 为什么这样更安全？

- API Key 存储在 Netlify 服务器上
- 只有 Netlify Function 能访问环境变量
- 前端代码不包含任何敏感信息
- 用户无法通过浏览器开发工具看到 API Key
- 即使前端代码被复制，也无法获取 API Key

---

## 需要帮助？

如果配置过程中遇到问题：
1. 查看 [TROUBLESHOOTING.md](TROUBLESHOOTING.md)
2. 检查 Netlify Function 日志
3. 查看浏览器控制台错误
4. 确认所有文件都已正确上传

**配置完成后，您的应用将更加安全可靠！** 🔒
