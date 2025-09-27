# Host-a-Website-with-Apache-on-Ubuntu-VM
This lab focuses on hosting a simple website using the Apache web server on an Ubuntu virtual machine. You will create a basic HTML page, test it from your Windows host browser, and secure it with HTTPS using a self-signed SSL certificate.

## 📖 Description
This lab focuses on hosting a simple website using the Apache web server on an Ubuntu virtual machine. You will create a basic HTML page, test it from your Windows host browser, and secure it with HTTPS using a self-signed SSL certificate.

## 🖥️ Environments Used
- **Host OS:** Windows 11  
- **Guest OS:** Ubuntu  
- **Virtualization:** VirtualBox  

## 🛠️ Lab Walkthrough

### 🔹Step 1: Install Apache Web Server
---
**Description:**  
Install the OpenSSH server on Ubuntu and ensure the service is running.

### 🖥️ Commands to Run (Ubuntu Linux Terminal)
<details>
  <summary>📌Show Commands  </summary>

  ```bash
# Update system packages
sudo apt update && sudo apt upgrade -y

# Install Apache2 package
sudo apt install apache2 -y

# Enable and start Apache service
sudo systemctl enable apache2
sudo systemctl start apache2

# Check Apache status
sudo systemctl status apache2
```
 </details>
  <details>
    <summary>Click to view results✅</summary>
<p align="center">✅Execution of commands resulted in Apache being active and running✅!
<img src="https://i.imgur.com/R2o23zO.png" height="60%" width="60%" alt="SSH Setup"/>
 </details>

### 🔹Step 2 – Create a Simple HTML Page
---
Set up a basic index.html to confirm Apache is serving content.  



### 🖥️ Commands to Run (Ubuntu Linux Terminal)

<details>
<summary>📌 Show Commands</summary>

```bash
echo "<h1>Hello from Apache</h1>" | sudo tee /var/www/html/index.html
```
</details>
  <details>
    <summary>Click to view results✅</summary>
   ✅ This instantly writes an HTML file with your test message. <p>
  <p align="center">
<img src="https://i.imgur.com/WOWCeKI.png" height="60%" width="60%" alt="SSH Setup"/>
 </details>
 
### 🔹Step 3 - Test Website from VM 
---
Access the web page to confirm Apache is serving content. 

### 🖥️ Steps to Take:

Open a browser inside the VM and type in browser:
 ```
http://localhost
```

 <details>
  <summary>Click to view results✅</summary> 
This is the message you should see if successful: <p>
  <p align="center">
<img src="https://i.imgur.com/40RR7A9.png" height="60%" width="60%" alt="SSH Setup"/>    <p>
   <p>

 
### 🔹Step 4: Enable HTTPS with Self-Signed SSL

Add basic hardening by configuring Apache to serve HTTPS traffic using a self-signed SSL certificate.


---
### 🖥️ Commands to Run (Ubuntu VM)
<details>
  <summary>📌Show commands</summary>

```bash
# Enable SSL module
sudo a2enmod ssl

# Create a self-signed SSL certificate (valid for 365 days)
sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 \
-keyout /etc/ssl/private/apache-selfsigned.key \
-out /etc/ssl/certs/apache-selfsigned.crt

# Create a new Apache SSL configuration file
sudo nano /etc/apache2/sites-available/self-signed.conf

# Enable the SSL site config
sudo a2ensite self-signed.conf

# Restart Apache
sudo systemctl restart apache2

```
</details>
 <details>
  <summary>Click to view results✅</summary> 
<p>
When successful, Proceeding shows the  Hello from Apache page, but over HTTPS.:<p>
  <p align="center">
<img src="https://i.imgur.com/kDI39fI.png" height="60%" width="60%" alt="SSH Setup"/>
    <p>
</details>

📝 Closing Notes

In this lab, I successfully hosted a website on Apache inside my Ubuntu VM:

✅ Installed and enabled Apache.
✅ Created and served a custom index.html page.
✅ Tested the page inside the VM’s browser.
✅ Configured HTTPS with a self-signed SSL certificate.

💡 Key Takeaways

Apache is a widely used web server for hosting websites.

The default web root on Ubuntu is /var/www/html/.

Self-signed certificates allow encryption, but browsers will warn because they aren’t trusted.

HTTPS setup is a key first step toward securing web traffic.

