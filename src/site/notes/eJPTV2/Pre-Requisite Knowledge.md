---
{"dg-publish":true,"permalink":"/e-jptv-2/pre-requisite-knowledge/","title":"Networking Recap - eJPTv2","tags":["ejptv2"]}
---


---

## eJPTv2 Training Notes

### 1. **Introduction to IP and MAC Addresses**

#### **IP Addresses**
- **IPv4 Address**: 32-bit number, written in decimal format as four octets separated by periods (e.g., `192.168.1.1`).
- **IPv6 Address**: 128-bit number, written in hexadecimal format, separated by colons (e.g., `2001:0db8:85a3:0000:0000:8a2e:0370:7334`).

**Types of IP Communication:**
- **Unicast**: One-to-one communication.
- **Multicast**: One-to-many communication within a specified group.
- **Broadcast**: One-to-all communication within a network segment.

#### **MAC Addresses**
- Unique 48-bit identifier assigned to network interfaces for communications at the data link layer.
- Format: Six pairs of hexadecimal digits, separated by colons or hyphens (e.g., `00:1A:2B:3C:4D:5E`).

#### **IP vs. MAC Addresses**
- **IP Address**: Used for logical addressing and routing.
- **MAC Address**: Used for physical addressing within a local network.

### 2. **Classes of IP Addresses**

#### **Class A**
- **Range**: `1.0.0.0` to `126.0.0.0`
- **Default Subnet Mask**: `255.0.0.0` (`/8`)
- **Hosts per Network**: 16,777,214
- **Private Range**: `10.0.0.0` to `10.255.255.255`

#### **Class B**
- **Range**: `128.0.0.0` to `191.255.0.0`
- **Default Subnet Mask**: `255.255.0.0` (`/16`)
- **Hosts per Network**: 65,534
- **Private Range**: `172.16.0.0` to `172.31.255.255`

#### **Class C**
- **Range**: `192.0.0.0` to `223.255.255.0`
- **Default Subnet Mask**: `255.255.255.0` (`/24`)
- **Hosts per Network**: 254
- **Private Range**: `192.168.0.0` to `192.168.255.255`

#### **Class D (Multicast)**
- **Range**: `224.0.0.0` to `239.255.255.255`

#### **Class E (Experimental)**
- **Range**: `240.0.0.0` to `255.255.255.255`

### 3. **Private and Public IP Addresses**

#### **Private IP Addresses**
- Used for internal network communication, not routable on the public internet.
- **Ranges**:
  - **Class A**: `10.0.0.0` to `10.255.255.255`
  - **Class B**: `172.16.0.0` to `172.31.255.255`
  - **Class C**: `192.168.0.0` to `192.168.255.255`

#### **Public IP Addresses**
- Routable on the public internet, globally unique.
- Assigned by IANA and regional internet registries.

### 4. **CIDR Notation**

#### **CIDR (Classless Inter-Domain Routing)**
- Allows for more flexible IP address allocation and routing.
- **Notation**: `IP address/prefix length` (e.g., `192.168.1.0/24`).

**Examples**:
- **/24**: 255.255.255.0 (256 addresses)
- **/12**: 255.240.0.0 (1,048,576 addresses)
- **/16**: 255.255.0.0 (65,536 addresses)

### 5. **Subnetting**

#### **Concept of Subnetting**
- Divides a large network into smaller sub-networks.
- Improves IP address allocation, network performance, and security.

#### **Subnet Mask**
- **/24**: 255.255.255.0
- **/16**: 255.255.0.0
- **/12**: 255.240.0.0

#### **Benefits of Subnetting**
- **Efficient IP Address Allocation**: Reduces IP address waste.
- **Improved Performance**: Limits broadcast traffic to subnets.
- **Enhanced Security**: Isolates network segments.
- **Simplified Management**: Easier network management.

### 6. **Subnetting Example**

#### **University Network Example**
- **Network**: `192.168.1.0/24`
- **Subnets**:
  - **Subnet 1**: `192.168.1.0/26` (64 IPs)
  - **Subnet 2**: `192.168.1.64/26` (64 IPs)
  - **Subnet 3**: `192.168.1.128/26` (64 IPs)
  - **Subnet 4**: `192.168.1.192/26` (64 IPs)

### 7. **Subnetting in Penetration Testing**

#### **Enumeration**
- **Network Mapping**: Identifying subnets helps map network structure.
- **Host Discovery**: Targeting specific subnets reveals live hosts.

#### **Penetration Testing**
- **Scope Definition**: Defines the scope of the test.
- **Segmentation Testing**: Assesses network segmentation security.
- **Traffic Analysis**: Monitors traffic within and between subnets.
- **Target Identification**: Focuses on high-value targets in specific subnets.

---

### Summary

- **IP Addresses**: Logical addresses for network communication.
- **MAC Addresses**: Physical addresses for local network communication.
- **IP Classes**: Class A, B, C for different network sizes; Class D for multicast; Class E for experimental.
- **Private vs. Public IPs**: Private for internal use; public for internet-facing devices.
- **CIDR Notation**: Flexible IP allocation and routing notation.
- **Subnetting**: Divides large networks into smaller subnets for better management, performance, and security.
- **Application in Penetration Testing**: Crucial for network mapping, host discovery, and assessing network segmentation.

These notes cover the foundational concepts you'll need for your eJPTv2 course. If you have any more questions or need further explanations, feel free to ask!