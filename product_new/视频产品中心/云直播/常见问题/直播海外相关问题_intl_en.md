### How to configure LVB push acceleration outside Mainland China?
You can go to the LVB Console > Domain Management, where the default push domain name is pre-configured with push acceleration outside Mainland China. If you want to use your own push domain name, add one and then complete CNAME-related operations as instructed to configure acceleration outside Mainland China for it.
		
### How to accelerate push for a playback domain name outside Mainland China?
Go to the LVB Console > Domain Management > Add Playback Domain, where you can select one of the two acceleration types as needed: global acceleration, which requires the domain name to have obtained ICP filing in Mainland China; otherwise, configuration will fail; acceleration outside Mainland China, which can be configured just as instructed, but playback is unavailable in Mainland China in this case.
	 
### How to check whether acceleration outside Mainland China has been configured for my domain name?
You can use a server outside Mainland China to run the `ping` command on the push and playback domain names; if the server IP is a nearest node IP, acceleration outside Mainland China has been configured. You can also use [this tool](https://tools.ipip.net/dns.php) to test your domain name and check whether the resolved IP corresponds to the acceleration region.
	 
### How to troubleshoot failures of LVB playback outside Mainland China?
Currently, playback outside Mainland China supports HTTP-FLV, HLS, and RTMP. You can troubleshoot playback issues in the following way:
1. Is the domain name pingable?
If not, check the current network environment.
2. If the obtained HTTP status code is 200?
	If it is not 200, there are several possible reasons for the failure. Generally, if the status code is 403, which indicates authentication failure, you need to check whether the calculation format of hotlink protection complies with the requirements. If the status code is 404, which indicates that the stream played back is not on the platform, you need to check whether the push is normal. For other error codes, submit a ticket for assistance.
	 
### What protocols does LVB push outside Mainland China support?
Currently, only RTMP is supported.
	 
### Does LVB playback outside Mainland China support HTTPS?
Yes. Go to the LVB Console > Domain Management > Playback Domain Name > Management > Advanced Configuration > HTTPS Configuration, where you can add an HTTPS certificate to the domain name for which you want to configure HTTPS pull.
	 
### Can I modify the region of LVB playback acceleration outside Mainland China?
Yes. You can do so in the LVB Console > Domain Management. It takes about 15 minutes for the change to take effect.
	 
### Does push acceleration outside Mainland China support HttpDNS scheduling?
Yes, but you need to [submit a ticket](https://console.cloud.tencent.com/workorder/category) for configuration in the backend.
