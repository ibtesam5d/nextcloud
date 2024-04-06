# Deploying Web Server in Screened Subnet with Azure

## SUMMARY
In this project a Nextcloud web server is deployed in a screened subnet using Azure cloud. Project started by creating a virtual network followed by a subnet. Subnet is protected by inbound and outbound rules by using Network Security Groups. An ubuntu server is deployed in a VM within the subnet. For remote administration of the server, Bastion service is used. Bastion allows connection to the VM using SSH without exposing an external port to the internet. Lastly, created a public IP and a DNS Label to access the web server through the public internet. This report also lists top five risks present in the network and remediations for each risk.

### The list of steps taken are given below:
 - Created a Resource Group
 - Created a Virtual Network and a subnet
 - Protected the subnet using a Network Security Group
 - Deployed Bastion to connect to a Virtual Machine
 - Created an Ubuntu Server Virtual Machine
 - Installed Nextcloud by connecting via SSH using Bastion
 - Published an IP
 - Created a DNS label

## RISKS and REMEDIATIONS
- Web servers in a screened subnet possesses high risk. Vulnerabilities can allow a threat actor to compromise the server and move into the internal network. After installation of the server, a vulnerability scan must be performed to find any existing vulnerabilities and implement controls accordingly.
- A self signed certificate is used here for a public facing web frontend. This will cause browser certificate error as the user's browser will not recognize our certificates. This will disrupt business operations and can cause significant financial and reputational damage. A commercially available certificate by trusted CA should be implemented.
- No endpoint security service is installed other than the secure boot and TPM. This makes the web server vulnerable to malware infection. An anti-malware solution needs to be installed.
- No intrusion detection and prevention capabilities present in the network to identify and block intrusion. A network based IDS/IPS will solve this issue.
- There is no visibility to the network to understand and analyze network traffic. A Security Information and Event Management (SIEM) tool can provide a clear picture to the network while alerting on any network event.
While it is not possible to identify every risk present in the network, it is important to constantly monitor the network and implement layered controls (defense in depth) to safeguard our infrastructure.

## CONCLUSION
This project successfully deployed an internet facing web server in a screened subnet within a private network. This mimics the real-world enterprise network infrastructure. Administration to the web server is securely done through the company intranet, in this case the AzureBastionSubnet over SSH. Also, the internal network is protected from the screened subnet with Network Security Group. TCP traffic from the public internet is allowed only over encrypted channels into the web server and data at rest is encrypted in the storage of the server.

This project followed best practices to design and creation of virtual networks, subnets, firewall configurations and secure protocols. After the project is done, unused resources are deprovisioned safely. This secure deprovisioning includes removal of Network Interfaces and SSH keys along with any user credentials, firewall rules and DNS label created.

