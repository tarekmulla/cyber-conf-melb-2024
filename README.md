# Build machine learning-based network intrusion detection system

This repository hosts the code featured in a [workshop](https://melbourne2024.cyberconference.com.au/workshops/workshop-QuZeh0r1Hn) at the [2024 Australian Cyber Conference in Melbourne](https://melbourne2024.cyberconference.com.au/). The [workshop](https://melbourne2024.cyberconference.com.au/workshops/workshop-QuZeh0r1Hn) highlights techniques for building a Machine Learning-powered Network Intrusion Detection System.


## Dataset Source

The dataset used in this project is called **UNSW-NB15**, it was generated using the IXIA PerfectStorm tool within the _Cyber Range Lab_ at the _Australian Centre for Cyber Security (ACCS)_ ([Moustafa and Slay, 2019](#moustafa_slay_1)). It features a hybrid mix of `normal` network activities and `attack` behaviours.

The dataset was collected through a study at the [University of New South Wales (UNSW)](https://www.unsw.edu.au/), using the `Tcpdump` tool to capture `100 GB` of raw traffic. It is officially available on their dataset library website [here](https://unsworks.unsw.edu.au/entities/dataset/4dc0e35c-6196-4c9d-945a-c50b981e5955).

The table below outlines the features present in the dataset.

| **Name of the Feature** | **Data Type** | **Units** | **Brief Description**|
|:----:|:----:|:----:|:----:|
|id               |numeric            |NA        |Record Identification number                                                                                                                     |
|dur              |numeric            |sec       |Record total duration                                                                                                                            |
|proto            |nominal categorical|NA        |Transaction protocol (`udp`, `arp`, `tcp`, `ospf`, etc..)                                                                                        |
|service          |numeric            |NA        |Transaction service, `http`, `ftp`, `smtp`, `ssh`, `dns`, `ftp-data` ,`irc`  and `-` if not much used service                                    |
|state            |nominal categorical|NA        |Transaction state and its dependent protocol, e.g. `ACC`, `CLO`, `CON`, `ECO`, `ECR`, `FIN`, `INT`, etc. , and `-` (if not used state)           |
|spkts            |numeric            |packets   |Source to destination packet count                                                                                                               |
|dpkts            |numeric            |packets   |Destination to source packet count                                                                                                               |
|sbytes           |numeric            |bytes     |Source to destination transaction bytes                                                                                                          |
|dbytes           |numeric            |bytes     |Destination to source transaction bytes                                                                                                          |
|rate             |numeric            |NA        |The rate of the connection time                                                                                                                  |
|sttl             |numeric            |sec       |Source to destination time to live value                                                                                                         |
|dttl             |numeric            |sec       |Destination to source time to live value                                                                                                         |
|sload            |numeric            |bits/sec  |Source bits per second                                                                                                                           |
|dload            |numeric            |bits/sec  |Destination bits per second                                                                                                                      |
|sloss            |numeric            |packets   |Source packets retransmitted or dropped                                                                                                          |
|dloss            |numeric            |packets   |Destination packets retransmitted or dropped                                                                                                     |
|sinpkt           |numeric            |mSec      |Source interpacket arrival time                                                                                                                  |
|dinpkt           |numeric            |mSec      |Destination interpacket arrival time                                                                                                             |
|sjit             |numeric            |mSec      |Source jitter                                                                                                                                    |
|djit             |numeric            |mSec      |Destination jitter                                                                                                                               |
|swin             |numeric            |NA        |Source TCP window advertisement value                                                                                                            |
|stcpb            |numeric            |NA        |Source TCP base sequence number                                                                                                                  |
|dtcpb            |numeric            |NA        |Destination TCP base sequence number                                                                                                             |
|dwin             |numeric            |NA        |Destination TCP window advertisement value                                                                                                       |
|tcprtt           |numeric            |sec       |TCP connection setup round-trip time, the sum of 'synack' and 'ackdat'.                                                                          |
|synack           |numeric            |sec       |TCP connection setup time, the time between the SYN and the SYN_ACK packets.                                                                     |
|ackdat           |numeric            |sec       |TCP connection setup time, the time between the SYN_ACK and the ACK packets.                                                                     |
|smean            |numeric            |NA        |Mean of the flow packet size transmitted by the src                                                                                              |
|dmean            |numeric            |NA        |Mean of the flow packet size transmitted by the dst                                                                                              |
|trans_depth      |numeric            |NA        |Represents the pipelined depth into the connection of http request/response transaction                                                          |
|response_body_len|numeric            |NA        |Actual uncompressed content size of the data transferred from the server's http service.                                                         |
|ct_srv_src       |integer            |connection|No. of connections that contain the same service and source address in 100 connections according to the last time.                               |
|ct_state_ttl     |numeric            |NA        |No. for each state according to specific range of values for source/destination time to live.                                                    |
|ct_dst_ltm       |integer            |connection|No. of connections of the same destination address in 100 connections according to the last time.                                                |
|ct_src_dport_ltm |integer            |connection|No of connections of the same source address and the destination port in 100 connections according to the last time.                             |
|ct_dst_sport_ltm |integer            |connection|No of connections of the same destination address and the source port in 100 connections according to the last time.                             |
|ct_dst_src_ltm   |integer            |connection|No of connections of the same source and the destination address in in 100 connections according to the last time.                               |
|is_ftp_login     |binary             |NA        |If the ftp session is accessed by user and password then `1` else `0`.                                                                           |
|ct_ftp_cmd       |integer            |NA        |No of flows that has a command in ftp session.                                                                                                   |
|ct_flw_http_mthd |numeric            |NA        |No. of flows that has methods such as Get and Post in http service.                                                                              |
|ct_src_ltm       |integer            |connection|No. of connections of the same source address in 100 connections according to the last time.                                                     |
|ct_srv_dst       |integer            |connection|No. of connections that contain the same service and destination address in 100 connections according to the last time.                          |
|is_sm_ips_ports  |binary             |NA        |If source equals to destination IP addresses and port numbers are equal, this variable takes value `1` else `0`.                                 |
|attack_cat       |nominal categorical|NA        |The attack category. Has nine categories `Fuzzers`, `Analysis`, `Backdoors`, `DoS Exploits`, `Generic`, `Reconnaissance`, `Shellcode` and `Worms`|
|label            |binary             |NA        |`0` for normal and `1` for attack records                                                                                                        |

---

## References

1. Moustafa, N., & Slay, J. (2019). _The UNSW-NB15 dataset_. Sydney; https://unsworks.unsw.edu.au/entities/dataset/4dc0e35c-6196-4c9d-945a-c50b981e5955.

2. Moustafa, N., & Slay, J. (2015). UNSW-NB15: A comprehensive data set for network intrusion detection systems (UNSW-NB15 Network Data Set). _2015 Military Communications and Information Systems Conference (MilCIS)_. https://doi.org/10.1109/milcis.2015.7348942
