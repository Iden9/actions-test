---
title: "gitgnore 的基本配置"
date: 2024-11-02
categories: ["git"]
---

## 在 `.gitignore` 文件中，你可以指定不希望被 Git 跟踪的文件和目录。以下是一些常见的设置方法：

1. **忽略特定文件**：
   ```plaintext
   # 忽略某个特定文件
   secret.txt
   ```

2. **忽略特定目录**：
   ```plaintext
   # 忽略某个目录及其内容
   logs/
   ```

3. **忽略某种类型的文件**：
   ```plaintext
   # 忽略所有的 .log 文件
   *.log

   # 忽略所有的 .tmp 文件
   *.tmp
   ```

4. **忽略所有文件，但保留特定文件**：
   ```plaintext
   # 忽略所有的 .txt 文件，但保留 example.txt
   *.txt
   !example.txt
   ```

5. **忽略特定模式的文件**：
   ```plaintext
   # 忽略所有在 temp 目录下的文件
   temp/*
   ```

6. **忽略全局配置**（例如操作系统生成的文件）：
   ```plaintext
   # macOS 系统生成的文件
   .DS_Store

   # Windows 系统生成的文件
   Thumbs.db
   ```

创建或编辑 `.gitignore` 文件后，确保它位于你的 Git 仓库根目录下。设置好后，Git 将忽略匹配这些规则的文件和目录，不再将它们提交到版本控制中。