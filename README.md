# FTP-Server-Setup-using-vsftpd-on-RHEL
End-to-end FTP server implementation on RHEL using vsftpd with secure file transfer capabilities.

🧠 Overview

Configured a fully functional FTP server using vsftpd on Red Hat Linux to enable seamless file transfer between a server and a client system.
- ✔ Supports file download & upload
- ✔ Uses anonymous authentication
- ✔ Demonstrates real-world Linux server setup

🏗️ Architecture

The setup follows a basic client-server model within a local network environment:

- FTP Server:
    - A Red Hat Linux system running vsftpd, responsible for hosting and managing shared files.
    - It listens on port 21 and handles all incoming FTP requests.

- Client Machine:
    - A separate system that connects to the FTP server using the FTP protocol to access files.

- Shared Directory:
The /var/ftp/pub directory acts as the central location for file exchange, where:
    - Files can be downloaded by clients
    - Uploads are enabled using a separate directory (upload)

- Security Layers:

    - SELinux controls application-level access
    - Firewall (iptables) controls network-level access
      
⚙️ Tech Stack

- 💻 Red Hat Linux
- 📦 vsftpd (FTP Server)
- 🔐 SELinux
- 🔥 iptables (Firewall)

⚡ Key Features

- ✨ Anonymous FTP Login
- 📥 File Download Support
- 📤 File Upload Support
- 🔐 Permission-based Access Control
- ⚙️ Service Management & Configuration

🔧 Quick Setup
- 1️⃣ Install & Start Service
  
        - yum install vsftpd -y
        - service vsftpd start
  
- 2️⃣ Configure Security (as shown in setup)
  
      - setenforce 0
      - getenforce   # Output: Permissive

      * service iptables stop

          - ✔ SELinux set to permissive
          - ✔ Firewall stopped successfully

- 3️⃣ Create File for Download (as in image)
cd /var/ftp/pub
cat > download
Hello

✔ File download created with sample content

📥 Download Files (Client Side)
ftp 192.168.125.140

Login:

- Name: anonymous
- Password: (press Enter)

Commands used:

- ls
- cd pub
- ls
- get download

- ✔ File download successfully retrieved
- ✔ Transfer completed (6 bytes)

📤 Enable Upload

- Step 1: Create Upload Directory
  
        - cd /var/ftp/pub
        - mkdir upload
        - chmod 777 upload
        - chown ftp:ftp upload
  
- Step 2: Update Configuration
  
        - vim /etc/vsftpd/vsftpd.conf

- Enable:

      - anon_upload_enable=YES
  
- Step 3: Restart Service
  
        - service vsftpd start
  
- 📤 Upload Files (Client Side)
  
        - ftp 192.168.125.140
        - cd pub
        - ls
        - cd upload
        - put upload_files

- ✔ File uploaded successfully
- ✔ Transfer completed (13 bytes)

🧪 Results

- ✔ Client successfully connected to server
- ✔ File download downloaded successfully
- ✔ Upload directory accessed
- ✔ File uploaded successfully
- ✔ End-to-end FTP workflow verified

💡 Learnings

- 🐧 Linux service configuration
- 🔐 Security layers (SELinux vs Firewall)
- 📂 File permissions (chmod, chown)
- 🌐 Client-server communication

🎯 Conclusion

Built a working FTP server environment capable of handling both file downloads and uploads using anonymous access. This setup reflects a real-world Linux server configuration and strengthens understanding of networking and system administration.
