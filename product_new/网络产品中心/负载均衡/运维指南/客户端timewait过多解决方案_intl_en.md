## Background
When performing stress testing on CLB, you may encounter connection failures caused by too many client TIME-WAIT (all ports are occupied in short time). Below are reasons and solutions:

## Linux parameter description
**tcp_timestamps:** whether to enable TCP timestamps. A timestamp is negotiated in TCP three-way handshake. If either party does not support this parameter, it will not be used in this connection.
**tcp_tw_recycle:** whether to enable reuse of TCP TIME-WAIT state.
**tcp_tw_resuse:** when enabled, connections in TIME_WAIT state that exceeds 1 second can be directly reused.

## Cause Analysis
The client has too many TIME_WAIT because it proactively closes connections. When the client closes a connection, the connection will enter TIME_WAIT state and be reused after 60 seconds by default. In this case, you can enable `tcp_tw_recycle` and `tcp_tw_resuse` parameters to facilitate reuse of connections in TIME_WAIT state.
If `tcp_timestamps` is currently disabled on CLB, `tcp_tw_recycle` and `tcp_tw_resuse` parameters enabled by the client will not take effect, and connections in TIME_WAIT state cannot be quickly reused. The following describes some Linux parameters and reasons why `tcp_timestamps` cannot be enabled on CLB:

1. tcp_tw_recycle and tcp_tw_resuse only take effect when tcp_timestamps is enabled.

2. tcp_timestamps and tcp_tw_recycle cannot be enabled at the same time, because the public network client may fail to access the server through the NAT gateway. The reasons are as follows:

If both tcp_tw_recycle and tcp_timestamps are enabled, timestamp in the socket connect requests of the same source IP (same server) must be incremental within 60 seconds. Taking 2.6.32 kernel as an example, the details are as follows:

![](https://mc.qcloudimg.com/static/img/2199611fec3b323a7b8fd3bb38459913/Linux1.png)

> tmp_opt.saw_tstamp: this socket supports tcp_timestamp
sysctl_tw_recycle: tcp_tw_recycle has been enabled for this server
TCP_PAWS_MSL: 60s; the last TCP communication of the source IP occurred within 60 seconds
TCP_PAWS_WINDOW: 1; the timestamp of the last TCP communication of the source IP is greater than that of this TCP communication

3. On CLB (Layer-7), tcp_timestamps is disabled because the public network client may fail to access the server through the NAT gateway, as shown in the example below:

a. 	A quintuple is still in TIME_WAIT state. In the port allocation policy of the NAT gateway, the same quintuple is reused in twice the maximum segment lifetime (2MSL), and an SYN packet is sent.

b. When tcp_timestamps is enabled and the following two conditions are met, the SYN packet will be dropped (because timestamp option is enabled, and the packet is considered as old).
i. Timestamp of last time > Timestamp of this time
ii. 	Packets are received within 24 days (the timestamp field is 32-bit and the timestamp is updated once per 1 millisecond by default in Linux. The timestamp will wrap around after 24 days).
Note: This problem is more obvious on mobile devices because clients share limited public network IPs under the ISP's NAT gateway and a quintuple can be reused in 2MSL. The timestamps sent from different clients may not be incremental.
Taking 2.6.32 kernel as an example, the details are as follows:

![](https://mc.qcloudimg.com/static/img/6228a7dc25c670d4d2fbddc9ea400779/Linux2.png)

> rx_opt->ts_recent: timestamp of last time
rx_opt->rcv_tsval: timestamp received in this time
get_seconds(): current time
rx_opt->ts_recent_stamp: time when the previous packet was received

## Solution
If the client has too many TIME_WAIT, see below for solutions:

**1. HTTP uses non-persistent connections (Connection: close). In this case, CLB proactively closes the connection, and the client will not generate TIME_WAIT**.

**2. If the scenario requires a persistent connection, enable SO_LINGER option of the socket and use RST to close the connection to avoid the TIME_WAIT state and achieve fast port reuse**.
