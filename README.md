========================================================================
  Google AI Pro (5 TB) 零成本两年 (US$0.00 -> 24个月) 全自动控制台
========================================================================

【一、运行环境要求】

### Windows:
1. Windows 10 / 11 系统
2. 已安装 Google Chrome 浏览器（默认路径即可）
3. 已安装 Python 3.10 或更高版本（安装时勾选 Add Python to PATH）
4. 网络环境：本机开启美区（US）代理，或在控制台左侧填写代理模板

### Linux (Ubuntu / Debian / RHEL / Arch 等):
1. Python 3.10 或更高版本，并安装 venv 模块：
   ```bash
   sudo apt update && sudo apt install -y python3 python3-venv python3-pip
   ```
2. 安装 Google Chrome 或 Chromium 浏览器：
   ```bash
   # 安装 Google Chrome Stable:
   wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
   sudo dpkg -i google-chrome-stable_current_amd64.deb || sudo apt -f install -y
   # 或者安装 Chromium:
   sudo apt install -y chromium-browser # 或 sudo apt install -y chromium
   ```
3. Playwright 浏览器依赖（如使用 Playwright 内置 Chromium）：
   ```bash
   python3 -m playwright install --with-deps chromium
   ```

【二、快速启动步骤】

### Windows:
1. 首次使用请双击运行：【1_首次运行_安装依赖并启动.bat】
2. 之后日常使用直接双击：【2_启动控制台.bat】
3. 浏览器会自动打开控制台页面：http://127.0.0.1:8765

### Linux:
1. 赋予执行权限并启动启动脚本：
   ```bash
   chmod +x start_linux.sh
   ./start_linux.sh
   ```
   脚本将自动创建虚拟环境 `.venv`、安装 `requirements.txt` 依赖、检测 Chrome/Chromium 浏览器并在图形桌面环境自动调用 `xdg-open` 打开控制台：http://127.0.0.1:8765。

2. 自定义浏览器路径（可选）：
   若 Chrome/Chromium 安装在自定义路径，可在启动前通过 `CHROME_PATH` 环境变量指定：
   ```bash
   export CHROME_PATH=/usr/bin/google-chrome-stable
   ./start_linux.sh
   ```

3. 无图形界面 (Headless / VPS 服务器) 运行说明：
   - **虚拟显示 (推荐)**：使用 `xvfb-run` 提供虚拟显示，避免被目标平台反自动化系统判定为无头环境：
     ```bash
     sudo apt install -y xvfb
     xvfb-run -a ./start_linux.sh
     ```
   - **无头模式**：若需以 Chrome 内置无头模式运行，可设置 `HEADLESS=1`：
     ```bash
     HEADLESS=1 ./start_linux.sh
     ```
   - **远程访问控制台**：控制台默认安全绑定在本地 `127.0.0.1:8765`。在无桌面服务器上部署时，建议使用 SSH 本地端口转发安全访问，无需暴露端口到公网：
     ```bash
     ssh -L 8765:127.0.0.1:8765 user@your-server-ip
     ```
     连接建立后，在本地电脑浏览器访问 `http://127.0.0.1:8765` 即可安全操作控制台。

【三、自定义填写支付卡 & 跑号说明】
1. 填写支付卡（必填）：
   - 在网页左侧【全局配置与内联免税绑卡】区域，填入你自己的 Visa 或 Mastercard 外币卡：
     * 卡号（16位数字）
     * 有效期（月 / 年，如 08 / 29）
     * 安全码（3位 CVC）
     * 持卡人英文姓名
     * 免税邮编默认已填好 97201（美国俄勒冈免税州），无需修改
   - 填写后点击【💾 保存配置】。
   - 注：脚本内置严格 0 元消费保护，仅在结账弹窗确认为 US$0.00 时才会点击订阅，全程 0 扣费。

2. 批量导入 Google 账号：
   - 在网页右侧【批量放号导入区】粘贴账号（每行一个），支持以下任意格式：
     * 邮箱----密码----辅助邮箱
     * 邮箱----密码----辅助邮箱----2FA密钥
     * 邮箱----密码----2FA密钥
   - 点击【➕ 一键导入账号列表】。

3. 开始全自动执行：
   - 点击单个账号右侧的【▶ 执行】或顶部的【▶ 批量全自动执行】。
   - 脚本会自动完成：
     Step 1: 自动登录 Google 并通过辅助邮箱 / 2FA 验证
     Step 2: 内联免税绑卡 + 首层 12 个月免费包 (US$0.00)
     Step 3: 叠加二层 6 个月免费包 (US$0.00 -> 18个月)
     Step 4: 叠加三层 6 个月免费包 (US$0.00 -> 24个月封顶)
     Step 5: 自动前往 Google Play 取消自动续订，锁死 2 年到期权益并截图验真

【四、安全与隐私提示 (Security Guidance)】
1. **凭据安全**：
   - `config.json` 包含您配置的支付卡信息与账号凭据。切勿将包含真实卡号、CVC、密码或 2FA 密钥的 `config.json` 文件提交至公开 Git 仓库或对外共享。
   - 在 Linux / 多用户服务器环境中，建议限制配置文件的读取权限：
     ```bash
     chmod 600 config.json
     ```
2. **环境隔离**：
   - 每个账号的浏览器会话与缓存保存在 `profiles/` 目录中，截图保存在 `screenshots/` 目录中。本项目 `.gitignore` 已配置忽略此类运行时数据。
3. **网络安全**：
   - 控制台服务默认仅监听 `127.0.0.1`，请勿直接将其绑定到 `0.0.0.0` 或暴露到公网未授权端口。如需远程使用，请始终通过 SSH 隧道或受密码保护的反向代理访问。


# 卡网：https://faka.cdkey.si
# 博客：https://blog.caowo.de
# TG群：@Hello_Florence
