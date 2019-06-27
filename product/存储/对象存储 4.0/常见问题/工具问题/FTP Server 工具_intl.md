### How do I enable the FTP feature?

COS is a persistent storage that supports Web-based requests but does not provide native FTP access. Intermediate transfer is required to use the FTP protocol. **It is recommended to set up your service by using the [FTP Server tool](https://intl.cloud.tencent.com/document/product/436/7214) provided by Tencent Cloud.**
As an outdated protocol, FTP protocol is unable to verify data integrity, ensure transfer security, or be integrated with the CAM system. Therefore, it is not recommended to use the FTP protocol for access, and Tencent Cloud will provide support for the FTP protocol and intermediate transfer software. 
For data synchronization, it is recommended to use the [COS Migration tool](https://intl.cloud.tencent.com/document/product/436/15392) or the [COSCMD tool](https://intl.cloud.tencent.com/document/product/436/10976).

### What does the masquerade_address option in the configuration file do and when does it need to be configured?

If the FTP server runs in the PASSIVE mode (which is enabled generally when the FTP client is behind a NAT gateway) on a server with multiple ENIs, you need to bind a unique IP for response in PASSIVE mode using the masquerade_address option. 

For example, an FTP server has multiple IPs. The private IP is 10.XXX.XXX.XXX, and the public IP is 123.XXX.XXX.XXX. The client connects to the FTP server via the public IP and using the PASSIVE mode. If the FTP server does not specify that the masquerade_address is bound to the public IP, the server may respond to the client via the private IP when it is in a PASSIVE mode. In this case, the client can connect to the FTP server, but cannot get any data response from the server.

If you need to configure masquerade_address, it is recommended to set it to the IP used by the client for connecting to the server.

### After the masquerade_address option is correctly configured, I can log in to the FTP server normally, but when I run the FTP command for fetching data such as "list" or "get", the error "The server returns a non-routable address" or "ftp: connect: No route to host" occurs. How do I deal with it?

The most possible reason for this is the FTP server's iptables or firewall policy is configured to reject or drop all ICMP protocol packets. After receiving the data connection IP returned by the FTP server in the PASSIVE mode, the FTP client will send an ICMP packet first to verify the connectivity of the IP. In this case, the errors such as "The server returns a non-routable address" may occur.

Solution: Configure the iptables policy to only reject or drop the ICMP packet types you want to block. For example, if you only want to block the external ICMP packets of Ping type, you can change the policy to: iptables -A INPUT -p icmp --icmp-type 8 -s 0/0 -j [REJECT/DROP].
Alternatively, you can allow the IP of the client that will access the FTP server.

### Why is the uploaded part retained in COS when the upload of a large file is canceled halfway?

The FTP server for the latest version of COS provides full streaming upload feature. When you upload a large file, the cancellation or disconnection of the upload will trigger the completion of upload. In this case, COS considers that your data stream has been uploaded and combines the uploaded data into a complete file. If you want to resume the upload, you can upload the file with the same name to overwrite the original one, or delete the incomplete file manually and upload the file again.

### Why does a limit on the size of file to be uploaded need to be set in the FTP server configuration?

For a mulpart upload in COS, the maximum number of file chunks to be uploaded is 10,000, and the size of each file chunk is limited to 1 MB-5 GB. The purpose of imposing the limits is to reasonably calculate the size of a file chunk.
The FTP server supports uploading a single file less than 200 GB by default. But it is not recommended to set the limit to a too large value, because a larger file size limit will cause a larger buffer for file chunks during upload, thus increasing the consumption of your memory. Therefore, you are advised to set a reasonable file size limit as needed.

### What will happen if the size of a uploaded file exceeds the limit?

If the size of the uploaded file exceeds the limit set in the configuration file, the system returns an IOError exception and marks the error message in the log.

If you have any other questions, [submit a ticket](https://console.cloud.tencent.com/workorder/category) attached with the complete `cos_v5.log` log.

