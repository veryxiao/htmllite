# HTMLLite 规范 v1.2

<p align="center">
  <img src="assets/logo.svg" alt="HTMLLite Logo" width="120">
</p>

<p align="center">
  <a href="https://github.com/veryxiao/htmllite/releases">
    <img src="https://img.shields.io/github/v/release/veryxiao/htmllite" alt="Latest Release">
  </a>
  <a href="LICENSE">
    <img src="https://img.shields.io/badge/license-MIT-blue.svg" alt="License">
  </a>
  <a href="https://github.com/veryxiao/htmllite/stargazers">
    <img src="https://img.shields.io/github/stars/veryxiao/htmllite" alt="Stars">
  </a>
</p>

<p align="center">
  为人工智能和大型语言模型设计的轻量级HTML子集
</p>

## 🚀 概述

HTMLLite 是一种专为AI和LLM设计的严格HTML子集，旨在将复杂文档转化为机器可理解的高质量结构化数据。

### 核心特性

- ⚡ **轻量纯粹** - 只包含定义内容结构的标签
- 🎯 **结构保真** - 无损保留文档关键结构
- 🧩 **原子化区块** - 独立且上下文完整的知识单元
- 🔗 **语义链接** - 明确的区块间逻辑关系
- 💎 **精确语义** - v1.2新增`<dl>`标签支持

## 📖 文档

- [在线文档](https://htmllite.org/)
- [规范详情 (Markdown)](docs/spec-v1.2.md)
- [English Version](README-EN.md)

## 🔧 快速开始

### 基本示例

```html
<div class="htmllite-document">
    <div data-htmllite-block="true">
        <h2>示例标题</h2>
        <dl>
            <dt>键</dt>
            <dd>值</dd>
        </dl>
    </div>
</div>
