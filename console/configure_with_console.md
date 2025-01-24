To configure a FortiGate firewall using the console, you'll typically use the CLI (Command Line Interface) to perform various configurations. Here's a general guide to get you started:

### Prerequisites:
- Console cable (often a USB to serial cable) to connect to the FortiGate device.
- Terminal emulator software (like PuTTY, Tera Term, or minicom) installed on your computer.
- Basic understanding of networking concepts.

### Step-by-Step Configuration:

1. **Connect to the FortiGate Console Port:**
   - Use a serial console cable to connect the FortiGate firewall's console port to your PC.
   - Launch a terminal emulator like PuTTY, set it to serial mode, and configure it to match the FortiGate's default serial settings:
     - Baud rate: 9600
     - Data bits: 8
     - Parity: None
     - Stop bits: 1
     - Flow control: None

2. **Login to the FortiGate:**
   - After establishing the console connection, power on the FortiGate device.
   - You'll be prompted with a login screen.
     - Username: `admin`
     - Password: (leave this blank by default, just press Enter)

3. **Basic Configuration Tasks:**
   You can now begin configuring the FortiGate firewall.

   #### Set the Hostname:
   ```bash
   config system global
   set hostname Your-FortiGate-Hostname
   end
   ```

   #### Set the Administrator Password:
   To secure the device, set an admin password:
   ```bash
   config system admin
   edit admin
   set password YourNewPassword
   next
   end
   ```

   #### Configure Interfaces:
   To configure the network interfaces, you'll need to assign IP addresses.

   - Configure the **WAN Interface**:
     ```bash
     config system interface
     edit port1
     set ip 192.168.1.1/24
     set allowaccess ping https ssh http
     next
     end
     ```
   
   - Configure the **LAN Interface**:
     ```bash
     config system interface
     edit port2
     set ip 10.0.0.1/24
     set allowaccess ping https ssh http
     next
     end
     ```

4. **Configure Routing:**
   If you are setting up routing, you'll need to configure a default route or other static routes.

   - Set up a default route (gateway) for the WAN interface:
     ```bash
     config router static
     edit 0
     set gateway 192.168.1.254
     set device port1
     next
     end
     ```

5. **Set Firewall Policies:**
   You'll need to configure basic firewall policies to allow traffic between your interfaces.

   - Allow traffic from LAN to WAN:
     ```bash
     config firewall policy
     edit 1
     set name "LAN-to-WAN"
     set srcintf "port2"
     set dstintf "port1"
     set action accept
     set srcaddr "all"
     set dstaddr "all"
     set schedule "always"
     set service "ALL"
     set logtraffic all
     next
     end
     ```

6. **Configure DNS and Time (Optional):**
   To ensure the device can resolve domain names, configure DNS.

   ```bash
   config system dns
   set primary 8.8.8.8
   set secondary 8.8.4.4
   end
   ```

   You may also want to configure the system time if it's not automatically syncing from an NTP server.

   ```bash
   config system global
   set timezone 04
   end
   ```

7. **Save the Configuration:**
   Always make sure to save your configuration to ensure it's persistent after reboot.

   ```bash
   execute backup config flash
   ```

### Other Useful Commands:

- **Show interface details:**
  ```bash
  show system interface
  ```

- **Check routing table:**
  ```bash
  get router info routing-table all
  ```

- **Show firewall policies:**
  ```bash
  show firewall policy
  ```

- **Reboot the device:**
  ```bash
  execute reboot
  ```

### Conclusion:
This guide covers a basic initial configuration for a FortiGate firewall. Depending on your specific network requirements, you can expand this configuration with additional features like VPNs, logging, security profiles, etc.
