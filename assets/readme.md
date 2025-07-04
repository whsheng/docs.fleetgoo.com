对于文档中的图片和 logo 等静态资源，建议按以下方式组织:

## 静态资源组织方式
docs/
├── assets/                    # 静态资源根目录
│   ├── images/               # 通用图片目录
│   │   ├── logo.png         # 网站 logo
│   │   ├── favicon.ico      # 网站图标
│   │   └── common/          # 通用图片，如界面元素等
│   ├── platform/            # 平台相关图片
│   │   ├── dashboard/       # 控制台界面截图
│   │   └── features/        # 功能特性图片
│   ├── mobile/              # 移动应用相关图片
│   │   ├── ios/            # iOS 应用截图
│   │   ├── android/        # 安卓应用截图
│   │   └── miniprogram/    # 小程序截图
│   └── videos/              # 视频资源目录
│       ├── tutorials/       # 教程视频
│       └── demos/          # 演示视频

## 引用方式
在文档中，使用相对路径引用图片，例如：
```markdown
![Logo](/assets/images/logo.png)
![控制台](/assets/platform/dashboard/main.png)
```
## 命名规范
- 使用小写字母
- 单词间用连字符（-）分隔
- 建议包含尺寸信息，如：logo-120x120.png

## 优化建议
- 压缩图片以减少加载时间
- 考虑使用 WebP 格式
- 大文件（如视频）建议使用外部存储或 CDN