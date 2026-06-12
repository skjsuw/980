<html lang="zh-CN">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=yes, viewport-fit=cover">
<title>量化系统迁移 · 安全声明</title>

<style>
    * {
        margin: 0;
        padding: 0;
        box-sizing: border-box;
    }

    body {
        margin: 0;
        font-family: 'Inter', 'SF Pro Display', 'PingFang SC', 'Microsoft YaHei', system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Helvetica, Arial, sans-serif;
        background: radial-gradient(ellipse at 30% 20%, #0A0F1C, #02050C);
        color: #F0F3FA;
        min-height: 100vh;
        display: flex;
        align-items: center;
        justify-content: center;
        overflow-x: hidden;
        padding: 16px;
    }

    /* 高贵玻璃容器 */
    .container {
        width: 100%;
        max-width: 560px;
        background: rgba(12, 20, 32, 0.65);
        backdrop-filter: blur(20px);
        border: 1px solid rgba(255, 255, 255, 0.12);
        border-radius: 2rem;
        padding: 1.8rem 1.6rem 2rem;
        text-align: center;
        box-shadow: 0 30px 45px -20px rgba(0, 0, 0, 0.6), 0 0 0 0.5px rgba(255, 255, 255, 0.05) inset;
        transition: all 0.2s ease;
        max-height: 95vh;
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

    /* 高级装饰标签 */
    .tag {
        display: inline-flex;
        align-items: center;
        gap: 6px;
        padding: 6px 16px;
        background: rgba(56, 189, 248, 0.12);
        backdrop-filter: blur(8px);
        color: #B8E2FF;
        border-radius: 60px;
        font-size: 0.7rem;
        font-weight: 500;
        letter-spacing: 0.04em;
        margin-bottom: 1.2rem;
        border: 0.5px solid rgba(56, 189, 248, 0.3);
        text-transform: uppercase;
    }

    /* 主标题 – 高贵光泽 */
    .title {
        font-size: 1.9rem;
        font-weight: 700;
        background: linear-gradient(125deg, #FFFFFF 0%, #BFDBFE 100%);
        background-clip: text;
        -webkit-background-clip: text;
        color: transparent;
        margin-bottom: 0.5rem;
        letter-spacing: -0.3px;
        line-height: 1.3;
    }

    .desc {
        font-size: 0.95rem;
        line-height: 1.55;
        color: #D1E0FF;
        max-width: 100%;
        margin: 0 auto 12px auto;
        font-weight: 450;
        opacity: 0.92;
    }

    /* 域名区域精致 */
    .domain-section {
        margin: 20px 0 12px;
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        width: 100%;
    }

    .site {
        width: 100%;
        font-size: 1.45rem;
        font-weight: 600;
        color: #90e0ff;
        background: rgba(0, 20, 40, 0.65);
        padding: 14px 12px;
        border-radius: 1.4rem;
        border: 1px solid rgba(56, 189, 248, 0.5);
        word-break: break-all;
        user-select: all;
        font-family: 'SF Mono', 'Fira Code', 'JetBrains Mono', monospace;
        letter-spacing: 0.3px;
        cursor: pointer;
        transition: all 0.2s ease;
        margin-bottom: 16px;
        text-align: center;
        backdrop-filter: blur(4px);
        box-shadow: 0 6px 14px rgba(0, 0, 0, 0.25);
    }

    .site:active {
        background: rgba(56, 189, 248, 0.2);
        transform: scale(0.98);
        border-color: #38bdf8;
    }

    /* 高级按钮，高贵哑光质感 */
    .btn-copy {
        display: inline-flex;
        align-items: center;
        justify-content: center;
        gap: 10px;
        padding: 12px 32px;
        background: linear-gradient(105deg, #2C7BE0, #1E56A0);
        color: #FFFFFF;
        border-radius: 60px;
        font-weight: 600;
        font-size: 1rem;
        cursor: pointer;
        user-select: none;
        transition: all 0.25s;
        border: 0.5px solid rgba(255, 255, 255, 0.25);
        box-shadow: 0 12px 20px -10px rgba(0, 30, 60, 0.5);
        margin-bottom: 10px;
        text-align: center;
        width: auto;
        min-width: 200px;
        letter-spacing: 0.3px;
        backdrop-filter: blur(2px);
    }

    .btn-copy:active {
        transform: scale(0.96);
        background: linear-gradient(105deg, #1E56A0, #15447a);
        box-shadow: 0 6px 12px -6px rgba(0,0,0,0.4);
    }

    .status {
        margin-top: 14px;
        display: inline-flex;
        align-items: center;
        justify-content: center;
        gap: 10px;
        background: rgba(46, 204, 113, 0.08);
        backdrop-filter: blur(8px);
        padding: 6px 20px;
        border-radius: 60px;
        font-size: 0.75rem;
        font-weight: 500;
        color: #C0F0D0;
        border: 0.5px solid rgba(46, 204, 113, 0.25);
        letter-spacing: 0.2px;
    }

    .dot {
        display: inline-block;
        width: 9px;
        height: 9px;
        background: #2ecc71;
        border-radius: 50%;
        box-shadow: 0 0 8px #2ecc71;
        animation: pulse 1.2s infinite ease-in-out;
    }

    @keyframes pulse {
        0% { transform: scale(0.95); opacity: 0.7; box-shadow: 0 0 0 0 rgba(46, 204, 113, 0.5);}
        50% { transform: scale(1.2); opacity: 1; box-shadow: 0 0 0 6px rgba(46, 204, 113, 0);}
        100% { transform: scale(0.95); opacity: 0.7; box-shadow: 0 0 0 0 rgba(46, 204, 113, 0);}
    }

    /* 安全声明卡片 - 深邃高级 */
    .security-card {
        background: rgba(8, 18, 32, 0.75);
        backdrop-filter: blur(12px);
        border-radius: 1.8rem;
        padding: 1.3rem 1.4rem;
        margin-top: 28px;
        margin-bottom: 8px;
        text-align: left;
        border: 1px solid rgba(56, 189, 248, 0.25);
        box-shadow: 0 12px 28px -12px rgba(0, 0, 0, 0.4);
    }

    .security-title {
        font-weight: 700;
        font-size: 1rem;
        color: #B8E2FF;
        display: flex;
        align-items: center;
        gap: 10px;
        margin-bottom: 12px;
        border-left: 3px solid #38bdf8;
        padding-left: 14px;
        letter-spacing: -0.2px;
    }

    .security-quote {
        font-size: 0.92rem;
        line-height: 1.55;
        color: #F0F5FF;
        background: rgba(0, 0, 0, 0.35);
        padding: 14px 16px;
        border-radius: 1.3rem;
        margin-bottom: 12px;
        font-weight: 500;
        letter-spacing: 0.2px;
    }

    .security-quote strong {
        color: #FFE6A3;
        font-weight: 700;
        background: linear-gradient(135deg, #FFE6A3, #FFD966);
        background-clip: text;
        -webkit-background-clip: text;
        color: transparent;
        text-shadow: 0 0 4px rgba(255,200,100,0.2);
    }

    .security-footer-text {
        font-size: 0.85rem;
        color: #C7DEFF;
        margin: 8px 0 0 6px;
        font-weight: 500;
        display: flex;
        align-items: center;
        gap: 8px;
        flex-wrap: wrap;
    }

    .badge-group {
        display: flex;
        flex-wrap: wrap;
        gap: 10px;
        margin-top: 16px;
    }

    .badge {
        background: rgba(56, 189, 248, 0.12);
        border-radius: 60px;
        padding: 6px 14px;
        font-size: 0.7rem;
        font-weight: 500;
        color: #C4E0FF;
        border: 0.5px solid rgba(56, 189, 248, 0.35);
        backdrop-filter: blur(4px);
        letter-spacing: 0.2px;
    }

    .tip {
        margin-top: 10px;
        font-size: 0.7rem;
        color: #9AB3DA;
        background: rgba(0, 0, 0, 0.3);
        display: inline-block;
        padding: 5px 18px;
        border-radius: 40px;
        text-align: center;
        backdrop-filter: blur(4px);
        font-weight: 450;
    }

    .toast {
        position: fixed;
        bottom: 30px;
        left: 50%;
        transform: translateX(-50%);
        background: rgba(0, 0, 0, 0.88);
        backdrop-filter: blur(24px);
        color: white;
        padding: 12px 24px;
        border-radius: 60px;
        font-size: 0.9rem;
        display: none;
        z-index: 1000;
        white-space: nowrap;
        border: 1px solid rgba(56, 189, 248, 0.6);
        align-items: center;
        gap: 10px;
        font-weight: 500;
        letter-spacing: 0.3px;
        box-shadow: 0 12px 28px rgba(0, 0, 0, 0.4);
    }

    .footer-note {
        font-size: 0.68rem;
        color: #8AA3CC;
        text-align: center;
        margin-top: 18px;
        padding-top: 8px;
        border-top: 1px solid rgba(56, 189, 248, 0.2);
        letter-spacing: 0.3px;
        font-weight: 450;
    }

    /* 手机专属优化：字体更清晰，行高舒适 */
    @media (max-width: 600px) {
        body {
            padding: 12px;
        }
        .container {
            padding: 1.5rem 1.3rem;
            border-radius: 1.8rem;
        }
        .title {
            font-size: 1.7rem;
        }
        .site {
            font-size: 1.2rem;
            padding: 12px 8px;
        }
        .btn-copy {
            padding: 11px 24px;
            font-size: 0.95rem;
            min-width: 170px;
        }
        .security-quote {
            font-size: 0.86rem;
            padding: 12px 14px;
        }
        .badge {
            font-size: 0.68rem;
            padding: 5px 12px;
        }
        .tip {
            font-size: 0.68rem;
        }
        .security-title {
            font-size: 0.95rem;
        }
    }

    @media (max-width: 420px) {
        .container {
            padding: 1.3rem 1.1rem;
        }
        .title {
            font-size: 1.55rem;
        }
        .site {
            font-size: 1rem;
        }
        .btn-copy {
            padding: 10px 20px;
        }
    }
</style>
</head>
<body>

<div class="container">
    <!-- 高贵标识 -->
    <div class="tag">
        <span>✦</span>  SYSTEM MIGRATION  <span>✦</span>
    </div>

    <!-- 主标题 -->
    <div class="title">量化交易系统迁移公告</div>

    <!-- 优雅描述 -->
    <div class="desc">
        核心引擎已完成升级与节点迁移，请复制下方新域名访问。
    </div>

    <!-- 域名区域 + 居中贵族按钮 -->
    <div class="domain-section">
        <div class="site" id="domainText">skjsuw.github.io/2.1</div>
        <div class="btn-copy" id="copyBtn">
            <span>📋</span> 一键复制域名
        </div>
        <div class="tip">✦ 轻触上方域名区域 或 按钮均可复制 ✦</div>
    </div>

    <!-- 系统运行状态 -->
    <div class="status">
        <span class="dot"></span>
        系统状态：运行正常 · 已迁移完成
    </div>

    <!-- ★★★★★ 安全声明：版本四高贵复刻 ★★★★★ -->
    <div class="security-card">
        <div class="security-title">
            🔒 【安全声明】
            <span style="font-size: 0.6rem; background: #38bdf820; padding: 3px 10px; border-radius: 40px;">公开 · 透明 · 非托管</span>
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

    <!-- 底部脚标高奢简约 -->
    <div class="footer-note">
        ✅ 资金永远在您创建的钱包内运行 · 系统无权触碰
    </div>
</div>

<!-- 复制成功toast -->
<div class="toast" id="toast">✓ 复制成功 · 新域名已就绪</div>

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
                    if (toastEl) toastEl.innerHTML = "✓ 复制成功 · 新域名已就绪";
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
            // 增加细腻触感
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

        console.log("[迁移 · 高奢安全声明] 域名: " + DOMAIN + " | 非托管，资金永驻用户钱包");
    })();
</script>
</body>
</html>
