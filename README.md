# Secure Deployment of Nextcloud Web Server in Azure Cloud Environment

## SUMMARY
Deployed a Nextcloud web server within an Azure cloud environment, hosted in a screened subnet for enhanced security. The project commenced with the creation of a virtual network and a subnet, both protected by inbound and outbound rules using Network Security Groups. An Ubuntu server was then deployed within the subnet, with remote administration facilitated through the implementation of a Bastion service. Utilizing Bastion allowed secure SSH connections to the VM without exposing external ports to the internet. Furthermore, a public IP and DNS label were configured to enable access to the web server from the public internet. Additionally, the project included a risk assessment, identifying the top five risks in the network along with corresponding remediation strategies.
### The list of steps taken are given below:
 - Created a Resource Group
 - Created a Virtual Network and a subnet
 - Protected the subnet using a Network Security Group
 - Deployed Bastion to connect to a Virtual Machine
 - Created an Ubuntu Server Virtual Machine
 - Installed Nextcloud by connecting via SSH using Bastion
 - Published an IP
 - Created a DNS label

### Network Diagram
<img src="https://github.com/ibtesam5d/nextcloud/blob/main/Network%20Diagram.png"/>

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

