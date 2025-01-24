Here’s a **short guide** for configuring a **trusted IP** range for the management interface on a FortiGate firewall:

## Single command:

```bash
config system interface
edit "mgmt"
set allowaccess ping https ssh fgfm
set ip 192.161.1.1 255.255.255.0
set trust-ip-1 192.161.1.0 255.255.255.0
next
end
```

---

### **1. Log in to the FortiGate CLI**
Use a serial console or SSH to access the CLI.

### **2. Enter Interface Configuration Mode**
Access the system interface configuration for the **management** interface.

```bash
config system interface
```

### **3. Edit the `mgmt` Interface**
Select the `mgmt` interface to modify its settings.

```bash
edit "mgmt"
```

### **4. Set Allowed Access Methods**
Define the access methods (e.g., `ping`, `https`, `ssh`, `fgfm`) that are allowed for the **mgmt** interface.

```bash
set allowaccess ping https ssh fgfm
```

### **5. Set Management IP and Subnet**
Assign an IP address and subnet mask to the **mgmt** interface.

```bash
set ip 192.161.1.1 255.255.255.0
```

### **6. Configure Trusted IP Range**
Specify the trusted IP range that will be allowed to access the **mgmt** interface. Replace `192.161.1.0 255.255.255.0` with the desired range.

```bash
set trust-ip-1 192.161.1.0 255.255.255.0
```

### **7. Save and Exit**
Save your configuration and exit.

```bash
next
end
```

---

### **Summary:**
- **`set allowaccess`**: Specifies the protocols allowed to manage the interface.
- **`set ip`**: Assigns an IP address to the interface.
- **`set trust-ip-1`**: Defines the trusted IP range allowed to access the management interface.

Now your **management interface** will allow access only from trusted IPs within the specified range, and only the allowed services will be accessible for management.

---

Let me know if you need any other configurations or explanations!
