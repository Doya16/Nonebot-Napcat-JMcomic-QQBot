<!-- README language switch -->
[![中文](https://img.shields.io/badge/%E4%B8%AD%E6%96%87-1677ff?style=for-the-badge)](README.md) [![English](https://img.shields.io/badge/English-555555?style=for-the-badge)](README.en.md)
<!-- /README language switch -->

# 📚 JM Bot - 同人本子下载与打包机器人

这是一个基于 [Nonebot2](https://v2.nonebot.dev/) + [jmcomic](https://github.com/tonquer/JMComic-qt) 封装库开发的 QQ 机器人插件，支持通过命令下载绅士本子，并打包成 PDF 或 ZIP 发送到群聊。

---

## 📸 使用截图演示

### ✅ 单章节本子下载（`.jm` 命令）
通过 `.jm [本子ID]` 命令下载单本本子，会自动生成 PDF 并上传到 QQ 群：

![单本请求效果](demo/%E5%8D%95%E6%9C%AC%E8%AF%B7%E6%B1%82.png)

---

### ✅ 多章节本子打包（已经整合进`.jm` 命令, 可以不用`.jmzip 命令`）
通过 `.jmzip [本子ID]` 获取已缓存的章节 PDF 并打包成 ZIP 上传：

![多本请求效果](demo/%E5%A4%9A%E6%9C%AC%E8%AF%B7%E6%B1%82.png)


## 📦 功能特性

- 支持命令 `.jm [本子ID]` 下载目标本子 （可统一使用）
- 自动识别章节结构，合并成单 PDF 或章节 PDF 后打包 ZIP
- 支持 `.jmzip [本子ID]` 获取之前缓存的压缩包（可不再使用）
- 文件上传成功后自动销毁缓存，避免资源泄露
- 下载过程中自动清理旧缓存

---

## 🧱 项目结构

```
jm_bot/
├── jm_handler.py           # 主处理逻辑，接收命令、管理流程
├── jm_downloader.py        # 与 jmcomic 库交互，下载与整理
├── jm_tools.py             # 图片转 PDF、章节合并、打包工具
├── cache/
│   ├── jm_config.yml       # jmcomic 配置文件（你需要自己准备）
│   └── jm_download/        # 下载缓存目录（运行时自动生成）
├── requirements.txt
└── README.md
```

---

## 🧰 安装依赖

你需要先安装以下依赖：

```bash
pip install -r requirements.txt
```

**或手动安装：**

```bash
pip install nonebot2 nonebot-adapter-onebot jmcomic pillow
```

---

## ⚙️ 使用方式

> 请确保你已正确部署了 Nonebot2，并加载本插件模块。

### 1. 准备 `jm_config.yml`

在项目目录的 `cache/` 子目录下，放置你准备好的 `jm_config.yml` 文件，内容示例可参考：
https://github.com/niuhuan/jmcomic/blob/master/jmcomic/config_default.yml

### 2. 启动 Nonebot2

```bash
nb run
```

### 3. 在 QQ 群中使用以下命令：

#### 下载本子：
```
.jm 472537
```

#### 打包压缩（也可以用.jm命令）：
```
.jmzip 472537
```

---

## 📥 文件上传机制说明

- 下载完成后会将 PDF 或 ZIP 文件上传至 QQ 群；
- 上传成功后会等待 90 秒自动删除；
- 若文件过大（>90MB），会发出提示信息；

---

## 🧼 缓存清理机制

系统会自动清理以下情况的缓存：
- 下载失败或异常中断
- 下载完成并发送后
- 用户主动发起 `.jmzip` 并处理成功后

---

## ✅ TODO

- ✅ 支持随机召唤本子（已注释代码框架）
- ✅ 支持图片格式自选（如 webp 转换）
- ✅ 多线程下载优化

---

## 📄 License

本项目仅供学习与交流，禁止用于商业或非法用途。原图与本子内容版权归原作者所有。
