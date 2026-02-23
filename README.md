# Undervolting-Arch-Linux-Intel-Laptops
Step by Step guide to the only successful method I found for undervolting 10th gen intel laptops using Arch Linux. I did not create the Undervolting tool, and as such, please refer to the original creator for any issues or troubleshooting steps - https://github.com/georgewhewell/undervolt.git
# Intel CPU Undervolt Setup (Arch Linux)

⚠️ **Warning:** Undervolting incorrectly can cause system instability. Test carefully.

---

## Install Python Dependencies (Arch)

```bash
sudo pacman -S git python python-setuptools
```

---

## Clone Repository

```bash
git clone https://github.com/georgewhewell/undervolt.git
```

---

## Enter Directory

```bash
cd undervolt
```

---

## Install Undervolt

```bash
sudo python setup.py install
```

---

## Test Undervolt Tool

```bash
sudo undervolt --read
```

---
<img width="952" height="676" alt="undervolt ss" src="https://github.com/user-attachments/assets/e5de5eea-2d52-49df-bbad-23180c9c2f41" />

this is what you should see (everything should say 0 at this point)

# Make It Persistent (Systemd Service)

Create service file:

```bash
sudo nano /etc/systemd/system/undervolt.service
```

## Use This as a Template
using -50 on the core/cache/gpu(igpu) is a very safe start that should have next to no issues running on all systems. Good practice is to go up by 5-10 (example -50 to -60) and stress test your PC via gaming or benchmarking tool to determine stability. every system will be different regardless of using the same/better/worse hardware.
```ini
[Unit]
Description=Apply Intel CPU undervolt & power limits
After=multi-user.target

[Service]
Type=oneshot
ExecStart=/usr/bin/undervolt --core -50 --cache -50 --gpu -50
RemainAfterExit=yes

[Install]
WantedBy=multi-user.target
```

Save & exit:
- CTRL+O → Enter
- CTRL+X

---

## Enable Service

```bash
sudo systemctl daemon-reload
sudo systemctl enable --now undervolt.service
```

---

## Reboot & Verify

```bash
sudo undervolt --read
```
