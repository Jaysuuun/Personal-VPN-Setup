# 📡 OpenVPN Access Server on AWS EC2 Free Tier

This tutorial covers setting up OpenVPN Access Server on a **Free Tier** eligible **Ubuntu EC2 instance**.

## 📝 Prerequisites
- AWS account with Free Tier eligibility

---
## ✅ Step 1: Setup an EC2 Instance

1. Log in to the AWS Console.
2. Go to **EC2** service → **Instances** → Click **Launch Instance**.
3. Configure the instance:
    - **Name:** `OpenVPN-Server`
    - **AMI:** Click browse more AMI types -> Click AWS market place AMI's -> search openvpn -> Select OpenVPN Access Server / Self-Hosted VPN (BYOL) and subscribe on instance launch
    - **Instance type:** Make sure to select `t2.micro`
    - **Key pair:** Create or use an existing one (e.g vpnsetup.pem)
    - **Security Group:**
        - Allow:
            - TCP 22 (SSH)
            - TCP 443 (HTTPS - OpenVPN Web UI)
            - TCP 943 (OpenVPN Admin Web UI)
            - UDP 1194 (OpenVPN Tunnel)
4. Click **Launch Instance**.

---

## 🔗 Step 2: Connect to EC2 via SSH

1. Locate your key pair Shift + Right click to open powershell 

```bash
ssh -i vpnsetup.pem root@ec2-26-166-230-00.ap-southeast-2.compute.amazonaws.com
```
This is just an example. If it doesnt work change `root` to `openvpn` then just say YES to everything and let the installation finish.
Default Username is openvpn and take note of the randomized password in the terminal.

2. Change your password

```bash
sudo passwd openvpn
```
Change your password to whatever you like

## 🌐 Step 3: Login to OpenVPN admin console

1. Login
```bash
https://<iPv4 Public IP>:943/admin
```


2. Under Configuration go to VPN settings.

3. Navigate to Routing, `Should client internet traffick be routed through the VPN` Change to YES Scroll down Save and Update Running Server.

## 💻 Step 4: Login to OpenVPN 

```bash
https://<iPv4 Public IP>:943
```

1. Login the same way as admin and choose which device you want the client to be installed.
2. Download and Install -> Launch client -> turn on VPN -> Input password


