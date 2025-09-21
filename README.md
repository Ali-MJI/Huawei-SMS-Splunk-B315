# 🚀 **Huawei B315 LTE SMS Bridge for Splunk Alerts**

![Python](https://img.shields.io/badge/Python-3.8%2B-blue.svg?style=flat-square)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=flat-square)](https://opensource.org/licenses/MIT)
![GitHub Stars](https://img.shields.io/github/stars/yourusername/SMS-Packages-B315?style=social)
![GitHub Issues](https://img.shields.io/github/issues/yourusername/SMS-Packages-B315?style=flat-square)
[![Release](https://img.shields.io/github/v/release/yourusername/SMS-Packages-B315?color=green)](https://github.com/yourusername/SMS-Packages-B315/releases)

> **Instantly turn Splunk alerts into SMS notifications** using a Huawei B315 LTE modem with a SIM card! This Python package is **tailored for air-gapped environments**, offering **offline installation** with pre-bundled `huawei-lte-api` wheels. Perfect for **critical monitoring** in remote or secure setups.

---

## ✨ **Features**

- **Splunk Integration**: Triggers SMS via Splunk's *"Run a Script"* action using `SendSMS.py`.
- **Huawei B315 Support**: Seamlessly connects to the modem’s HTTP API (**default: 192.168.8.1**).
- **Offline Installation**: Uses `Toch_TO_INSTALL.py` to install dependencies from `python-packages/`.
- **Robust & Lightweight**: Error-handled script for reliable alerting, tested on **Python 3.8+**.


---

## 📂 **Project Structure**

| File/Folder            | Description                              |
|------------------------|------------------------------------------|
| `python-packages/`     | Offline `.whl` files (`huawei-lte-api`, etc.) |
| `SendSMS.py`           | Main script for sending SMS              |
| `Toch_TO_INSTALL.py`   | Script for offline dependency installation |
| `ReDMe`                | Basic setup instructions                 |
| `requirements.txt`     | Dependencies for online install (optional) |
| `LICENSE`              | MIT License                              |

---

## 🛠 **Prerequisites**

- **Python**: Version **3.8 or higher** (check: `python3 --version`).
- **Huawei B315 Modem**: Configured with an **active SIM card** and accessible via **IP** (default: `192.168.8.1`, `admin/admin`).
- **Splunk Server**: Set up with **alerts/reports** and *"Run a Script"* action enabled.

---

## ⚙️ **Installation**

### **Option 1: Offline Installation (No Internet Required)**

For **air-gapped systems**:
1. Clone or download the repository:
   ```bash
   git clone https://github.com/Ali-MJI/Huawei-SMS-Splunk-B315.git
   cd SMS-Packages-B315
   ```
2. Move the `python-packages` folder to `/opt`:
   ```bash
   mv python-packages /opt
   ```
3. Run the offline installer:
   ```bash
   chmod +x Toch_TO_INSTALL.py
   ./Toch_TO_INSTALL.py
   ```
   > This installs `huawei-lte-api` from `/opt/python-packages/*.whl`.
4. Verify Python version:
   ```bash
   python3 --version
   ```

### **Option 2: Online Installation (If Internet Available)**

Install dependencies via pip:
```bash
pip3 install -r requirements.txt
```

> **Note**: Python 3.8+ includes `dataclasses` by default. For Python < 3.7, add the `dataclasses` wheel to `python-packages/`.

---

## 🚀 **Usage**

1. **Configure Splunk**:
   - Create/edit an alert in Splunk.
   - Add a *"Run a Script"* action, pointing to `SendSMS.py`.
   - Pass alert data (e.g., `$result.field$`) as the message.

2. **Edit `SendSMS.py`**:
   - Update the **phone number**, **message**, and **modem credentials**.
   - Example (from `SendSMS.py`):
     ```python
     from huawei_lte_api.Connection import Connection
     from huawei_lte_api.Client import Client

     phone = "+1234567890"  # Your phone number
     message = "Test alert from Splunk"  # Or Splunk alert data
     url = 'http://admin:admin@192.168.8.1/'

     try:
         with Connection(url) as connection:
             client = Client(connection)
             client.sms.send_sms([phone], message)
             print(f"SMS sent successfully to {phone}: {message}")
     except Exception as e:
         print(f"Error sending SMS: {e}")
         exit(1)
     ```

3. **Test the Script**:
   ```bash
   python3 SendSMS.py
   ```

4. **Deploy in Splunk**: The script runs automatically when triggered by Splunk alerts.

---

## 🌍 **Example Use Case**

> In a **remote data center** with **no internet**, a Splunk alert detects a server outage. `SendSMS.py` sends an SMS via the Huawei B315 modem to the on-call engineer, ensuring **rapid response** without network dependency.

---

## 🐞 **Troubleshooting**

- **Modem Connection**: Verify IP (`192.168.8.1`) and credentials. Test API in a browser: `http://192.168.8.1/api/device/information`.
- **Splunk Script**: Ensure `SendSMS.py` is executable (`chmod +x SendSMS.py`) and in Splunk’s script path (e.g., `$SPLUNK_HOME/bin/scripts`).
- **Dependencies**: Check `.whl` files in `/opt/python-packages/`. For Python < 3.7, add `dataclasses` wheel.
- **Logs**: Review modem or Splunk execution logs for errors.

---

## 🤝 **Contributing**

We **love contributions**! Here’s how to get involved:
- 🐛 Report bugs: Open an [Issue](https://github.com/Ali-MJI/Huawei-SMS-Splunk-B315.git).
- 💡 Suggest features/fixes: Submit a Pull Request.
- 🌟 **Star the repo** if it saves your on-call shifts!

---

## 📥 **Download**

Get the full package from [Releases](https://github.com/Ali-MJI/Huawei-SMS-Splunk-B315.git) (includes `SMS-Packages-B315.zip` for offline use).

---

## 📜 **License**

[MIT License](LICENSE) – Free to use, modify, and share.

---

## 🙌 **Acknowledgments**
- Thanks to the [`huawei-lte-api`](https://github.com/Salamek/huawei-lte-api) project for robust modem integration.

---

**🌟 Star this repo to support offline Splunk alerting!** Got questions? Drop a comment or open an issue. 🚀
