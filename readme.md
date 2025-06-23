## April University Wireless Networking Project (Cisco Packet Tracer)

## Overview

This project simulates a university with three campuses located in different geographic areas. Each campus provides secure wireless access to students using the same SSID and password across all locations.

Once a student connects to the wireless network on any campus, they can automatically connect at any other campus without entering credentials again. This setup mimics real-world enterprise Wi-Fi roaming using WPA2-Personal security.

This project was built in **Cisco Packet Tracer** and demonstrates:
- Secure wireless LAN with WPA2 encryption
- Wireless roaming simulation using consistent configuration
- WAN links between campuses using serial connections
- Basic static routing between networks
- DHCP for automatic IP address allocation



## Devices and Components Used

For each of the three campuses:
- 1 Cisco 2811 Router
- 1 Cisco 2960 Switch
- 1 Cisco WRT300N Wireless Router
- 1 Modular Laptop (with WPC300N wireless card)
- 1 Server for DHCP 

WAN connections:
- Serial DCE cables between routers



## Wireless Network Configuration

All wireless routers use the following settings:

- **SSID:** UniWiFi  
- **Security Mode:** WPA2-Personal  
- **Encryption:** AES  
- **Passphrase:** UniConnect2025!  

---

## IP Addressing Scheme

| Campus    | LAN Network     | Router LAN IP   | Wireless Router LAN IP | DHCP Pool Range               |
|-----------|-----------------|-----------------|------------------------|-------------------------------|
| Campus A  | 192.168.10.0/24  | 192.168.10.254   | 192.168.10.1        | 192.168.10.10 – 192.168.10.100 |
| Campus B  | 192.168.20.0/24  | 192.168.20.254   | 192.168.20.1        | 192.168.20.10 – 192.168.20.100 |
| Campus C  | 192.168.30.0/2   | 192.168.30.254   | 192.168.30.1        | 192.168.30.10 – 192.168.30.100 |

| WAN Link         | IP Range         | 
|------------------|------------------|
| Campus A ↔ B     | 10.0.0.0/30      |
| Campus B ↔ C     | 10.0.0.4/30      |

---

## Step-by-Step Setup Instructions

### 1. Add the Wireless Laptop

1. Go to **End Devices** > drag **Laptop** to the workspace.
2. Click the laptop > go to the **Physical** tab.
3. Turn off the laptop using the power button.
4. Insert the **WPC300N** wireless card into the **left-side slot**.
5. Turn the laptop back on.
6. Go to **Desktop** > **PC Wireless** > connect to `UniWiFi`.
7. Enter the password: `UniConnect2025!`.

### 2. Configure the WRT300N Wireless Router

1. Click on the WRT300N router.
2. Under the **GUI** tab:
   - Set **SSID** to `UniversityWiFi`
   - Set **Security Mode** to WPA2-Personal
   - Set password/passphrase to `UniConnect2025!`
   - Optional: Set DHCP to enabled and define your DHCP pool.

3. Under **LAN settings**:
   - IP address: `192.168.X.1` (X = 10, 20, 30 based on campus)
   - Subnet mask: `255.255.255.0`

4. Connect the **Ethernet port of WRT300N** to **Switch port Fa0/1** using a copper straight-through cable.


## 3. Configure Each Campus Router

## Campus A 

interface FastEthernet0/0
ip address 192.168.1.254 255.255.255.0
no shutdown
exit

interface Serial0/0/0
ip address 10.0.0.1 255.255.255.252
clock rate 64000
no shutdown
exit

ip route 192.168.2.0 255.255.255.0 10.0.0.2
ip route 192.168.3.0 255.255.255.0 10.0.0.2

## Campus B

enable
configure terminal
interface FastEthernet0/0
ip address 192.168.2.254 255.255.255.0
no shutdown
exit
interface Serial0/0/0
ip address 10.0.0.2 255.255.255.252
no shutdown
exit
interface Serial0/0/1
ip address 10.0.0.5 255.255.255.252
clock rate 64000
no shutdown
exit

ip route 192.168.1.0 255.255.255.0 10.0.0.1
ip route 192.168.3.0 255.255.255.0 10.0.0.6

## Campus C

enable
configure terminal
interface FastEthernet0/0
ip address 192.168.3.254 255.255.255.0
no shutdown
exit
interface Serial0/0/1
ip address 10.0.0.6 255.255.255.252
no shutdown
exit

ip route 192.168.1.0 255.255.255.0 10.0.0.5
ip route 192.168.2.0 255.255.255.0 10.0.0.5

## Testing

  - Ensure laptops get IPs via DHCP.

  - Ping between campuses.

  - Roam laptops by deleting and re-adding them on another campus.
