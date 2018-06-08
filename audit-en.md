# The Block Producer Security Audit

> by SlowMist Security Team  & Joinsec Team
> 
> Thanks IMEOS.ONE for translation

#### [中文版](./audit.md)

## Contents

* [Audit Core Goals](#audit-core-goals)
* [Audit Core Direction](#audit-core-direction)
* [Audit Coverage](#audit-coverage)
	* [1. Block Producer Self Audit](#1-block-producer-self-audit)
		* [1.1 Architecture Audit](#11-architecture-audit)
		* [1.2 RPC Security Audit](#12-rpc-security-audit)
		* [1.3 Configuration Security Audit](#13-configuration-security-audit)
	* [2. Team Security Audit](#2-team-security-audit)
		* [2.1  Infrastructure Audit](#21-infrastructure-audit)
		* [2.2 BP vulnerability Audit](#22-bp-vulnerability-audit)
		* [2.3 Performance Audit under DDoS](#23-performance-audit-under-ddos)
* [Contributors](#contributors)

## Audit Core Goals

Auditing the security status of BP exposed on the public network to find the common security issues
Auditing the BP architecture performance under DDoS
Aimed on EOS, perform a custom payloads attack test to detecting the robustness of overll frame.

## Audit Core Direction

Finding vulnerabilities that could cause the entire BP nodes to stop blocking
The vulnerabilities that Single-point blocking attacks caused by architectural defects could lead to BP node failures
The vulnerabilities that service misconfiguration causes server to be remotely attacked and controlled
The vulnerabilities that BP's sensitive information (especially the server SSH connection private key leaks on GitHub) 

## Audit Coverage

In order to achieve the most efficient and the most comprehensive effect, block producer security audit give priority to with self-audit (many sensitive servers and operations should not be directly exposed to third parties and need to rely on BP to self-audit) and security team provides professional guidance and collaboration.

### 1. Block Producer Self Audit

Refer: [EOS BP Nodes Security Checklist](./README-en.md)

#### 1.1 Architecture Audit

1. Whether the BP's server is fully isolated from the external network to ensuring that if a malicious attack from the external network does not directly affect the BP server out of the block
1. Whether the BP's have multi-link design to prevents BP can not to synchronize with other BPs cause by single points of failure (or DDoS to single point)
1. Whether the BP has the necessary security hardening (such as whether to properly deploy high-prevention DDoS attacks in the periphery of some core communication nodes and proper deployment of HIDS)

#### 1.2 RPC Security Audit

1. Whether to restrict the RPC services for non-essential BP
1. If open RPC services, whether to disable unnecessary wallet_plugin、wallet_api_plugin and producer_api_plugin
1. Is SSL enabled on RPC

#### 1.3 Configuration Security Audit

1. Confirm whether configured of active multi-signature keys is correct
1. Whether to turn on logging, whether more security logging plug-ins, etc. under certain conditions
1. Whether the parameter configuration of max-clients is reasonable,  whether it is easiest to attacked by P2P connection full number of connections and could not be synchronized. 
1. Whether to start the BP program with non-root authority
1. Whether to change the default port of the SSH service, whether the server SSH is configured with a white list, and setting to allow only  login with key(encrypted key) and prohibit login with password


### 2. Team Security Audit

#### 2.1 Infrastructure audit

1. whether the  server provider is a quality supplier with security. Since building infrastructure security requires huge amounts of money and efforts,  if choose some small services, it is highly possible that the Internet service providers will cutdown the connection when server surfering hacks. Therefore, it is a very cost-effective and safe choice to stand on the shoulders of giants. After testing, UCloud, AWS, Google Cloud, etc. have very good anti-attack and post-attack resilience.
1. Performing security audit of the real open port service of  the BPC's  public network IP  will prevent the operator from exposing vulnerable points due to incorrect configuration of service and security rules.

#### 2.2 BP vulnerability audit

1. Audit the ability of nodes to counter full-network scanning and the ability to  hide real public network IP. For example,  whether the bp uses the default port configuration (e.g., use the default port 8888, 9876, or other ports like this kind, etc.) led to the vulnerability of exposing to entire network scanning, and easy to be  attacked (currently we already know some test nodes have encountered RPC scanning and malicious call).
1. Audit whether the sensitive information of node is leaked on the public network, such as on GitHub.
1. Whether the RPC port is capable of making malicious calls
1. If the BP node deploys other programs other than the main EOSIO program, vulnerability attack and defense audit is conducted for the third party programs.
1. Whether the node has settle down  a customized emergency response plan.

#### 2.3 Performance Audit under DDoS

1. Performing field testing against the  Layer4 level of p2p port, to test the ability of anti UDP Flood, anti TCP Flood, etc(including all kinds of mainstream reflex attack). Test the stability of nodes with real attack traffic.
1. Performing field testing against the  Layer7 level of RPC port to test the ability of anti-CC attracking. Detect the stability of the BP using a large number of attack nodes with high concurrent requests that consume server performance.

## Contributors

Special thanks to:

* HelloEOS
* EOS Asia
* EOSBIXIN
* EOS Pacific
* UnlimitedEOS
* EOS Cannon
* EOSpace
* Blockgenic
* EOSeco
* EOSLaoMao
* OneChain
* EOS Store
* EOS Beijing
* MotionEOS
* EOSvillage
* EOS AntPool

Thanks to these bps for participating in the node security test, they have accumulated valuable data for community safety.
