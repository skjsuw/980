<html lang="zh-CN">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=yes, viewport-fit=cover">
<title>量化迁移 · 安全声明</title>

<style>
    * {
        margin: 0;
        padding: 0;
        box-sizing: border-box;
    }

    body {
        margin: 0;
        font-family: "Inter", "SF Pro Text", "PingFang SC", "Microsoft YaHei", system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Helvetica, Arial, sans-serif;
        background: radial-gradient(ellipse at 30% 20%, #0c1124, #03060f);
        color: #f0f4fe;
        min-height: 100vh;
        display: flex;
        align-items: center;
        justify-content: center;
        overflow-x: hidden;
        padding: 20px 16px;
    }

    /* 容器——手机宽度舒适，内边距充足 */
    .container {
        width: 100%;
        max-width: 600px;
        background: rgba(12, 20, 34, 0.78);
        backdrop-filter: blur(24px);
        border: 1px solid rgba(255, 255, 255, 0.12);
        border-radius: 2rem;
        padding: 2rem 1.5rem 2rem;
        text-align: center;
        box-shadow: 0 30px 50px -20px rgba(0, 0, 0, 0.6), 0 0 0 0.5px rgba(255, 255, 255, 0.05) inset;
        max-height: 96vh;
        overflow-y: auto;
        scrollbar-width: thin;
    }

    .container::-webkit-scrollbar {
        width: 4px;
        background: rgba(255,255,255,0.05);
    }
    .container::-webkit-scrollbar-thumb {
        background: #38bdf8aa;
        border-radius: 12px;
    }

    /* 标签字体清晰加大 */
    .tag {
        display: inline-flex;
        align-items: center;
        gap: 8px;
        padding: 8px 18px;
        background: rgba(56, 189, 248, 0.14);
        backdrop-filter: blur(8px);
        color: #c2e2ff;
        border-radius: 60px;
        font-size: 0.8rem;
        font-weight: 600;
        letter-spacing: 0.04em;
        margin-bottom: 1.4rem;
        border: 0.5px solid rgba(56, 189, 248, 0.4);
        text-transform: uppercase;
    }

    /* 标题超大清晰 */
    .title {
        font-size: 2rem;
        font-weight: 750;
        background: linear-gradient(125deg, #FFFFFF, #cae3ff);
        background-clip: text;
        -webkit-background-clip: text;
        color: transparent;
        margin-bottom: 0.75rem;
        letter-spacing: -0.2px;
        line-height: 1.35;
    }

    /* 描述字体加大行高 */
    .desc {
        font-size: 1rem;
        line-height: 1.6;
        color: #e2ecff;
        max-width: 100%;
        margin: 0 auto 14px auto;
        font-weight: 480;
        opacity: 0.95;
    }

    .domain-section {
        margin: 24px 0 16px;
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        width: 100%;
    }

    /* 域名区域 - 大号字体，高对比 */
    .site {
        width: 100%;
        font-size: 1.6rem;
        font-weight: 620;
        color: #aaf0ff;
        background: rgba(0, 20, 45, 0.7);
        padding: 16px 12px;
        border-radius: 1.5rem;
        border: 1px solid rgba(56, 189, 248, 0.65);
        word-break: break-all;
        user-select: all;
        font-family: 'SF Mono', 'Fira Code', monospace;
        letter-spacing: 0.4px;
        cursor: pointer;
        transition: all 0.2s ease;
        margin-bottom: 20px;
        text-align: center;
        backdrop-filter: blur(4px);
        box-shadow: 0 8px 18px rgba(0, 0, 0, 0.3);
    }

    .site:active {
        background: rgba(56, 189, 248, 0.2);
        transform: scale(0.98);
        border-color: #6bc8ff;
    }

    /* 按钮清晰易点 */
    .btn-copy {
        display: inline-flex;
        align-items: center;
        justify-content: center;
        gap: 12px;
        padding: 14px 32px;
        background: linear-gradient(105deg, #2c7be0, #1a4f96);
        color: #ffffff;
        border-radius: 80px;
        font-weight: 650;
        font-size: 1.1rem;
        cursor: pointer;
        user-select: none;
        transition: all 0.2s;
        border: 0.5px solid rgba(255, 255, 255, 0.3);
        box-shadow: 0 12px 22px -10px rgba(0, 40, 80, 0.5);
        margin-bottom: 12px;
        text-align: center;
        min-width: 220px;
        letter-spacing: 0.4px;
    }

    .btn-copy:active {
        transform: scale(0.97);
        background: linear-gradient(105deg, #1e56a0, #133e70);
    }

    /* 状态标 - 清晰圆润 */
    .status {
        margin-top: 16px;
        display: inline-flex;
        align-items: center;
        justify-content: center;
        gap: 12px;
        background: rgba(46, 204, 113, 0.1);
        backdrop-filter: blur(8px);
        padding: 8px 24px;
        border-radius: 60px;
        font-size: 0.85rem;
        font-weight: 600;
        color: #caf5df;
        border: 0.5px solid rgba(46, 204, 113, 0.35);
    }

    .dot {
        display: inline-block;
        width: 11px;
        height: 11px;
        background: #2ecc71;
        border-radius: 50%;
        box-shadow: 0 0 8px #2ecc71;
        animation: pulse 1.2s infinite;
    }

    @keyframes pulse {
        0% { transform: scale(0.95); opacity: 0.7; box-shadow: 0 0 0 0 rgba(46, 204, 113, 0.5);}
        50% { transform: scale(1.2); opacity: 1; box-shadow: 0 0 0 6px rgba(46, 204, 113, 0);}
        100% { transform: scale(0.95); opacity: 0.7; box-shadow: 0 0 0 0 rgba(46, 204, 113, 0);}
    }

    /* 安全声明卡片 - 充足留白，大字号 */
    .security-card {
        background: rgba(6, 16, 28, 0.8);
        backdrop-filter: blur(12px);
        border-radius: 2rem;
        padding: 1.5rem 1.5rem;
        margin-top: 28px;
        margin-bottom: 12px;
        text-align: left;
        border: 1px solid rgba(56, 189, 248, 0.3);
        box-shadow: 0 14px 28px -12px rgba(0, 0, 0, 0.5);
    }

    .security-title {
        font-weight: 720;
        font-size: 1.1rem;
        color: #cae6ff;
        display: flex;
        align-items: center;
        gap: 12px;
        margin-bottom: 16px;
        border-left: 4px solid #38bdf8;
        padding-left: 16px;
        letter-spacing: -0.2px;
    }

    .security-quote {
        font-size: 1rem;
        line-height: 1.65;
        color: #f2f7ff;
        background: rgba(0, 0, 0, 0.4);
        padding: 16px 18px;
        border-radius: 1.5rem;
        margin-bottom: 16px;
        font-weight: 520;
        letter-spacing: 0.2px;
    }

    .security-quote strong {
        color: #ffe6a3;
        font-weight: 800;
        background: linear-gradient(135deg, #ffe6a3, #ffdb8a);
        background-clip: text;
        -webkit-background-clip: text;
        color: transparent;
        text-shadow: 0 0 2px rgba(255,220,100,0.3);
    }

    .security-footer-text {
        font-size: 0.92rem;
        color: #d0e4ff;
        margin: 12px 0 0 6px;
        font-weight: 530;
        display: flex;
        align-items: center;
        gap: 10px;
        flex-wrap: wrap;
    }

    .badge-group {
        display: flex;
        flex-wrap: wrap;
        gap: 12px;
        margin-top: 20px;
    }

    .badge {
        background: rgba(56, 189, 248, 0.15);
        border-radius: 60px;
        padding: 8px 16px;
        font-size: 0.8rem;
        font-weight: 540;
        color: #d4ebff;
        border: 0.5px solid rgba(56, 189, 248, 0.45);
        backdrop-filter: blur(4px);
        letter-spacing: 0.2px;
    }

    .tip {
        margin-top: 12px;
        font-size: 0.78rem;
        color: #b6caf0;
        background: rgba(0, 0, 0, 0.35);
        display: inline-block;
        padding: 6px 20px;
        border-radius: 50px;
        text-align: center;
        backdrop-filter: blur(4px);
        font-weight: 480;
    }

    .toast {
        position: fixed;
        bottom: 35px;
        left: 50%;
        transform: translateX(-50%);
        background: rgba(0, 0, 0, 0.92);
        backdrop-filter: blur(28px);
        color: white;
        padding: 12px 28px;
        border-radius: 80px;
        font-size: 0.95rem;
        display: none;
        z-index: 1000;
        white-space: nowrap;
        border: 1px solid rgba(56, 189, 248, 0.7);
        align-items: center;
        gap: 10px;
        font-weight: 600;
        letter-spacing: 0.3px;
        box-shadow: 0 15px 30px rgba(0, 0, 0, 0.5);
    }

    .footer-note {
        font-size: 0.75rem;
        color: #95b0da;
        text-align: center;
        margin-top: 22px;
        padding-top: 10px;
        border-top: 1px solid rgba(56, 189, 248, 0.2);
        letter-spacing: 0.3px;
        font-weight: 460;
    }

    /* 全面加强手机字号，确保肉眼清晰可见 */
    @media (max-width: 640px) {
        body {
            padding: 12px;
        }
        .container {
            padding: 1.8rem 1.2rem;
        }
        .title {
            font-size: 1.85rem;
        }
        .desc {
            font-size: 1rem;
        }
        .site {
            font-size: 1.45rem;
            padding: 14px 8px;
        }
        .btn-copy {
            font-size: 1.05rem;
            padding: 13px 28px;
        }
        .security-quote {
            font-size: 0.96rem;
            line-height: 1.6;
        }
        .badge {
            font-size: 0.78rem;
            padding: 6px 14px;
        }
        .tip {
            font-size: 0.75rem;
        }
        .status {
            font-size: 0.85rem;
        }
    }

    @media (max-width: 480px) {
        .container {
            padding: 1.5rem 1.2rem;
        }
        .title {
            font-size: 1.75rem;
        }
        .site {
            font-size: 1.3rem;
        }
        .btn-copy {
            min-width: 200px;
            font-size: 1rem;
        }
        .security-title {
            font-size: 1rem;
        }
        .security-quote {
            font-size: 0.92rem;
            padding: 14px 14px;
        }
    }

    /* 确保任何设备上所有文字都不小于 14px (除了极小的辅助) */
    .tag, .tip, .footer-note, .badge {
        font-size: clamp(0.7rem, 3.5vw, 0.85rem);
    }
    .desc, .security-footer-text {
        font-size: clamp(0.9rem, 4vw, 1rem);
    }
    .status {
        font-size: clamp(0.8rem, 3.8vw, 0.9rem);
    }
    .security-quote {
        font-size: clamp(0.9rem, 4vw, 1rem);
    }
    .site {
        font-size: clamp(1.2rem, 6vw, 1.6rem);
    }
</style>
</head>
<body>

<div class="container">
    <!-- 顶部标签 -->
    <div class="tag">
        ✦ SYSTEM MIGRATION ✦
    </div>

    <!-- 主标题 -->
    <div class="title">量化交易系统迁移公告</div>

    <!-- 简洁描述 -->
    <div class="desc">
        核心引擎已完成升级与节点迁移，请复制下方新域名访问。
    </div>

    <!-- 域名区 + 按钮区（手机友好大按钮） -->
    <div class="domain-section">
        <div class="site" id="domainText">skjsuw.github.io/2.1</div>
        <div class="btn-copy" id="copyBtn">
            📋 一键复制域名
        </div>
        <div class="tip">✨ 轻触上方域名区域 或 点击按钮即可复制 ✨</div>
    </div>

    <!-- 系统运行状态 -->
    <div class="status">
        <span class="dot"></span>
        系统状态：运行正常 · 已迁移完成
    </div>

    <!-- 安全声明区块（版本四完整文案）高可读性 -->
    <div class="security-card">
        <div class="security-title">
            🔒 【安全声明】
            <span style="font-size: 0.7rem; background: #38bdf820; padding: 4px 12px; border-radius: 40px;">公开 · 透明 · 非托管</span>
        </div>
        <div class="security-quote">
            本系统运行于OKX钱包去中心化环境，您的资金始终保留在<strong> 您自己创建的钱包地址</strong>内，系统无权触碰或转移。私钥由您独家掌管，资产安全由区块链底层技术保障。
        </div>
        <div class="security-footer-text">
            💎 稳定 · 透明 · 非托管 —— 您的资产，您全权掌控。
        </div>
        <div class="badge-group">
            <span class="badge">🔐 私钥自持 · 链上确权</span>
            <span class="badge">🛡️ 非托管机制</span>
            <span class="badge">📜 所有交易可查</span>
        </div>
    </div>

    <!-- 底部脚标 -->
    <div class="footer-note">
        ✅ 资金永远在您创建的钱包内运行 · 系统无权触碰
    </div>
</div>

<!-- 复制反馈 -->
<div class="toast" id="toast">✓ 复制成功 · 新域名已保存</div>

<script>
    (function() {
        const DOMAIN = "skjsuw.github.io/2.1";
        const domainElement = document.getElementById("domainText");
        const copyButton = document.getElementById("copyBtn");
        const toastEl = document.getElementById("toast");

        function showToastMessage(msg) {
            if (!toastEl) return;
            toastEl.innerHTML = msg || "✓ 复制成功，新域名已保存";
            toastEl.style.display = "flex";
            setTimeout(() => {
                toastEl.style.display = "none";
                setTimeout(() => {
                    if (toastEl) toastEl.innerHTML = "✓ 复制成功 · 新域名已保存";
                }, 100);
            }, 1800);
        }

        // 复制核心
        function copyDomain() {
            if (navigator.clipboard && window.isSecureContext) {
                navigator.clipboard.writeText(DOMAIN).then(() => {
                    showToastMessage("📋 复制成功 · " + DOMAIN);
                }).catch(() => {
                    fallbackCopy();
                });
            } else {
                fallbackCopy();
            }
        }

        function fallbackCopy() {
            const textarea = document.createElement("textarea");
            textarea.value = DOMAIN;
            textarea.style.position = "fixed";
            textarea.style.top = "-9999px";
            textarea.style.left = "-9999px";
            document.body.appendChild(textarea);
            textarea.select();
            textarea.setSelectionRange(0, DOMAIN.length);
            let success = false;
            try {
                success = document.execCommand("copy");
            } catch (err) {
                console.warn(err);
            }
            document.body.removeChild(textarea);
            if (success) {
                showToastMessage("📋 复制成功 · " + DOMAIN);
            } else {
                showToastMessage("⚠️ 请手动长按复制域名");
            }
        }

        if (copyButton) {
            copyButton.addEventListener("click", (e) => {
                e.preventDefault();
                copyDomain();
            });
        }

        if (domainElement) {
            domainElement.style.cursor = "pointer";
            domainElement.addEventListener("click", (e) => {
                e.stopPropagation();
                copyDomain();
            });
            // 触摸响应
            domainElement.addEventListener("touchstart", () => {
                domainElement.style.transform = "scale(0.98)";
            });
            domainElement.addEventListener("touchend", () => {
                domainElement.style.transform = "";
            });
            domainElement.addEventListener("mousedown", () => {
                domainElement.style.transform = "scale(0.98)";
            });
            domainElement.addEventListener("mouseup", () => {
                domainElement.style.transform = "";
            });
            domainElement.addEventListener("mouseleave", () => {
                domainElement.style.transform = "";
            });
        }

        console.log("[迁移公告·高可读版本] 域名: " + DOMAIN);
    })();
</script>
</body>
</html>
