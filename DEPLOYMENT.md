# 📱 SmartBeamX Vercel 部署指南

## 🎯 **部署概览**

SmartBeamX 项目采用双重部署策略：
- **本地开发**: 使用标准 uniapp 命令
- **Vercel部署**: 使用自定义构建脚本生成演示页面

## 🚀 **快速部署步骤**

### **方法1: 通过 Vercel 网站 (推荐)**

1. **登录 Vercel**
   ```
   访问: https://vercel.com
   使用 GitHub 账号登录
   ```

2. **导入项目**
   ```
   点击 "New Project"
   选择 "Import Git Repository"
   选择仓库: fatman1221/smart-beamx
   ```

3. **配置部署设置**
   ```
   Framework Preset: Other
   Build Command: node build-for-vercel.js
   Output Directory: dist
   Install Command: npm install --legacy-peer-deps
   Root Directory: ./
   ```

4. **部署**
   ```
   点击 "Deploy" 按钮
   等待构建完成 (约1-2分钟)
   ```

### **方法2: 通过 Vercel CLI**

1. **安装 CLI**
   ```bash
   npm install -g vercel
   ```

2. **登录**
   ```bash
   vercel login
   # 选择 GitHub 登录方式
   ```

3. **部署**
   ```bash
   vercel --prod
   ```

## ⚙️ **配置文件说明**

### **vercel.json**
```json
{
  "version": 2,
  "buildCommand": "node build-for-vercel.js",
  "outputDirectory": "dist",
  "installCommand": "npm install --legacy-peer-deps"
}
```

### **build-for-vercel.js**
- 自定义构建脚本
- 生成适合 Vercel 的静态 HTML 页面
- 包含 SmartBeamX 功能演示
- 响应式设计，支持移动端

## 🛠 **本地测试**

在推送代码前，可以本地测试构建：

```bash
# 测试构建脚本
node build-for-vercel.js

# 检查输出
ls -la dist/

# 本地预览 (可选)
cd dist && python -m http.server 8000
# 访问: http://localhost:8000
```

## 🔄 **自动部署**

每次推送到 `main` 分支时，Vercel 会自动：
1. 检测到代码变更
2. 运行 `npm install --legacy-peer-deps`
3. 执行 `node build-for-vercel.js`
4. 部署 `dist/` 目录到 CDN

## 📱 **部署结果**

成功部署后，您将获得：
- **演示网站**: 展示 SmartBeamX 所有功能模块
- **响应式设计**: 完美适配手机和桌面
- **动态效果**: 包含粒子动画和交互
- **GitHub链接**: 直接链接到源码仓库

## 🎨 **功能展示**

演示页面包含以下模块：
- 🏠 首页
- 🔧 模式
- 🎬 场景  
- 🛒 商城
- 👤 我的
- ⚙️ 设置

## 🐛 **常见问题**

### **构建失败**
```bash
# 检查 Node.js 版本
node --version  # 推荐 16.x 或更高

# 清理依赖重新安装
rm -rf node_modules package-lock.json
npm install --legacy-peer-deps
```

### **部署超时**
- Vercel 免费版有构建时间限制
- 我们的构建脚本很轻量，通常不会超时

### **更新不生效**
- 检查是否推送到了 `main` 分支
- 在 Vercel 仪表板检查构建日志

## 📊 **监控和维护**

- **构建状态**: 在 Vercel 仪表板查看
- **访问统计**: Vercel 提供基本分析
- **错误监控**: 检查浏览器控制台

---

🎉 **恭喜！您的 SmartBeamX 项目现在可以在全球 CDN 上访问了！**
