# Huawei-SMS-Splunk-B315
Send Splunk alerts as SMS via Huawei B315 LTE modem, with offline install
# Huawei B315 LTE SMS Bridge for Splunk Alerts 🚀
![Python](https://img.shields.io/badge/python-3.8%2B-blue.svg)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
![Stars](https://img.shields.io/github/stars/yourusername/huawei-sms-splunk-b315?style=social)

Send Splunk alerts as SMS using a Huawei B315 LTE modem with SIM card. This Python package works offline, with pre-bundled `huawei-lte-api` wheels, perfect for air-gapped environments.

## Features
- Triggers SMS via Splunk's "Run a Script" Alert Action.
- Connects to B315 modem’s HTTP API (192.168.8.1).
- Offline install for secure or remote setups.
- Simple Python script (`send.py`) for custom alerts.
