# 故障排查指南 | Troubleshooting Guide

## 如果应用没有响应 | If the App is Not Responding

### 第一步：测试 API 连接

1. 打开应用
2. 滚动到底部的"设置"区域
3. 输入您的 DeepSeek API Key
4. 点击"🧪 Test API Connection / 测试 API 连接"按钮
5. 查看结果：
   - ✅ 如果显示"连接成功"，说明 API 工作正常
   - ❌ 如果显示错误，请查看错误信息

### 第二步：检查浏览器控制台

打开浏览器开发者工具（按 F12 或右键点击 → 检查）：

**Chrome/Edge:**
1. 按 F12 打开开发者工具
2. 点击"Console"（控制台）标签
3. 查找红色错误信息

**Safari:**
1. 按 Cmd+Option+C 打开控制台
2. 查找错误信息

**Firefox:**
1. 按 F12 打开开发者工具
2. 点击"Console"标签
3. 查找错误信息

### 常见错误及解决方法

#### 错误 1：API Key 无效
```
错误信息：Invalid API key / Unauthorized
解决方法：
1. 访问 https://platform.deepseek.com/api_keys
2. 确认您的 API Key 是否有效
3. 创建新的 API Key 并替换
4. 确保 API Key 以 "sk-" 开头
```

#### 错误 2：网络连接失败
```
错误信息：Failed to fetch / Network error
解决方法：
1. 检查您的网络连接
2. 确认防火墙没有阻止 api.deepseek.com
3. 尝试使用 VPN（如果在某些地区）
4. 检查是否有代理设置干扰
```

#### 错误 3：CORS 错误
```
错误信息：CORS policy / Access-Control-Allow-Origin
解决方法：
这是正常现象，因为浏览器的安全策略。解决方案：
1. 确保使用 HTTPS 访问应用（Netlify 自动提供）
2. 不要使用 file:// 协议本地打开（必须通过服务器）
```

#### 错误 4：配额超限
```
错误信息：Quota exceeded / Rate limit
解决方法：
1. 检查 DeepSeek 账户余额
2. 查看 API 使用限制
3. 等待限制重置（通常每分钟/小时重置）
```

### 第三步：使用测试命令

在浏览器控制台中运行以下命令测试：

```javascript
// 测试 API Key 是否已保存
console.log('API Key exists:', !!localStorage.getItem('deepseek_api_key'));

// 测试 fetch 功能
fetch('https://api.deepseek.com/chat/completions', {
    method: 'POST',
    headers: {
        'Content-Type': 'application/json',
        'Authorization': 'Bearer ' + document.getElementById('apiKey').value
    },
    body: JSON.stringify({
        model: 'deepseek-chat',
        messages: [{ role: 'user', content: 'test' }],
        max_tokens: 10
    })
}).then(r => r.json()).then(d => console.log('API Response:', d)).catch(e => console.error('API Error:', e));
```

### 第四步：清除缓存

如果问题持续：

1. 清除浏览器缓存
2. 清除本地存储：
   - 打开控制台
   - 输入：`localStorage.clear()`
   - 刷新页面
   - 重新输入 API Key

### 调试模式

应用已内置详细的控制台日志。在控制台中您会看到：

- "Sending message: ..." - 发送消息时
- "Calling DeepSeek API..." - 调用 API 时
- "Response status: 200" - API 响应状态
- "Received response: ..." - 收到回复时
- 各种错误信息（如有）

### 检查清单

- [ ] API Key 已正确输入（以 sk- 开头）
- [ ] API Key 已保存（刷新页面后仍然存在）
- [ ] 网络连接正常
- [ ] 浏览器是最新版本
- [ ] 没有浏览器扩展干扰（尝试无痕模式）
- [ ] DeepSeek 账户有余额
- [ ] 通过 HTTPS 访问（而非 HTTP 或 file://）

### 联系支持

如果以上步骤都无法解决问题，请提供以下信息：

1. 浏览器类型和版本
2. 错误信息截图
3. 控制台日志（F12 → Console 中的内容）
4. API Key 前10个字符（例如：sk-1234567...）
5. 测试 API 连接的结果

## 额外提示

### 语音功能不工作？

1. 确保使用 Chrome 或 Edge 浏览器
2. 允许麦克风权限
3. 检查系统麦克风设置
4. 在 HTTPS 环境下使用（Netlify 自动提供）

### 语音播放没有声音？

1. 检查设备音量
2. 确认浏览器允许自动播放音频
3. 尝试手动点击 🔊 图标
4. 检查系统音频设置

### 界面显示异常？

1. 清除浏览器缓存
2. 强制刷新（Ctrl+F5 或 Cmd+Shift+R）
3. 确保网络能访问 Google Fonts

---

**如果您发现 bug 或有改进建议，欢迎反馈！**
