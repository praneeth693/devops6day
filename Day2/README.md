# 🌌 Deploying a Static Web App on AWS EC2

This repository showcases the complete process I followed to deploy a static HTML login page on an **AWS EC2 Ubuntu instance**. It walks through launching the instance, configuring security, setting up Apache2, and deploying a basic HTML file.

---

## 🚀 What I Did

- Launched and configured an Ubuntu EC2 instance
- Created key pairs and security groups
- Connected to the instance using PuTTY
- Installed and configured Apache2 web server
- Deployed a static HTML login page

---

## 🚪 Launch EC2 Instance

1. Go to EC2 Dashboard on AWS
2. Launch a new instance with the following:
   - **Name**: MyStaticWebApp
   - **OS**: Ubuntu
   - **Instance Type**: t2.small (you can change as per app size)
3. Create a **key pair**:
   - Choose format: `.ppk` for PuTTY
   - Select RSA and download it
4. Create a **security group**:
   - Allow port **80** (HTTP) and **22** (SSH)
5. Choose storage (e.g., 15GB)
6. Launch the instance

---

## 🔑 Connect via PuTTY (Windows)

1. Download and install PuTTY
2. Open PuTTY and do the following:
   - **Host Name**: Use your EC2 public IP
   - Under `SSH > Auth`, **browse your .ppk key file**
   - Click `Open` and accept security prompt
3. Once connected, switch to root:

```bash
sudo -i
```

4. Update the server:

```bash
apt update -y
```

---

## 🏢 Install Apache2 and Setup Web Server

```bash
apt install apache2 -y
```

Check status:

```bash
service apache2 status
```

If inactive, restart Apache:

```bash
service apache2 restart
```

Navigate to the default root directory:

```bash
cd /var/www/html
```

Remove default page and create new index:

```bash
rm index.html
nano index.html
```

Copy-paste HTML login page code (from [W3Schools](https://www.w3schools.com)) into the file. Use:

- Press `i` to insert text
- Paste your HTML code
- Save and exit using:

```bash
ESC + :wq + Enter
```

Restart Apache again:

```bash
service apache2 restart
```

---

## 🔍 View Your Static Web App

Open your browser and go to:

```
http://<your-ec2-public-ip>
```

Make sure your EC2 security group has port **80** enabled to allow traffic.

You should now see your **HTML login page** hosted from your EC2 instance! 🌐

---

## 🙌 Summary

Through this project, I learned how to:

- Use EC2 for web hosting
- Configure cloud instances securely
- Host and serve static content using Apache2
