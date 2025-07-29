
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta name="description" content="HTMLLite规范v1.2 - 为人工智能和大型语言模型设计的轻量级HTML子集">
    <meta name="keywords" content="HTMLLite, AI, LLM, 结构化数据, 知识库, RAG">
    <title>HTMLLite规范 v1.2 | 为AI优化的轻量级HTML子集</title>
    
    <!-- 引入专业字体 -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&family=JetBrains+Mono:wght@400;500&display=swap" rel="stylesheet">
    
    <style>
        /* 设计系统变量 */
        :root {
            /* 色彩系统 */
            --color-primary: #2563eb;
            --color-primary-dark: #1d4ed8;
            --color-primary-light: #3b82f6;
            --color-secondary: #10b981;
            --color-accent: #f59e0b;
            --color-danger: #ef4444;
            
            /* 中性色 */
            --color-gray-50: #f9fafb;
            --color-gray-100: #f3f4f6;
            --color-gray-200: #e5e7eb;
            --color-gray-300: #d1d5db;
            --color-gray-400: #9ca3af;
            --color-gray-500: #6b7280;
            --color-gray-600: #4b5563;
            --color-gray-700: #374151;
            --color-gray-800: #1f2937;
            --color-gray-900: #111827;
            
            /* 排版 */
            --font-sans: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
            --font-mono: 'JetBrains Mono', 'Consolas', monospace;
            
            /* 间距 */
            --spacing-xs: 0.5rem;
            --spacing-sm: 1rem;
            --spacing-md: 1.5rem;
            --spacing-lg: 2rem;
            --spacing-xl: 3rem;
            --spacing-2xl: 4rem;
            
            /* 圆角 */
            --radius-sm: 0.375rem;
            --radius-md: 0.5rem;
            --radius-lg: 0.75rem;
            --radius-xl: 1rem;
            
            /* 阴影 */
            --shadow-sm: 0 1px 2px 0 rgb(0 0 0 / 0.05);
            --shadow-md: 0 4px 6px -1px rgb(0 0 0 / 0.1);
            --shadow-lg: 0 10px 15px -3px rgb(0 0 0 / 0.1);
            --shadow-xl: 0 20px 25px -5px rgb(0 0 0 / 0.1);
        }

        /* 基础重置 */
        *, *::before, *::after {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }

        html {
            font-size: 16px;
            scroll-behavior: smooth;
            -webkit-font-smoothing: antialiased;
            -moz-osx-font-smoothing: grayscale;
        }

        body {
            font-family: var(--font-sans);
            line-height: 1.6;
            color: var(--color-gray-800);
            background-color: #ffffff;
            overflow-x: hidden;
        }

        /* 布局容器 */
        .container {
            max-width: 1280px;
            margin: 0 auto;
            padding: 0 var(--spacing-md);
        }

        .content-container {
            max-width: 980px;
            margin: 0 auto;
        }

        /* 顶部导航栏 */
        .navbar {
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            background: rgba(255, 255, 255, 0.95);
            backdrop-filter: blur(10px);
            border-bottom: 1px solid var(--color-gray-200);
            z-index: 1000;
            transition: all 0.3s ease;
        }

        .navbar.scrolled {
            box-shadow: var(--shadow-md);
        }

        .navbar-content {
            display: flex;
            justify-content: space-between;
            align-items: center;
            height: 4rem;
        }

        .navbar-brand {
            display: flex;
            align-items: center;
            gap: var(--spacing-sm);
            text-decoration: none;
            color: var(--color-gray-900);
        }

        .navbar-logo {
            width: 32px;
            height: 32px;
            background: linear-gradient(135deg, var(--color-primary), var(--color-primary-dark));
            border-radius: var(--radius-md);
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            font-weight: 700;
            font-size: 0.875rem;
        }

        .navbar-title {
            font-size: 1.25rem;
            font-weight: 600;
        }

        .navbar-version {
            background: var(--color-primary);
            color: white;
            padding: 0.125rem 0.5rem;
            border-radius: var(--radius-sm);
            font-size: 0.75rem;
            font-weight: 500;
        }

        .navbar-nav {
            display: flex;
            align-items: center;
            gap: var(--spacing-lg);
        }

        .nav-link {
            color: var(--color-gray-600);
            text-decoration: none;
            font-weight: 500;
            transition: color 0.2s;
            position: relative;
        }

        .nav-link:hover {
            color: var(--color-primary);
        }

        .nav-link.active {
            color: var(--color-primary);
        }

        .nav-link.active::after {
            content: '';
            position: absolute;
            bottom: -1.5rem;
            left: 0;
            right: 0;
            height: 3px;
            background: var(--color-primary);
            border-radius: 3px 3px 0 0;
        }

        .download-btn {
            display: inline-flex;
            align-items: center;
            gap: 0.5rem;
            background: var(--color-primary);
            color: white;
            padding: 0.5rem 1.25rem;
            border-radius: var(--radius-md);
            text-decoration: none;
            font-weight: 500;
            transition: all 0.2s;
        }

        .download-btn:hover {
            background: var(--color-primary-dark);
            transform: translateY(-1px);
            box-shadow: var(--shadow-md);
        }

        /* 主页头部 */
        .hero {
            padding: 8rem 0 4rem;
            background: linear-gradient(to bottom, var(--color-gray-50), white);
            text-align: center;
        }

        .hero-content {
            max-width: 800px;
            margin: 0 auto;
        }

        .hero-badge {
            display: inline-flex;
            align-items: center;
            gap: 0.5rem;
            background: var(--color-gray-100);
            color: var(--color-gray-700);
            padding: 0.375rem 1rem;
            border-radius: 9999px;
            font-size: 0.875rem;
            font-weight: 500;
            margin-bottom: var(--spacing-md);
        }

        .hero-badge-dot {
            width: 8px;
            height: 8px;
            background: var(--color-secondary);
            border-radius: 50%;
            animation: pulse 2s infinite;
        }

        .hero-title {
            font-size: 3.5rem;
            font-weight: 700;
            color: var(--color-gray-900);
            margin-bottom: var(--spacing-md);
            letter-spacing: -0.02em;
        }

        .hero-subtitle {
            font-size: 1.25rem;
            color: var(--color-gray-600);
            margin-bottom: var(--spacing-lg);
            line-height: 1.8;
        }

        .hero-actions {
            display: flex;
            gap: var(--spacing-sm);
            justify-content: center;
            flex-wrap: wrap;
        }

        .btn-primary {
            display: inline-flex;
            align-items: center;
            gap: 0.5rem;
            background: var(--color-primary);
            color: white;
            padding: 0.75rem 1.5rem;
            border-radius: var(--radius-md);
            text-decoration: none;
            font-weight: 600;
            transition: all 0.2s;
            border: 2px solid transparent;
        }

        .btn-primary:hover {
            background: var(--color-primary-dark);
            transform: translateY(-1px);
            box-shadow: var(--shadow-lg);
        }

        .btn-secondary {
            display: inline-flex;
            align-items: center;
            gap: 0.5rem;
            background: white;
            color: var(--color-gray-700);
            padding: 0.75rem 1.5rem;
            border-radius: var(--radius-md);
            text-decoration: none;
            font-weight: 600;
            transition: all 0.2s;
            border: 2px solid var(--color-gray-300);
        }

        .btn-secondary:hover {
            background: var(--color-gray-50);
            border-color: var(--color-gray-400);
        }

        /* 内容区域布局 */
        .main-layout {
            display: grid;
            grid-template-columns: 280px 1fr;
            gap: var(--spacing-xl);
            margin: var(--spacing-2xl) 0;
            position: relative;
        }

        /* 侧边栏 */
        .sidebar {
            position: sticky;
            top: 5rem;
            height: fit-content;
            max-height: calc(100vh - 6rem);
            overflow-y: auto;
        }

        .sidebar-section {
            margin-bottom: var(--spacing-lg);
        }

        .sidebar-title {
            font-size: 0.75rem;
            font-weight: 600;
            text-transform: uppercase;
            letter-spacing: 0.05em;
            color: var(--color-gray-500);
            margin-bottom: var(--spacing-sm);
        }

        .sidebar-nav {
            display: flex;
            flex-direction: column;
            gap: 0.25rem;
        }

        .sidebar-link {
            display: block;
            padding: 0.5rem 1rem;
            color: var(--color-gray-600);
            text-decoration: none;
            border-radius: var(--radius-md);
            transition: all 0.2s;
            font-size: 0.875rem;
            position: relative;
        }

        .sidebar-link:hover {
            background: var(--color-gray-100);
            color: var(--color-gray-900);
        }

        .sidebar-link.active {
            background: var(--color-primary);
            color: white;
            font-weight: 500;
        }

        .sidebar-link.sub-link {
            padding-left: 2rem;
            font-size: 0.8125rem;
        }

        /* 主内容区域 */
        .main-content {
            min-width: 0;
        }

        .content-section {
            margin-bottom: var(--spacing-2xl);
            scroll-margin-top: 5rem;
        }

        /* 排版样式 */
        h1, h2, h3, h4, h5, h6 {
            font-weight: 600;
            line-height: 1.3;
            color: var(--color-gray-900);
            margin-top: 0;
        }

        h1 { font-size: 2.5rem; margin-bottom: var(--spacing-lg); }
        h2 { font-size: 2rem; margin-bottom: var(--spacing-md); margin-top: var(--spacing-xl); }
        h3 { font-size: 1.5rem; margin-bottom: var(--spacing-sm); margin-top: var(--spacing-lg); }
        h4 { font-size: 1.25rem; margin-bottom: var(--spacing-sm); margin-top: var(--spacing-md); }

        p {
            margin-bottom: var(--spacing-sm);
            color: var(--color-gray-700);
            line-height: 1.8;
        }

        /* 特色卡片 */
        .feature-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: var(--spacing-md);
            margin: var(--spacing-lg) 0;
        }

        .feature-card {
            background: white;
            border: 1px solid var(--color-gray-200);
            border-radius: var(--radius-lg);
            padding: var(--spacing-lg);
            transition: all 0.3s;
        }

        .feature-card:hover {
            border-color: var(--color-primary);
            box-shadow: var(--shadow-lg);
            transform: translateY(-2px);
        }

        .feature-icon {
            width: 48px;
            height: 48px;
            background: var(--color-primary);
            background: linear-gradient(135deg, var(--color-primary), var(--color-primary-light));
            border-radius: var(--radius-md);
            display: flex;
            align-items: center;
            justify-content: center;
            margin-bottom: var(--spacing-sm);
            color: white;
            font-size: 1.5rem;
        }

        .feature-title {
            font-size: 1.125rem;
            font-weight: 600;
            margin-bottom: var(--spacing-xs);
            color: var(--color-gray-900);
        }

        .feature-description {
            font-size: 0.875rem;
            color: var(--color-gray-600);
            line-height: 1.6;
        }

        /* 升级特性卡片 */
        .upgrade-card {
            background: linear-gradient(135deg, var(--color-primary), var(--color-primary-dark));
            color: white;
            padding: var(--spacing-lg);
            border-radius: var(--radius-lg);
            margin: var(--spacing-lg) 0;
        }

        .upgrade-card h3 {
            color: white;
            margin-bottom: var(--spacing-md);
        }

        .upgrade-list {
            list-style: none;
        }

        .upgrade-list li {
            display: flex;
            align-items: flex-start;
            gap: var(--spacing-sm);
            margin-bottom: var(--spacing-sm);
            color: rgba(255, 255, 255, 0.9);
            line-height: 1.6;
        }

        .upgrade-list li::before {
            content: '✓';
            display: flex;
            align-items: center;
            justify-content: center;
            width: 20px;
            height: 20px;
            background: rgba(255, 255, 255, 0.2);
            border-radius: 50%;
            flex-shrink: 0;
            font-size: 0.75rem;
            font-weight: 600;
            margin-top: 2px;
        }

        /* 表格样式 */
        .spec-table {
            width: 100%;
            border-collapse: collapse;
            margin: var(--spacing-lg) 0;
            background: white;
            border: 1px solid var(--color-gray-200);
            border-radius: var(--radius-lg);
            overflow: hidden;
        }

        .spec-table th {
            background: var(--color-gray-50);
            padding: var(--spacing-sm) var(--spacing-md);
            text-align: left;
            font-weight: 600;
            color: var(--color-gray-900);
            border-bottom: 1px solid var(--color-gray-200);
        }

        .spec-table td {
            padding: var(--spacing-sm) var(--spacing-md);
            border-bottom: 1px solid var(--color-gray-100);
        }

        .spec-table tr:last-child td {
            border-bottom: none;
        }

        .spec-table tr:hover {
            background: var(--color-gray-50);
        }

        .spec-table .highlight-row {
            background: #f0fdf4;
        }

        .spec-table .highlight-row td {
            color: var(--color-secondary);
            font-weight: 500;
        }

        /* 代码块样式 */
        .code-container {
            position: relative;
            margin: var(--spacing-md) 0;
        }

        .code-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            background: var(--color-gray-800);
            padding: var(--spacing-xs) var(--spacing-md);
            border-radius: var(--radius-lg) var(--radius-lg) 0 0;
        }

        .code-language {
            color: var(--color-gray-400);
            font-size: 0.75rem;
            font-weight: 500;
            text-transform: uppercase;
            letter-spacing: 0.05em;
        }

        .code-copy-btn {
            background: transparent;
            border: 1px solid var(--color-gray-600);
            color: var(--color-gray-400);
            padding: 0.25rem 0.75rem;
            border-radius: var(--radius-sm);
            font-size: 0.75rem;
            cursor: pointer;
            transition: all 0.2s;
        }

        .code-copy-btn:hover {
            background: var(--color-gray-700);
            color: white;
            border-color: var(--color-gray-500);
        }

        .code-copy-btn.copied {
            background: var(--color-secondary);
            color: white;
            border-color: var(--color-secondary);
        }

        .code-block {
            background: var(--color-gray-900);
            padding: var(--spacing-md);
            border-radius: 0 0 var(--radius-lg) var(--radius-lg);
            overflow-x: auto;
            margin: 0;
        }

        .code-block pre {
            margin: 0;
            font-family: var(--font-mono);
            font-size: 0.875rem;
            line-height: 1.6;
            color: #e5e7eb;
        }

        .code-block code {
            font-family: var(--font-mono);
        }

        /* 内联代码 */
        code:not(.code-block code) {
            background: var(--color-gray-100);
            color: var(--color-gray-800);
            padding: 0.125rem 0.375rem;
            border-radius: var(--radius-sm);
            font-family: var(--font-mono);
            font-size: 0.875em;
            font-weight: 500;
        }

        /* 比较卡片 */
        .comparison-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: var(--spacing-md);
            margin: var(--spacing-lg) 0;
        }

        .comparison-card {
            padding: var(--spacing-lg);
            border-radius: var(--radius-lg);
            position: relative;
            overflow: hidden;
        }

        .comparison-card.before {
            background: #fef2f2;
            border: 2px solid #fee2e2;
        }

        .comparison-card.after {
            background: #f0fdf4;
            border: 2px solid #dcfce7;
        }

        .comparison-badge {
            position: absolute;
            top: 0;
            left: 0;
            background: var(--color-danger);
            color: white;
            padding: 0.25rem 1rem;
            font-size: 0.75rem;
            font-weight: 600;
            text-transform: uppercase;
            letter-spacing: 0.05em;
        }

        .comparison-card.after .comparison-badge {
            background: var(--color-secondary);
        }

        .comparison-card h4 {
            margin-top: var(--spacing-md);
            margin-bottom: var(--spacing-sm);
            color: var(--color-gray-900);
        }

        /* 警告和提示框 */
        .alert {
            padding: var(--spacing-md);
            border-radius: var(--radius-lg);
            margin: var(--spacing-md) 0;
            display: flex;
            gap: var(--spacing-sm);
            align-items: flex-start;
        }

        .alert-icon {
            flex-shrink: 0;
            width: 20px;
            height: 20px;
            margin-top: 2px;
        }

        .alert-content {
            flex: 1;
        }

        .alert-info {
            background: #eff6ff;
            border: 1px solid #dbeafe;
            color: #1e40af;
        }

        .alert-warning {
            background: #fef3c7;
            border: 1px solid #fde68a;
            color: #92400e;
        }

        .alert-success {
            background: #f0fdf4;
            border: 1px solid #dcfce7;
            color: #166534;
        }

        /* 页脚 */
        .footer {
            background: var(--color-gray-900);
            color: var(--color-gray-400);
            padding: var(--spacing-2xl) 0;
            margin-top: var(--spacing-2xl);
        }

        .footer-content {
            display: grid;
            grid-template-columns: 2fr 1fr 1fr;
            gap: var(--spacing-xl);
        }

        .footer-section h4 {
            color: white;
            font-size: 1rem;
            margin-bottom: var(--spacing-sm);
        }

        .footer-section p {
            color: var(--color-gray-400);
            font-size: 0.875rem;
            line-height: 1.6;
        }

        .footer-links {
            display: flex;
            flex-direction: column;
            gap: var(--spacing-xs);
        }

        .footer-link {
            color: var(--color-gray-400);
            text-decoration: none;
            font-size: 0.875rem;
            transition: color 0.2s;
        }

        .footer-link:hover {
            color: white;
        }

        .footer-bottom {
            border-top: 1px solid var(--color-gray-800);
            margin-top: var(--spacing-xl);
            padding-top: var(--spacing-lg);
            text-align: center;
            font-size: 0.875rem;
        }

        /* 返回顶部按钮 */
        .back-to-top {
            position: fixed;
            bottom: 2rem;
            right: 2rem;
            width: 48px;
            height: 48px;
            background: var(--color-primary);
            color: white;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            text-decoration: none;
            opacity: 0;
            transform: translateY(10px);
            transition: all 0.3s;
            box-shadow: var(--shadow-lg);
            z-index: 100;
        }

        .back-to-top.visible {
            opacity: 1;
            transform: translateY(0);
        }

        .back-to-top:hover {
            background: var(--color-primary-dark);
            transform: translateY(-2px);
            box-shadow: var(--shadow-xl);
        }

        /* 动画 */
        @keyframes pulse {
            0%, 100% {
                opacity: 1;
            }
            50% {
                opacity: 0.5;
            }
        }

        @keyframes fadeInUp {
            from {
                opacity: 0;
                transform: translateY(20px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        .animate-fadeInUp {
            animation: fadeInUp 0.6s ease-out forwards;
        }

        /* 响应式设计 */
        @media (max-width: 1024px) {
            .main-layout {
                grid-template-columns: 1fr;
            }

            .sidebar {
                display: none;
            }

            .hero-title {
                font-size: 2.5rem;
            }

            .comparison-grid {
                grid-template-columns: 1fr;
            }

            .footer-content {
                grid-template-columns: 1fr;
                text-align: center;
            }
        }

        @media (max-width: 640px) {
            .navbar-nav {
                display: none;
            }

            .hero-title {
                font-size: 2rem;
            }

            .hero-subtitle {
                font-size: 1rem;
            }

            .hero-actions {
                flex-direction: column;
                width: 100%;
            }

            .btn-primary, .btn-secondary {
                width: 100%;
                justify-content: center;
            }

            .feature-grid {
                grid-template-columns: 1fr;
            }
        }

        /* 打印样式 */
        @media print {
            .navbar, .sidebar, .back-to-top, .hero-actions, .download-btn {
                display: none;
            }

            body {
                color: black;
                background: white;
            }

            .main-layout {
                grid-template-columns: 1fr;
            }

            .code-block {
                background: #f3f4f6;
                color: black;
                page-break-inside: avoid;
            }

            h1, h2, h3, h4 {
                page-break-after: avoid;
            }
        }

        /* 语法高亮 */
        .token-tag { color: #93c5fd; }
        .token-attr { color: #fbbf24; }
        .token-string { color: #86efac; }
        .token-comment { color: #6b7280; font-style: italic; }
    </style>
</head>
<body>
    <!-- 导航栏 -->
    <nav class="navbar" id="navbar">
        <div class="container">
            <div class="navbar-content">
                <a href="#" class="navbar-brand">
                    <div class="navbar-logo">HL</div>
                    <span class="navbar-title">HTMLLite 规范</span>
                    <span class="navbar-version">v1.2</span>
                </a>
                
                <div class="navbar-nav">
                    <a href="#overview" class="nav-link">概述</a>
                    <a href="#features" class="nav-link">特性</a>
                    <a href="#specification" class="nav-link">规范</a>
                    <a href="#examples" class="nav-link">示例</a>
                    <a href="#resources" class="nav-link">资源</a>
                    <a href="#" class="download-btn">
                        <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                            <path d="M21 15v4a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2v-4"/>
                            <polyline points="7 10 12 15 17 10"/>
                            <line x1="12" y1="15" x2="12" y2="3"/>
                        </svg>
                        下载规范
                    </a>
                </div>
            </div>
        </div>
    </nav>

    <!-- 主页头部 -->
    <header class="hero">
        <div class="container">
            <div class="hero-content">
                <div class="hero-badge">
                    <span class="hero-badge-dot"></span>
                    最新版本 v1.2 • 2025年7月29日发布
                </div>
                <h1 class="hero-title">HTMLLite 规范</h1>
                <p class="hero-subtitle">
                    为人工智能和大型语言模型设计的轻量级HTML子集<br>
                    让非结构化文档转化为AI可理解的高质量结构化数据
                </p>
                <div class="hero-actions">
                    <a href="#quick-start" class="btn-primary">
                        <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                            <polygon points="5 3 19 12 5 21 5 3"/>
                        </svg>
                        快速开始
                    </a>
                    <a href="https://github.com" class="btn-secondary">
                        <svg width="20" height="20" viewBox="0 0 24 24" fill="currentColor">
                            <path d="M12 0c-6.626 0-12 5.373-12 12 0 5.302 3.438 9.8 8.207 11.387.599.111.793-.261.793-.577v-2.234c-3.338.726-4.033-1.416-4.033-1.416-.546-1.387-1.333-1.756-1.333-1.756-1.089-.745.083-.729.083-.729 1.205.084 1.839 1.237 1.839 1.237 1.07 1.834 2.807 1.304 3.492.997.107-.775.418-1.305.762-1.604-2.665-.305-5.467-1.334-5.467-5.931 0-1.311.469-2.381 1.236-3.221-.124-.303-.535-1.524.117-3.176 0 0 1.008-.322 3.301 1.23.957-.266 1.983-.399 3.003-.404 1.02.005 2.047.138 3.006.404 2.291-1.552 3.297-1.23 3.297-1.23.653 1.653.242 2.874.118 3.176.77.84 1.235 1.911 1.235 3.221 0 4.609-2.807 5.624-5.479 5.921.43.372.823 1.102.823 2.222v3.293c0 .319.192.694.801.576 4.765-1.589 8.199-6.086 8.199-11.386 0-6.627-5.373-12-12-12z"/>
                        </svg>
                        查看 GitHub
                    </a>
                </div>
            </div>
        </div>
    </header>

    <!-- 主内容区域 -->
    <div class="container">
        <div class="main-layout">
            <!-- 侧边栏 -->
            <aside class="sidebar">
                <div class="sidebar-section">
                    <h4 class="sidebar-title">快速导航</h4>
                    <nav class="sidebar-nav">
                        <a href="#overview" class="sidebar-link active">概述</a>
                        <a href="#why-htmllite" class="sidebar-link">为什么需要 HTMLLite</a>
                        <a href="#upgrade" class="sidebar-link">v1.2 升级特性</a>
                        <a href="#principles" class="sidebar-link">设计原则</a>
                        <a href="#specification" class="sidebar-link">格式规范</a>
                        <a href="#elements" class="sidebar-link sub-link">允许的元素</a>
                        <a href="#structure" class="sidebar-link sub-link">文档结构</a>
                        <a href="#examples" class="sidebar-link">应用示例</a>
                        <a href="#dl-study" class="sidebar-link">DL标签深度研究</a>
                        <a href="#best-practices" class="sidebar-link">最佳实践</a>
                        <a href="#tools" class="sidebar-link">工具和资源</a>
                    </nav>
                </div>
                
                <div class="sidebar-section">
                    <h4 class="sidebar-title">相关资源</h4>
                    <nav class="sidebar-nav">
                        <a href="#" class="sidebar-link">API 文档</a>
                        <a href="#" class="sidebar-link">转换工具</a>
                        <a href="#" class="sidebar-link">验证器</a>
                        <a href="#" class="sidebar-link">社区论坛</a>
                    </nav>
                </div>
            </aside>

            <!-- 主内容 -->
            <main class="main-content">
                <!-- 概述部分 -->
                <section id="overview" class="content-section">
                    <h1>概述</h1>
                    
                    <div class="alert alert-info">
                        <svg class="alert-icon" viewBox="0 0 20 20" fill="currentColor">
                            <path fill-rule="evenodd" d="M18 10a8 8 0 11-16 0 8 8 0 0116 0zm-7-4a1 1 0 11-2 0 1 1 0 012 0zM9 9a1 1 0 000 2v3a1 1 0 001 1h1a1 1 0 100-2v-3a1 1 0 00-1-1H9z" clip-rule="evenodd"/>
                        </svg>
                        <div class="alert-content">
                            <strong>核心理念：</strong>HTMLLite 专注于内容本身，剥离所有表现层元素，为AI提供清晰、无歧义的结构化数据。
                        </div>
                    </div>

                    <p>
                        HTMLLite 是一种为人工智能（AI）和大型语言模型（LLM）设计的、严格的HTML轻量级子集。它旨在将人类编写的复杂文档，转化为机器可以无歧义地解析、理解和推理的高质量结构化数据。
                    </p>

                    <p>
                        通过剥离标准HTML中所有与表现层（样式、脚本）相关的元素，并增强其描述内容结构与关联的能力，HTMLLite 解决了非结构化数据在AI应用中的三个核心痛点：
                    </p>

                    <div class="feature-grid">
                        <div class="feature-card">
                            <div class="feature-icon">📊</div>
                            <h3 class="feature-title">上下文完整</h3>
                            <p class="feature-description">确保每个知识区块都包含完整的上下文信息，避免信息碎片化。</p>
                        </div>
                        <div class="feature-card">
                            <div class="feature-icon">🔗</div>
                            <h3 class="feature-title">结构清晰</h3>
                            <p class="feature-description">使用严格的标签集合，消除结构歧义，提供清晰的文档层级。</p>
                        </div>
                        <div class="feature-card">
                            <div class="feature-icon">🤖</div>
                            <h3 class="feature-title">关系明确</h3>
                            <p class="feature-description">通过语义链接机制，让AI理解不同内容块之间的逻辑关系。</p>
                        </div>
                    </div>
                </section>

                <!-- v1.2 升级特性 -->
                <section id="upgrade" class="content-section">
                    <h2>v1.2 升级亮点</h2>
                    
                    <div class="upgrade-card">
                        <h3>🚀 本次升级的核心改进</h3>
                        <ul class="upgrade-list">
                            <li><strong>[新增]</strong> 在"允许的内容元素"中正式加入了定义列表 (<code>&lt;dl&gt;</code>, <code>&lt;dt&gt;</code>, <code>&lt;dd&gt;</code>) 元素</li>
                            <li><strong>[推荐]</strong> 明确推荐使用定义列表作为表示键值对数据的最佳实践</li>
                            <li><strong>[澄清]</strong> 再次强调了 <code>&lt;strong&gt;</code> 和 <code>&lt;em&gt;</code> 标签作为可选的语义强调元素</li>
                        </ul>
                        <p style="margin-top: 1rem; color: rgba(255,255,255,0.9);">
                            这次升级的核心是通过引入定义列表（Description List）元素，极大地增强了HTMLLite对键值对（Key-Value）数据的语义表示能力。
                        </p>
                    </div>
                </section>

                <!-- 设计原则 -->
                <section id="principles" class="content-section">
                    <h2>设计原则</h2>
                    
                    <div class="feature-grid">
                        <div class="feature-card">
                            <div class="feature-icon">⚡</div>
                            <h3 class="feature-title">轻量纯粹</h3>
                            <p class="feature-description">只包含用于定义内容结构的HTML标签，剔除所有表现层元素。</p>
                        </div>
                        <div class="feature-card">
                            <div class="feature-icon">🎯</div>
                            <h3 class="feature-title">结构保真</h3>
                            <p class="feature-description">无损保留原始文档的关键结构，特别是表格、列表和多级标题。</p>
                        </div>
                        <div class="feature-card">
                            <div class="feature-icon">🧩</div>
                            <h3 class="feature-title">原子化区块</h3>
                            <p class="feature-description">将文档拆分为独立的、上下文完整的"知识区块"。</p>
                        </div>
                        <div class="feature-card">
                            <div class="feature-icon">🔗</div>
                            <h3 class="feature-title">语义链接</h3>
                            <p class="feature-description">提供结构化的链接机制，使机器能够理解区块之间的逻辑关系。</p>
                        </div>
                        <div class="feature-card">
                            <div class="feature-icon">💎</div>
                            <h3 class="feature-title">精确语义</h3>
                            <p class="feature-description">鼓励使用最能准确描述数据内在关系的HTML标签。</p>
                        </div>
                        <div class="feature-card">
                            <div class="feature-icon">🚀</div>
                            <h3 class="feature-title">AI优先</h3>
                            <p class="feature-description">每个设计决策都以提升AI理解能力为首要目标。</p>
                        </div>
                    </div>
                </section>

                <!-- 格式规范 -->
                <section id="specification" class="content-section">
                    <h2>格式规范</h2>
                    
                    <h3 id="structure">文档结构</h3>
                    
                    <h4>根容器</h4>
                    <p>所有 HTMLLite 内容必须被包含在一个唯一的根 <code>&lt;div&gt;</code> 容器内，并使用 <code>class="htmllite-document"</code> 进行标识。</p>
                    
                    <div class="code-container">
                        <div class="code-header">
                            <span class="code-language">HTML</span>
                            <button class="code-copy-btn" onclick="copyCode(this)">复制</button>
                        </div>
                        <div class="code-block">
                            <pre><code><span class="token-tag">&lt;div</span> <span class="token-attr">class</span>=<span class="token-string">"htmllite-document"</span><span class="token-tag">&gt;</span>
    <span class="token-comment">&lt;!-- 所有内容都在这里 --&gt;</span>
<span class="token-tag">&lt;/div&gt;</span></code></pre>
                        </div>
                    </div>

                    <h4>知识区块</h4>
                    <p>一个知识区块由一个带有 <code>data-htmllite-block="true"</code> 属性的 <code>&lt;div&gt;</code> 元素定义。区块之间不可嵌套，并应以标题开始。</p>

                    <div class="code-container">
                        <div class="code-header">
                            <span class="code-language">HTML</span>
                            <button class="code-copy-btn" onclick="copyCode(this)">复制</button>
                        </div>
                        <div class="code-block">
                            <pre><code><span class="token-tag">&lt;div</span> <span class="token-attr">data-htmllite-block</span>=<span class="token-string">"true"</span><span class="token-tag">&gt;</span>
    <span class="token-tag">&lt;h2&gt;</span>区块标题<span class="token-tag">&lt;/h2&gt;</span>
    <span class="token-comment">&lt;!-- 区块内容 --&gt;</span>
<span class="token-tag">&lt;/div&gt;</span></code></pre>
                        </div>
                    </div>

                    <h3 id="elements">允许的内容元素</h3>
                    <p>在每个 <code>data-htmllite-block</code> 内部，只允许使用以下HTML标签：</p>
                    
                    <table class="spec-table">
                        <thead>
                            <tr>
                                <th style="width: 30%">元素</th>
                                <th style="width: 50%">用途</th>
                                <th style="width: 20%">备注</th>
                            </tr>
                        </thead>
                        <tbody>
                            <tr>
                                <td><code>&lt;h2&gt;</code> - <code>&lt;h6&gt;</code></td>
                                <td>标题：定义区块内的主题和子主题层级</td>
                                <td>必需</td>
                            </tr>
                            <tr>
                                <td><code>&lt;p&gt;</code></td>
                                <td>段落：包含常规文本内容</td>
                                <td>-</td>
                            </tr>
                            <tr>
                                <td><code>&lt;ul&gt;</code>, <code>&lt;ol&gt;</code>, <code>&lt;li&gt;</code></td>
                                <td>列表：用于表示项目列表或有序步骤</td>
                                <td>-</td>
                            </tr>
                            <tr>
                                <td><code>&lt;table&gt;</code>, <code>&lt;thead&gt;</code>, <code>&lt;tbody&gt;</code>, <code>&lt;tr&gt;</code>, <code>&lt;th&gt;</code>, <code>&lt;td&gt;</code></td>
                                <td>表格：用于结构化数据展示</td>
                                <td>保留 rowspan 和 colspan</td>
                            </tr>
                            <tr class="highlight-row">
                                <td><strong><code>&lt;dl&gt;</code>, <code>&lt;dt&gt;</code>, <code>&lt;dd&gt;</code></strong></td>
                                <td><strong>定义列表：用于表示键值对数据</strong></td>
                                <td><strong>v1.2 新增</strong></td>
                            </tr>
                            <tr>
                                <td><code>&lt;sup&gt;</code>, <code>&lt;sub&gt;</code></td>
                                <td>上/下标：用于脚注标记、化学式等</td>
                                <td>-</td>
                            </tr>
                            <tr>
                                <td><code>&lt;strong&gt;</code>, <code>&lt;em&gt;</code></td>
                                <td>强调：用于标记重点词汇</td>
                                <td>可选，语义强调</td>
                            </tr>
                            <tr>
                                <td><code>&lt;br&gt;</code></td>
                                <td>换行：在段落内强制换行</td>
                                <td>-</td>
                            </tr>
                        </tbody>
                    </table>

                    <h4>关联链接</h4>
                    <p>一个关联链接由 <code>data-htmllite-link="true"</code> 的 <code>&lt;div&gt;</code> 定义，包含 <code>data-href</code> 属性和描述子元素。</p>

                    <div class="code-container">
                        <div class="code-header">
                            <span class="code-language">HTML</span>
                            <button class="code-copy-btn" onclick="copyCode(this)">复制</button>
                        </div>
                        <div class="code-block">
                            <pre><code><span class="token-tag">&lt;div</span> <span class="token-attr">data-htmllite-link</span>=<span class="token-string">"true"</span> <span class="token-attr">data-href</span>=<span class="token-string">"/path/to/resource.htmllite"</span><span class="token-tag">&gt;</span>
    <span class="token-tag">&lt;strong</span> <span class="token-attr">class</span>=<span class="token-string">"htmllite-link-title"</span><span class="token-tag">&gt;</span>相关资料标题<span class="token-tag">&lt;/strong&gt;</span>
    <span class="token-tag">&lt;p</span> <span class="token-attr">class</span>=<span class="token-string">"htmllite-link-description"</span><span class="token-tag">&gt;</span>
        资料的简要描述...
    <span class="token-tag">&lt;/p&gt;</span>
<span class="token-tag">&lt;/div&gt;</span></code></pre>
                        </div>
                    </div>

                    <div class="alert alert-warning">
                        <svg class="alert-icon" viewBox="0 0 20 20" fill="currentColor">
                            <path fill-rule="evenodd" d="M8.257 3.099c.765-1.36 2.722-1.36 3.486 0l5.58 9.92c.75 1.334-.213 2.98-1.742 2.98H4.42c-1.53 0-2.493-1.646-1.743-2.98l5.58-9.92zM11 13a1 1 0 11-2 0 1 1 0 012 0zm-1-8a1 1 0 00-1 1v3a1 1 0 002 0V6a1 1 0 00-1-1z" clip-rule="evenodd"/>
                        </svg>
                        <div class="alert-content">
                            <strong>禁止的元素：</strong>严禁使用任何与内容结构无关的标签，如 <code>&lt;style&gt;</code>, <code>&lt;script&gt;</code>, <code>&lt;link&gt;</code>, <code>&lt;iframe&gt;</code>, <code>&lt;span&gt;</code> (在区块内), <code>&lt;form&gt;</code> 等。
                        </div>
                    </div>
                </section>

                <!-- 应用示例 -->
                <section id="examples" class="content-section">
                    <h2>应用 v1.2 规范的示例</h2>
                    <p>现在，我们使用 HTMLLite v1.2 规范来转换数据，正式采用 <code>&lt;dl&gt;</code> 标签作为最佳实践：</p>

                    <div class="code-container">
                        <div class="code-header">
                            <span class="code-language">HTML</span>
                            <button class="code-copy-btn" onclick="copyCode(this)">复制</button>
                        </div>
                        <div class="code-block">
                            <pre><code><span class="token-tag">&lt;div</span> <span class="token-attr">class</span>=<span class="token-string">"htmllite-document"</span><span class="token-tag">&gt;</span>
    <span class="token-tag">&lt;div</span> <span class="token-attr">data-htmllite-block</span>=<span class="token-string">"true"</span><span class="token-tag">&gt;</span>
        <span class="token-tag">&lt;h2&gt;</span>144: 南四湖以东水源涵养、生物多样性维护生态保护红线区<span class="token-tag">&lt;/h2&gt;</span>
        
        <span class="token-tag">&lt;dl&gt;</span>
            <span class="token-tag">&lt;dt&gt;</span>代码<span class="token-tag">&lt;/dt&gt;</span>
            <span class="token-tag">&lt;dd&gt;</span>SD-04-B1-01<span class="token-tag">&lt;/dd&gt;</span>
            
            <span class="token-tag">&lt;dt&gt;</span>生态功能<span class="token-tag">&lt;/dt&gt;</span>
            <span class="token-tag">&lt;dd&gt;</span>水源涵养、生物多样性维护<span class="token-tag">&lt;/dd&gt;</span>

            <span class="token-tag">&lt;dt&gt;</span>类型<span class="token-tag">&lt;/dt&gt;</span>
            <span class="token-tag">&lt;dd&gt;</span>湿地、湖泊、农田<span class="token-tag">&lt;/dd&gt;</span>
        <span class="token-tag">&lt;/dl&gt;</span>
        
        <span class="token-tag">&lt;h3&gt;</span>所在行政区域<span class="token-tag">&lt;/h3&gt;</span>
        <span class="token-tag">&lt;dl&gt;</span>
            <span class="token-tag">&lt;dt&gt;</span>市<span class="token-tag">&lt;/dt&gt;</span>
            <span class="token-tag">&lt;dd&gt;</span>枣庄市<span class="token-tag">&lt;/dd&gt;</span>
            <span class="token-tag">&lt;dt&gt;</span>县(区、市)<span class="token-tag">&lt;/dt&gt;</span>
            <span class="token-tag">&lt;dd&gt;</span>滕州市<span class="token-tag">&lt;/dd&gt;</span>
        <span class="token-tag">&lt;/dl&gt;</span>
        
        <span class="token-tag">&lt;h3&gt;</span>外边界<span class="token-tag">&lt;/h3&gt;</span>
        <span class="token-tag">&lt;dl&gt;</span>
            <span class="token-tag">&lt;dt&gt;</span>面积(km²)<span class="token-tag">&lt;/dt&gt;</span>
            <span class="token-tag">&lt;dd&gt;</span>53.69<span class="token-tag">&lt;/dd&gt;</span>
            <span class="token-tag">&lt;dt&gt;</span>边界描述<span class="token-tag">&lt;/dt&gt;</span>
            <span class="token-tag">&lt;dd&gt;</span>滕州市西部的滨湖镇境内。<span class="token-tag">&lt;/dd&gt;</span>
            <span class="token-tag">&lt;dt&gt;</span>拐点坐标<span class="token-tag">&lt;/dt&gt;</span>
            <span class="token-tag">&lt;dd&gt;</span>1:116 51'04"E, 35 06'01"N; 2:116 °50'50"E, 35 °05'01"N; ...<span class="token-tag">&lt;/dd&gt;</span>
        <span class="token-tag">&lt;/dl&gt;</span>

        <span class="token-tag">&lt;h3&gt;</span>I类红线区<span class="token-tag">&lt;/h3&gt;</span>
        <span class="token-tag">&lt;dl&gt;</span>
            <span class="token-tag">&lt;dt&gt;</span>面积(km²)<span class="token-tag">&lt;/dt&gt;</span>
            <span class="token-tag">&lt;dd&gt;</span>N/A<span class="token-tag">&lt;/dd&gt;</span>
            <span class="token-tag">&lt;dt&gt;</span>边界描述<span class="token-tag">&lt;/dt&gt;</span>
            <span class="token-tag">&lt;dd&gt;</span>/<span class="token-tag">&lt;/dd&gt;</span>
            <span class="token-tag">&lt;dt&gt;</span>拐点坐标<span class="token-tag">&lt;/dt&gt;</span>
            <span class="token-tag">&lt;dd&gt;</span>/<span class="token-tag">&lt;/dd&gt;</span>
        <span class="token-tag">&lt;/dl&gt;</span>
        
        <span class="token-tag">&lt;h3&gt;</span>备注与关联<span class="token-tag">&lt;/h3&gt;</span>
        <span class="token-tag">&lt;p&gt;</span>此区域包含滕州红荷湿地省级地质公园、滕州滨湖国家湿地公园、部分滕州市公益林。<span class="token-tag">&lt;/p&gt;</span>
        
        <span class="token-tag">&lt;div</span> <span class="token-attr">data-htmllite-link</span>=<span class="token-string">"true"</span> <span class="token-attr">data-href</span>=<span class="token-string">"/parks/tengzhou-red-lotus-geopark.htmllite"</span><span class="token-tag">&gt;</span>
            <span class="token-tag">&lt;strong</span> <span class="token-attr">class</span>=<span class="token-string">"htmllite-link-title"</span><span class="token-tag">&gt;</span>相关资料：滕州红荷湿地省级地质公园<span class="token-tag">&lt;/strong&gt;</span>
            <span class="token-tag">&lt;p</span> <span class="token-attr">class</span>=<span class="token-string">"htmllite-link-description"</span><span class="token-tag">&gt;</span>
                查看关于"滕州红荷湿地省级地质公园"的详细信息，包括其具体范围、保护目标和管理规定。
            <span class="token-tag">&lt;/p&gt;</span>
        <span class="token-tag">&lt;/div&gt;</span>
    <span class="token-tag">&lt;/div&gt;</span>
<span class="token-tag">&lt;/div&gt;</span></code></pre>
                        </div>
                    </div>

                    <div class="alert alert-success">
                        <svg class="alert-icon" viewBox="0 0 20 20" fill="currentColor">
                            <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm3.707-9.293a1 1 0 00-1.414-1.414L9 10.586 7.707 9.293a1 1 0 00-1.414 1.414l2 2a1 1 0 001.414 0l4-4z" clip-rule="evenodd"/>
                        </svg>
                        <div class="alert-content">
                            <h4 style="margin-top: 0;">v1.2 升级的价值</h4>
                            <ul style="margin: 0.5rem 0 0 1.5rem; line-height: 1.8;">
                                <li><strong>对机器更友好：</strong><code>&lt;dl&gt;</code> 列表为AI提供了关于"键"和"值"关系的强信号</li>
                                <li><strong>语义更精确：</strong>准确反映了原始JSON数据的内在结构</li>
                                <li><strong>结构更清晰：</strong>使得键值对的层级关系一目了然</li>
                            </ul>
                        </div>
                    </div>
                </section>

                <!-- DL标签深度研究 -->
                <section id="dl-study" class="content-section">
                    <h2>DL、DT、DD 标签深度研究</h2>
                    <p>定义列表（Description List）是一个强大但经常被低估的HTML工具，让我们深入了解它的结构和用法。</p>

                    <h3>什么是定义列表？</h3>
                    <p>定义列表是一种用于展示"名/值"对（或"术语/描述"对）的HTML结构。它天生包含两个层次：</p>
                    
                    <ol style="margin: 1rem 0 1rem 2rem;">
                        <li><strong>术语/名称 (Term)：</strong>你想要定义或描述的主体</li>
                        <li><strong>描述/值 (Description)：</strong>对该术语的具体解释或其对应的值</li>
                    </ol>

                    <h3>三个核心标签详解</h3>
                    <div class="feature-grid">
                        <div class="feature-card">
                            <div class="tag-name" style="margin-bottom: 1rem;">&lt;dl&gt;</div>
                            <h4>Description List - 定义列表</h4>
                            <p><strong>含义：</strong>"定义列表"的缩写</p>
                            <p><strong>角色：</strong>容器标签，包裹整个名值对列表</p>
                            <p><strong>类比：</strong>如果把整个列表看作字典，<code>&lt;dl&gt;</code> 就是这本字典本身</p>
                        </div>
                        
                        <div class="feature-card">
                            <div class="tag-name" style="margin-bottom: 1rem;">&lt;dt&gt;</div>
                            <h4>Definition Term - 定义术语</h4>
                            <p><strong>含义：</strong>"定义术语"的缩写</p>
                            <p><strong>角色：</strong>名称/键 (Name/Key) 标签</p>
                            <p><strong>类比：</strong>在字典里，<code>&lt;dt&gt;</code> 就是要查的词条</p>
                        </div>
                        
                        <div class="feature-card">
                            <div class="tag-name" style="margin-bottom: 1rem;">&lt;dd&gt;</div>
                            <h4>Definition Description - 定义描述</h4>
                            <p><strong>含义：</strong>"定义描述"的缩写</p>
                            <p><strong>角色：</strong>描述/值 (Description/Value) 标签</p>
                            <p><strong>类比：</strong>在字典里，<code>&lt;dd&gt;</code> 就是词条的解释</p>
                        </div>
                    </div>

                    <h3>为什么在 HTMLLite 中使用它如此重要？</h3>
                    <p>在 HTMLLite 的语境下，使用 <code>&lt;dl&gt;</code> 远比使用 <code>&lt;p&gt;</code> 或 <code>&lt;strong&gt;</code> 更好，原因在于其无与伦比的语义精确性。</p>

                    <div class="comparison-grid">
                        <div class="comparison-card before">
                            <span class="comparison-badge">不推荐</span>
                            <h4>使用 &lt;p&gt; 标签</h4>
                            <div class="code-container">
                                <div class="code-block" style="background: #f9fafb; color: #1f2937;">
                                    <pre><code>&lt;p&gt;代码: SD-04-B1-01&lt;/p&gt;</code></pre>
                                </div>
                            </div>
                            <p><strong>机器的理解：</strong>"这是一个段落，内容是'代码: SD-04-B1-01'。"</p>
                            <p>机器需要通过NLP识别冒号，并猜测"代码"是键，"SD-04-B1-01"是值。这个过程可能出错，且计算成本更高。</p>
                        </div>
                        
                        <div class="comparison-card after">
                            <span class="comparison-badge">推荐</span>
                            <h4>使用 &lt;dl&gt; 标签</h4>
                            <div class="code-container">
                                <div class="code-block" style="background: #f0fdf4; color: #166534;">
                                    <pre><code>&lt;dl&gt;
  &lt;dt&gt;代码&lt;/dt&gt;
  &lt;dd&gt;SD-04-B1-01&lt;/dd&gt;
&lt;/dl&gt;</code></pre>
                                </div>
                            </div>
                            <p><strong>机器的理解：</strong>"这是一个定义列表。术语是'代码'，描述是'SD-04-B1-01'。"</p>
                            <p>这种结构化的关系是明确的、无歧义的。AI可以直接抓取内容，无需猜测。</p>
                        </div>
                    </div>
                </section>

                <!-- 最佳实践 -->
                <section id="best-practices" class="content-section">
                    <h2>最佳实践</h2>
                    
                    <div class="feature-grid">
                        <div class="feature-card">
                            <div class="feature-icon">📝</div>
                            <h3 class="feature-title">保持简洁</h3>
                            <p class="feature-description">每个知识区块应该聚焦于单一主题，避免内容过于庞大。</p>
                        </div>
                        <div class="feature-card">
                            <div class="feature-icon">🏷️</div>
                            <h3 class="feature-title">使用语义标签</h3>
                            <p class="feature-description">优先使用最能准确描述内容关系的标签，如键值对使用 <code>&lt;dl&gt;</code>。</p>
                        </div>
                        <div class="feature-card">
                            <div class="feature-icon">🔗</div>
                            <h3 class="feature-title">建立链接</h3>
                            <p class="feature-description">通过关联链接建立知识区块之间的关系网络。</p>
                        </div>
                        <div class="feature-card">
                            <div class="feature-icon">✅</div>
                            <h3 class="feature-title">验证结构</h3>
                            <p class="feature-description">使用验证工具确保文档符合 HTMLLite 规范。</p>
                        </div>
                        <div class="feature-card">
                            <div class="feature-icon">📊</div>
                            <h3 class="feature-title">保留元数据</h3>
                            <p class="feature-description">保留对AI理解有帮助的关键元数据信息。</p>
                        </div>
                        <div class="feature-card">
                            <div class="feature-icon">🎯</div>
                            <h3 class="feature-title">目标明确</h3>
                            <p class="feature-description">始终以提升AI理解能力为首要目标进行文档设计。</p>
                        </div>
                    </div>
                </section>
            </main>
        </div>
    </div>

    <!-- 页脚 -->
    <footer class="footer">
        <div class="container">
            <div class="footer-content">
                <div class="footer-section">
                    <h4>关于 HTMLLite</h4>
                    <p>HTMLLite 是为AI时代设计的下一代文档格式，专注于为人工智能和大型语言模型提供清晰、结构化的数据输入。</p>
                    <p style="margin-top: 1rem;">加入我们，共同构建AI友好的知识体系。</p>
                </div>
                <div class="footer-section">
                    <h4>快速链接</h4>
                    <div class="footer-links">
                        <a href="#" class="footer-link">规范文档</a>
                        <a href="#" class="footer-link">API 参考</a>
                        <a href="#" class="footer-link">转换工具</a>
                        <a href="#" class="footer-link">示例库</a>
                        <a href="#" class="footer-link">社区论坛</a>
                    </div>
                </div>
                <div class="footer-section">
                    <h4>资源</h4>
                    <div class="footer-links">
                        <a href="#" class="footer-link">GitHub</a>
                        <a href="#" class="footer-link">NPM Package</a>
                        <a href="#" class="footer-link">VS Code 插件</a>
                        <a href="#" class="footer-link">贡献指南</a>
                        <a href="#" class="footer-link">更新日志</a>
                    </div>
                </div>
            </div>
            <div class="footer-bottom">
                <p>&copy; 2025 HTMLLite 规范 v1.2. 专为构建企业知识库、RAG系统和AI Agent而设计。</p>
            </div>
        </div>
    </footer>

    <!-- 返回顶部按钮 -->
    <a href="#" class="back-to-top" id="backToTop">
        <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
            <polyline points="18 15 12 9 6 15"></polyline>
        </svg>
    </a>

    <script>
        // 导航栏滚动效果
        const navbar = document.getElementById('navbar');
        const backToTop = document.getElementById('backToTop');
        
        window.addEventListener('scroll', () => {
            if (window.scrollY > 50) {
                navbar.classList.add('scrolled');
            } else {
                navbar.classList.remove('scrolled');
            }
            
            if (window.scrollY > 300) {
                backToTop.classList.add('visible');
            } else {
                backToTop.classList.remove('visible');
            }
        });

        // 平滑滚动
        document.querySelectorAll('a[href^="#"]').forEach(anchor => {
            anchor.addEventListener('click', function (e) {
                e.preventDefault();
                const target = document.querySelector(this.getAttribute('href'));
                if (target) {
                    target.scrollIntoView({
                        behavior: 'smooth',
                        block: 'start'
                    });
                }
            });
        });

        // 侧边栏高亮当前章节
        const sections = document.querySelectorAll('.content-section');
        const sidebarLinks = document.querySelectorAll('.sidebar-link');
        
        function highlightSidebarLink() {
            const scrollPosition = window.scrollY + 100;
            
            sections.forEach((section, index) => {
                const sectionTop = section.offsetTop;
                const sectionBottom = sectionTop + section.offsetHeight;
                
                if (scrollPosition >= sectionTop && scrollPosition < sectionBottom) {
                    sidebarLinks.forEach(link => link.classList.remove('active'));
                    const activeLink = document.querySelector(`.sidebar-link[href="#${section.id}"]`);
                    if (activeLink) activeLink.classList.add('active');
                }
            });
        }
        
        window.addEventListener('scroll', highlightSidebarLink);
        highlightSidebarLink();

        // 代码复制功能
        function copyCode(button) {
            const codeBlock = button.parentElement.nextElementSibling.querySelector('code');
            const textArea = document.createElement('textarea');
            textArea.value = codeBlock.textContent;
            document.body.appendChild(textArea);
            textArea.select();
            document.execCommand('copy');
            document.body.removeChild(textArea);
            
            button.textContent = '已复制';
            button.classList.add('copied');
            
            setTimeout(() => {
                button.textContent = '复制';
                button.classList.remove('copied');
            }, 2000);
        }

        // 添加页面加载动画
        document.addEventListener('DOMContentLoaded', () => {
            const elements = document.querySelectorAll('.content-section, .feature-card');
            
            const observer = new IntersectionObserver((entries) => {
                entries.forEach(entry => {
                    if (entry.isIntersecting) {
                        entry.target.classList.add('animate-fadeInUp');
                    }
                });
            }, {
                threshold: 0.1,
                rootMargin: '0px 0px -50px 0px'
            });
            
            elements.forEach(element => {
                observer.observe(element);
            });
        });

        // 导航栏活动链接
        const navLinks = document.querySelectorAll('.nav-link');
        
        function updateNavLinks() {
            const scrollPosition = window.scrollY + 100;
            
            sections.forEach(section => {
                const sectionTop = section.offsetTop;
                const sectionBottom = sectionTop + section.offsetHeight;
                
                if (scrollPosition >= sectionTop && scrollPosition < sectionBottom) {
                    navLinks.forEach(link => link.classList.remove('active'));
                    const activeNavLink = document.querySelector(`.nav-link[href="#${section.id}"]`);
                    if (activeNavLink) activeNavLink.classList.add('active');
                }
            });
        }
        
        window.addEventListener('scroll', updateNavLinks);
        updateNavLinks();
    </script>
</body>
</html>
