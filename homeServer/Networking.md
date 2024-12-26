# IP
this inet value gives use the IP Address as well as the size of the subnet (in this case 24 bits)

**Network Address**: 192.168.1.0
**Host Address**: 192.168.1.155

- **inet 192.168.1.155/24 (in CIDR notation)**
	- ipv4 address
	- this is a '/24' address

- **inet6 fe80::9a92:b671:882a:b33a/64 (in CIDR notation)**
	- ipv6 address 
	- expressed in 128 bit units (num1::num2::...::numn)

# Gateway Address
the private IP address of the router itself. In our case, it is (usually it is the network address +1):

**Extracted From**: route4 default **via 192.168.1.1** metric 600
- **Gateway**: 192.168.1.1

