Huawei B315 LTE SMS Bridge for Splunk Alerts 🚀

Transform your Splunk alerts into instant SMS notifications using a Huawei B315 LTE modem with a SIM card. This Python package is designed for air-gapped environments, offering a fully offline installation with pre-bundled huawei-lte-api wheel files. Perfect for critical monitoring in remote or secure setups!
Features

Splunk Integration: Triggers SMS via Splunk's "Run a Script" Alert Action.
Huawei B315 Support: Seamlessly connects to the modem’s HTTP API (default: 192.168.8.1).
Offline Installation: Includes wheel files for huawei-lte-api and dependencies.
Customizable: Easily modify send.py for tailored alerts or bulk SMS.
Lightweight & Robust: Tested on Python 3.8+, with error handling for modem connectivity.

Project Structure
Python-package/
├── src/
│   └── send.py              # Main script for sending SMS
├── wheels/                  # Offline .whl files for dependencies
│   ├── huawei-lte-api-*.whl
│   └── [other dependencies]
├── install_offline.sh       # Script for offline installation
├── requirements.txt         # Dependencies for online installation
├── README.md               # This file
└── LICENSE                 # MIT License

Prerequisites

Python: Version 3.8 or higher (python3 --version).
Huawei B315 Modem: Configured with an active SIM card and accessible via IP (default: 192.168.8.1).
Splunk Server: Set up with alerts/reports and "Run a Script" action enabled.
Credentials: Modem admin username/password (default: admin/admin).

Installation
Option 1: Offline Installation (No Internet Required)
For air-gapped systems, use the bundled wheel files:

Clone or download the repository:git clone https://github.com/yourusername/huawei-sms-splunk-b315.git
cd huawei-sms-splunk-b315


Run the offline installer:chmod +x Python-package/install_offline.sh
./Python-package/install_offline.sh

This installs huawei-lte-api and dependencies from the wheels/ folder.

Option 2: Online Installation (If Internet Available)
Install dependencies via pip:
pip3 install -r Python-package/requirements.txt


Note: Python 3.8+ includes dataclasses by default. For Python < 3.7, add the dataclasses wheel to wheels/.

Usage

Configure Splunk:
Create or edit an alert in Splunk.
Add a "Run a Script" action, pointing to Python-package/src/send.py.
Pass alert data (e.g., $result.field$) to the script.


Edit send.py:
Update modem IP, credentials, and target phone numbers.
Example:from huawei_lte_api.Client import Client
from huawei_lte_api.Connection import Connection

# Connect to Huawei B315 modem
connection = Connection('http://192.168.8.1', username='admin', password='admin')
client = Client(connection)

# Send SMS with Splunk alert
alert_message = "Splunk Alert: Critical server error detected!"
phone_numbers = ['+1234567890']  # Add recipient numbers
client.sms.send_sms(phone_numbers, alert_message)
print("SMS sent successfully!")




Test the Script:cd Python-package/src
python3 send.py


Deploy in Splunk: The script runs automatically when triggered by Splunk alerts.

Example Use Case
Imagine a remote data center with no internet. A Splunk alert detects a server failure. This package sends an SMS via the B315 modem to the on-call engineer, ensuring rapid response without network dependency.
Troubleshooting

Modem Connection Issues: Verify IP (192.168.8.1) and credentials. Test API access in a browser (e.g., http://192.168.8.1/api/device/information).
Splunk Script Errors: Ensure send.py is executable (chmod +x send.py) and in Splunk’s script path (e.g., $SPLUNK_HOME/bin/scripts).
Dependency Errors: Check Python version. For missing dependencies, add relevant .whl files to wheels/.
Logs: Check modem logs or Splunk’s execution logs for errors.

Contributing
We love contributions! Here's how to get involved:

🐛 Report bugs: Open an Issue.
💡 Suggest features or submit fixes: Create a Pull Request.
🌟 Star the repo if it saves your on-call shifts!

Download
Grab the full package from Releases (includes Python-package.zip for offline use).
License
MIT License – Free to use, modify, and distribute.
Acknowledgments

Built with inspiration from xAI’s Grok.
Thanks to the huawei-lte-api community for robust modem integration.


Star this repo to support real-time alerting in air-gapped environments! Questions? Drop a comment or open an issue. 🚀
