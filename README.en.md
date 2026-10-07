<!-- README language switch -->
[![中文](https://img.shields.io/badge/%E4%B8%AD%E6%96%87-555555?style=for-the-badge)](README.md) [![English](https://img.shields.io/badge/English-1677ff?style=for-the-badge)](README.en.md)
<!-- /README language switch -->

# 📚 JM Bot — Doujinshi Download and Packaging Bot

A QQ bot plugin built with [Nonebot2](https://v2.nonebot.dev/) and the [jmcomic](https://github.com/tonquer/JMComic-qt) wrapper library. It downloads adult doujinshi through commands and packages them as PDF or ZIP files for delivery to group chats.

---

## 📸 Usage screenshots

### ✅ Single-chapter download (`.jm` command)

Use `.jm [comic ID]` to download a title, automatically generate a PDF, and upload it to the QQ group:

![Single-title request](demo/%E5%8D%95%E6%9C%AC%E8%AF%B7%E6%B1%82.png)

---

### ✅ Multi-chapter packaging (now included in `.jm`; `.jmzip` is optional)

Use `.jmzip [comic ID]` to retrieve cached chapter PDFs and upload them in a ZIP archive:

![Multi-chapter request](demo/%E5%A4%9A%E6%9C%AC%E8%AF%B7%E6%B1%82.png)

## 📦 Features

- Download a title with `.jm [comic ID]`; this can be used as the general-purpose command.
- Detect chapter structure automatically and produce a single PDF or a ZIP of chapter PDFs.
- Retrieve previously cached archives with `.jmzip [comic ID]`; this command is no longer required.
- Remove the cache after a successful upload to avoid leaving resources behind.
- Clean up old cache files during downloads.

---

## 🧱 Project structure

```text
jm_bot/
├── jm_handler.py           # Command handling and workflow management
├── jm_downloader.py        # jmcomic integration, downloading, and organization
├── jm_tools.py             # Image-to-PDF conversion, chapter merging, and packaging
├── cache/
│   ├── jm_config.yml       # jmcomic configuration; provide this yourself
│   └── jm_download/        # Download cache, created at runtime
├── requirements.txt
└── README.md
```

---

## 🧰 Dependencies

Install the required dependencies:

```bash
pip install -r requirements.txt
```

**Or install them manually:**

```bash
pip install nonebot2 nonebot-adapter-onebot jmcomic pillow
```

---

## ⚙️ Usage

> Make sure Nonebot2 is deployed correctly and this plugin module is loaded.

### 1. Prepare `jm_config.yml`

Place your `jm_config.yml` in the project's `cache/` subdirectory. For an example configuration, see:
https://github.com/niuhuan/jmcomic/blob/master/jmcomic/config_default.yml

### 2. Start Nonebot2

```bash
nb run
```

### 3. Use these commands in a QQ group

#### Download a title

```text
.jm 472537
```

#### Package an archive (also supported by `.jm`)

```text
.jmzip 472537
```

---

## 📥 File uploads

- Upload the PDF or ZIP to the QQ group once the download finishes.
- Wait 90 seconds after a successful upload, then delete the uploaded file automatically.
- Notify the user if the file is too large (>90 MB).

---

## 🧼 Cache cleanup

The system automatically cleans up cached files:

- When a download fails or is interrupted.
- After a download completes and is sent.
- After a user runs `.jmzip` and processing succeeds.

---

## ✅ TODO

- ✅ Random title requests (commented-out code scaffold).
- ✅ Selectable image formats, such as WebP conversion.
- ✅ Multithreaded download optimization.

---

## 📄 License

This project is for learning and discussion only. Commercial or illegal use is prohibited. Copyright in the original images and comic content belongs to the respective creators.
