
Proxy Server Setup and Monitoring with Squid, Webmin, and Calamaris

1. Update Your System
Update the package list:

```bash
sudo apt update
```

2. Install Squid
Install Squid with this command:

```bash
sudo apt install -y squid
```

3. Configure Squid
Open Squid Configuration File

```bash
sudo nano /etc/squid/squid.conf
```

Set Up Access Control and Port

- Ensure the line `http_port 3128` is active (uncommented).
- Add these lines to allow access from your local network (adjust 192.168.1.0/24 if needed):

```conf
acl localnet src 192.168.1.0/24
http_access allow localnet
http_access deny all
```

To block specific websites, add this:

```conf
acl blocked_sites dstdomain .facebook.com .example.com
http_access deny blocked_sites
```

Save and Exit (Press Ctrl + X, then Y, and Enter).

4. Restart Squid
Apply the configuration:

```bash
sudo systemctl restart squid
```

5. Install Webmin for Squid Management and Monitoring
- Download Webmin

```bash
wget http://prdownloads.sourceforge.net/webadmin/webmin_1.991_all.deb
```

- Install Webmin

```bash
sudo dpkg --install webmin_1.991_all.deb
```

- Access Webmin
  - Open a browser and go to https://your_server_ip:10000.
  - Log in to Webmin (using your server's username and password) to monitor and configure Squid through the Squid module.

6. Install Calamaris for Log Analysis
- Install Calamaris

```bash
sudo apt install -y calamaris
```

- Run Calamaris on Squid Logs
  - Use this command to analyze logs manually:

```bash
sudo calamaris -a /var/log/squid/access.log
```

You can also configure it to generate daily reports automatically.

This setup now includes Squid with Webmin for a user-friendly GUI to monitor and configure the proxy, along with Calamaris for generating Squid log reports to analyze usage and performance.

