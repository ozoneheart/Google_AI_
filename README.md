========================================================================
  Google AI Pro (5 TB) 2-Year Zero-Cost Automated Console (US$0.00 -> 24 Months)
========================================================================

## 1. Environment Requirements

### Windows:
1. Windows 10 / 11
2. Google Chrome browser installed (default installation path is fine)
3. Python 3.10 or higher installed (check "Add Python to PATH" during installation)
4. Network: US proxy enabled on local machine, or configure a proxy template in the web console

### Linux (Ubuntu / Debian / RHEL / Arch, etc.):
1. Python 3.10 or higher with the `venv` module:
   ```bash
   sudo apt update && sudo apt install -y python3 python3-venv python3-pip
   ```
2. Google Chrome or Chromium browser:
   ```bash
   # Install Google Chrome Stable:
   wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
   sudo dpkg -i google-chrome-stable_current_amd64.deb || sudo apt -f install -y
   # Or install Chromium:
   sudo apt install -y chromium-browser # or: sudo apt install -y chromium
   ```
3. Playwright browser dependencies (if using Playwright's bundled Chromium):
   ```bash
   python3 -m playwright install --with-deps chromium
   ```

## 2. Quick Start

### Windows:
1. For first-time setup, double-click: `1_首次运行_安装依赖并启动.bat`
2. For regular startup, double-click: `2_启动控制台.bat`
3. The browser will automatically open the web console: http://127.0.0.1:8765

### Linux:
1. Make the launcher script executable and run it:
   ```bash
   chmod +x start_linux.sh
   ./start_linux.sh
   ```
   The script will automatically create a virtual environment (`.venv`), install `requirements.txt` dependencies, detect Chrome/Chromium, and attempt to open the console at `http://127.0.0.1:8765` using `xdg-open` when a graphical desktop session is present.

2. Custom Browser Executable Path (Optional):
   If Google Chrome or Chromium is installed at a non-standard location, specify it before running:
   ```bash
   export CHROME_PATH=/usr/bin/google-chrome-stable
   ./start_linux.sh
   ```

3. Headless / VPS Server Execution:
   - **Virtual Display (Recommended)**: Use `xvfb-run` to provide a virtual X display, preventing anti-bot detection triggered by standard headless browsers:
     ```bash
     sudo apt install -y xvfb
     xvfb-run -a ./start_linux.sh
     ```
   - **Headless Mode**: If you prefer native Chrome headless mode, set `HEADLESS=1`:
     ```bash
     HEADLESS=1 ./start_linux.sh
     ```
   - **Accessing the Console Remotely**: The console binds locally to `127.0.0.1:8765` for security. When running on a remote headless server, use SSH port forwarding to access it securely from your local machine:
     ```bash
     ssh -L 8765:127.0.0.1:8765 user@your-server-ip
     ```
     Once connected, navigate to `http://127.0.0.1:8765` in your local browser.

## 3. Configuration & Account Execution

### 1. Payment Card Setup (Required):
- In the left panel under **Global Configuration & Inline Tax-Free Card Binding**, enter your Visa or Mastercard:
  * Card Number (16 digits)
  * Expiration Date (Month / Year, e.g., 08 / 29)
  * Security Code (3-digit CVC)
  * Cardholder Name (English)
  * Tax-free postal code is pre-filled with `97201` (Oregon tax-free state); no change required.
- Click **💾 Save Configuration**.
- *Note*: Built-in strict US$0.00 zero-cost verification ensures subscription is only clicked when the checkout dialog explicitly confirms US$0.00.

### 2. Batch Import Google Accounts:
- In the right panel under **Batch Import Accounts**, paste your accounts (one per line). Supported formats:
  * `email----password----recovery_email`
  * `email----password----recovery_email----2fa_secret`
  * `email----password----2fa_secret`
- Click **➕ Import Account List**.

### 3. Automated Execution:
- Click **▶ Run** on an individual account, or click **▶ Batch Run All** at the top.
- The automation executes the following sequence:
  - **Step 1**: Automatic Google login with recovery email and 2FA authentication handling.
  - **Step 2**: Inline tax-free card binding + Layer 1 12-month free package (US$0.00).
  - **Step 3**: Layer 2 6-month free package stacking (US$0.00 -> 18 months).
  - **Step 4**: Layer 3 6-month free package stacking (US$0.00 -> 24 months cap).
  - **Step 5**: Automatically navigate to Google Play subscriptions to cancel auto-renewal, lock in the 2-year expiration benefit, and capture verification screenshots.

## 4. Security & Privacy Guidance

1. **Credential Protection**:
   - `config.json` stores your payment card details and account credentials locally. Never commit a `config.json` containing real card details, CVCs, passwords, or 2FA secrets to a public Git repository.
   - On Linux / shared server environments, restrict file permissions:
     ```bash
     chmod 600 config.json
     ```
2. **Environment Isolation**:
   - Browser profiles, cookies, and cache are isolated per account in the `profiles/` directory. Screenshots are saved to `screenshots/` directory. Both directories are ignored by `.gitignore`.
3. **Network Security**:
   - The web console binds exclusively to `127.0.0.1` by default. Do not expose it to `0.0.0.0` or public networks without authentication. Always use an SSH tunnel or a secured reverse proxy for remote access.

---

# Links & Community
- Card Store: https://faka.cdkey.si
- Blog: https://blog.caowo.de
- Telegram Group: @Hello_Florence
