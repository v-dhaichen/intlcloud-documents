Some attackers may record real server IP history, and the exposed IPs allow them to bypass Anti-DDoS Advanced and directly attack your real server. In this case, we recommend that you change the actual real server IP. You can refer to this document before changing the real server IP to check the risk factors to prevent the new IP from disclosure.

## Checklist
### Check DNS resolution history
Check all the DNS resolution history of the attacked real server IP, including resolution records of sub-domain names, MX (Mail Exchanger) records of mail servers, and NS (Name Server) records. Make sure all these records are configured to the Anti-DDoS Advanced IP so that the DNS is not resolving to the new real server IP.

### Check for information disclosure and command execution vulnerabilities
- Check websites or business systems for possible information disclosure vulnerabilities, such as phpinfo() disclosure and sensitive information leakage on Github.
- Check websites or business systems for command execution vulnerabilities.

### Check for Trojans and backdoors
Check the real server for potential Trojans, backdoors and other hidden dangers.

## Other Suggestions
- To prevent attackers scanning C range or other similar IP range, we do not recommend using the same IP or an IP similar to the old IP as the new real server IP. 
- We recommend preparing the backup linkage and the backup IP in advance.
- We recommend that setting the scope of access sources to prevent malicious scanning.
- We recommend that you refer to [Real Server-based Defense Scheduling Solution](https://intl.cloud.tencent.com/document/product/297/15564) and apply the solution based on your actual demands.
