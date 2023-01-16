### What are some different types of Routes available in AWS?

In Amazon Web Services (AWS), a route table is used to control the flow of network traffic within a Virtual Private Cloud (VPC) or a subnet. 
A route table contains a set of rules, called routes, that specify where network traffic should be directed. 
There are several different types of routes that can be added to a route table, including:

* <b>Local route:</b> This is the default route that is automatically added to a route table. It directs all traffic for the VPC or subnet to the local network interface.

* <b>Internet gateway route:</b> This route directs all traffic for the VPC or subnet to the Internet gateway, allowing instances in the VPC or subnet to access the Internet.

* <b>Virtual private gateway route:</b> This route directs all traffic for the VPC or subnet to a virtual private gateway, allowing instances in the VPC or subnet to access a VPN connection.

* <b>Peering connection route:</b> This route directs all traffic for the VPC or subnet to a VPC peering connection, allowing instances in the VPC or subnet to access another VPC.

* <b>NAT gateway route:</b> This route directs all traffic for the VPC or subnet to a NAT gateway, allowing instances in a private subnet to access the Internet while preserving their private IP addresses.

* <b>VPN connection route:</b> This route directs all traffic for the VPC or subnet to a VPN connection, allowing instances in the VPC or subnet to access another network over a VPN.

* <b>Transit Gateway route:</b> This route directs all traffic for the VPC or subnet to a Transit Gateway, allowing instances in the VPC or subnet to access multiple VPCs and on-premises networks.

#### It is important to note that the traffic flow to each of these destinations, can be further fine-tuned via CIDR block, IP address or security group filtering



### What are some different types of record that can be added to a DNS Zone?

There are several different types of records that can be added to a DNS zone, including:

* <b>A record (Address record):</b> This record maps a hostname to an IPv4 address.

* <b>AAAA record (IPv6 address record):</b> This record maps a hostname to an IPv6 address.

* <b>CNAME record (Canonical Name record):</b> This record maps a hostname to another hostname.

* <b>MX record (Mail eXchange record):</b> This record maps a domain name to a list of mail servers responsible for handling email for that domain.

* <b>NS record (Name Server record):</b> This record maps a domain name to a list of name servers responsible for that domain.

* <b>PTR record (Pointer record):</b> This record maps an IP address to a hostname.

* <b>SOA record (Start of Authority record):</b> This record contains information about the DNS zone, including the primary name server, the email address of the domain administrator, and various settings for the zone.

* <b>TXT record (Text record):</b> This record is used to store any text-based information, such as SPF data, DKIM, DMARC, etc.

#### It is important to note that each record type has different attributes and is used for specific purposes, and depending on the DNS provider there can be more record types available.
