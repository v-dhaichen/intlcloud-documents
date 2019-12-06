
The following describes the common server ports. For more information about service application ports for Windows, see the official Microsoft document ([Windows Service Overview and Network Port Requirements](https://support.microsoft.com/en-us/help/832017/service-overview-and-network-port-requirements-for-windows?spm=5176.7740724.2.3.omd4DB%3Fspm%3D5176.7740724.2.3.omd4DB)).

| Port number | Service | Description |
|---------|---------|---------|
| 21 | FTP | An open FTP server port for uploading and downloading. |
| 22 | SSH | Port 22 is the SSH port. It is used to remotely connect to Linux system servers in CLI mode. |
| 25 | SMTP | SMTP server's open port for sending emails.
| 80 | HTTP | This port is used for web services such as IIS, Apache, and Nginx to provide external access. |
| 110 | POP3 | Port 110 is open for the POP3 (email protocol 3) service. |
| 137, 138, 139 | NetBIOS protocol | Ports 137 and 138 are UDP ports for transferring files via My Network Places. <br>Port 139: Connections over port 139 attempt to access the NetBIOS/SMB service. This protocol is used for file and printer sharing on Windows and SAMBA. |
| 143 | IMAP | Port 143 is mainly used for Internet Message Access Protocol (IMAP) v2, a protocol for receiving emails akin to POP3. |
| 443 | HTTPS | Web browsing port. This is another type of HTTP that provides encryption and transmission over secure ports. |
| 1433 | SQL Server | Port 1433 is the default port for SQL Server. The SQL Server service uses two ports: TCP-1433 and UDP-1434. Port 1433 is used for SQL Server to provide external services, while port 1434 is used to respond the requester that which TCP/IP port is being used by SQL Server. |
| 3306 | MySQL | Port 3306, the default port for MySQL databases, is used by MySQL to provide external services. |
| 3389 | Windows Server Remote Desktop Services | Port 3389 is the service port for remote desktop on Windows 2000/2003 Server, through which you can connect to a remote server by using the Remote Desktop connection tool. |
| 8080 | Proxy port | Similar to port 80, port 8080 is used for the WWW proxy service for web browsing. Port number ":8080" is often appended to the URL when users visit a website or use a proxy server. In addition, after the Apache Tomcat web server is installed, the default service port is port 8080. |
