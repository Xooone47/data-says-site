# GitHub Pages 自动部署指南

## 概述

此项目已配置了GitHub Actions工作流，当您将代码推送到GitHub仓库时，会自动将`dist`目录部署到GitHub Pages。

## 配置步骤

### 1. 在GitHub上启用GitHub Pages

1. 将您的代码推送到GitHub仓库
2. 进入仓库的 **Settings** 页面
3. 在左侧菜单中找到 **Pages**
4. 在 **Source** 部分选择：
   - **GitHub Actions**（而不是从分支部署）

### 2. 工作流触发条件

- **自动触发**：当推送到 `main` 分支时
- **手动触发**：在GitHub仓库的 **Actions** 标签页中手动运行工作流

### 3. 部署流程

工作流会自动执行以下步骤：

1. 检出代码
2. 配置Pages部署环境
3. 上传`dist`目录作为静态网站
4. 部署到GitHub Pages

## 重要说明

### 关于dist目录

- 您的项目已经包含构建好的`dist`目录
- 工作流会直接使用现有的`dist`目录内容
- 不需要额外的构建步骤

### 关于路径问题

在您的`index.html`中，资源路径使用了绝对路径：
```html
<script type="module" crossorigin src="/data-says-site/static/js/index-C5EG3zoJ.js">
```

如果部署后出现资源加载问题，您可能需要：

1. 修改为相对路径：`./static/js/index-C5EG3zoJ.js`
2. 或者在GitHub Pages设置中配置正确的base路径

### 验证部署

部署完成后，您可以在以下地址访问网站：
```
https://[您的GitHub用户名].github.io/[仓库名]/
```

## 故障排除

### 常见问题

1. **资源404错误**：检查资源路径是否正确
2. **部署失败**：查看GitHub Actions日志了解详细错误信息
3. **页面空白**：检查浏览器控制台是否有JavaScript错误

### 调试建议

- 在本地浏览器中打开`dist/index.html`测试功能
- 检查所有资源文件是否存在于dist目录中
- 确保GitHub Pages设置正确

## 手动部署

如果您需要手动触发部署：

1. 进入GitHub仓库的 **Actions** 标签页
2. 选择 **Deploy to GitHub Pages** 工作流
3. 点击 **Run workflow** 按钮
4. 选择分支并运行