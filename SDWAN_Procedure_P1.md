# RivanCorp SD-WAN Deployment Lab
## Step-by-Step Procedure

This guide covers the initial setup and startup procedure for the RivanCorp SD-WAN Deployment Lab, including EVE-NG access, vManage startup, and SecureCRT console access.

---

## STEP 1 - Configure a Host Route for the vManage GUI

Open **Command Prompt (CMD)** and add a host route for the vManage GUI:

```cmd
route add 10.69.255.13 mask 255.255.255.255 10.69.255.6
```

> **Note:** Run Command Prompt as **Administrator** if the command requires elevated privileges.

---

## STEP 2 - Review the SD-WAN Appliance Credentials

### SD-WAN Appliance Login

> **Username:** `admin`  
> **Password:** `C1sc0123`

### Appliance Console Ports

| Device | Port |
| --- | ---: |
| CLOUD | `32902` |
| PKI SERVER | `32913` |
| vManage | `32897` |
| vSmart | `32898` |
| vBond | `32899` |
| vEdge-LUZON | `32900` |
| vEdge-VISAYAS | `32903` |
| vEdge-MINDANAO | `32904` |
| CSW-LUZON | `32905` |
| CSW-VISAYAS | `32906` |
| CSW-MINDANAO | `32907` |

---

## STEP 3 - Obtain the EVE Lab IP Address

Identify and take note of the IP address assigned to the **EVE Lab**.

<img width="564" height="136" alt="EVE Lab IP Address" src="https://github.com/user-attachments/assets/91c17d71-c891-4cb2-829c-6ec80199dfee" />

---

## STEP 4 - Access the EVE-NG Topology

Open the EVE-NG web interface using the IP address obtained in **Step 3**.

Use the following credentials:

> **Username:** `rivan`  
> **Password:** `C1sc0123`

Click **Sign In**.

<img width="1440" height="782" alt="EVE-NG Login Page" src="https://github.com/user-attachments/assets/cdc31fc2-7ce3-4173-951c-10cc5a19256e" />

---

## STEP 5 - Open the RivanCorp SD-WAN Deployment Lab

From the EVE-NG lab list:

1. Locate **RivanCorp SDWAN Deployment Lab**.
2. Select the lab.
3. Click **Open**.

<img width="1438" height="652" alt="RivanCorp SD-WAN Deployment Lab" src="https://github.com/user-attachments/assets/47bab84c-0ccf-468c-afff-c17c51668d41" />

---

## STEP 6 - Enable Dark Mode

Once inside the topology, navigate to the menu on the **left side** of the EVE-NG interface.

Enable **Dark Mode** for better visibility of the topology and device information.

<img width="145" height="373" alt="EVE-NG Dark Mode Option" src="https://github.com/user-attachments/assets/c6dd8cd7-7bb1-4fc0-a1c6-bffea598cd0a" />

---

## STEP 7 - Start the vManage Manager

Locate the **vManage-Manager** node in the topology.

1. Right-click **vManage-Manager**.
2. Click **Start**.

<img width="259" height="256" alt="Start vManage Manager" src="https://github.com/user-attachments/assets/22ccbee1-2d4c-4baa-83bc-ee911340865a" />

---

## STEP 8 - Access vManage Using SecureCRT

After starting **vManage-Manager**, access its console using **SecureCRT** via Telnet.

Configure the SecureCRT session with the following information:

| Setting | Value |
| --- | --- |
| Protocol | `Telnet` |
| IP Address | `208.8.8.187` |
| Port | `32897` |
| Device | `vManage` |

> [!IMPORTANT]
> vManage may take approximately **10 minutes** to fully initialize. Do not proceed with vManage configuration until the system reports that it is ready.

---

## STEP 9 - Start the vSmart, vBond, and CLOUD Nodes

While waiting for vManage to initialize, start the following nodes:

1. **vSmart-Controller**
2. **vBond-Validator**
3. **CLOUD**

Access each device through **SecureCRT** using Telnet.

Use the following IP address:

```text
208.8.8.187
```

Use the appropriate console port for each device:

| Device | Telnet Port |
| --- | ---: |
| CLOUD | `32902` |
| vSmart | `32898` |
| vBond | `32899` |

<img width="577" height="581" alt="SecureCRT SD-WAN Console Sessions" src="https://github.com/user-attachments/assets/ea86fd30-a108-4097-b11a-d89919d04947" />

---

## STEP 10 - Verify That vManage Is Ready

Wait approximately **10 minutes** for the vManage appliance to complete its startup process.

Monitor the **vManage-Manager** console in SecureCRT.

The expected output should indicate that the system is ready, similar to the following:

<img width="1065" height="707" alt="vManage System Ready Output" src="https://github.com/user-attachments/assets/b1f9e1c9-a7c8-485d-b6d2-583b12fe68c6" />

> [!NOTE]
> Once the **system ready** message appears, the vManage appliance has completed its initialization and you can proceed with the next configuration steps.

---

## STEP 11 - Verify the vManage NMS Services

Access the **vManage-Manager CLI** through SecureCRT.

Run the following command to check the status of all vManage NMS services:

```bash
request nms all status
```

<img width="525" height="100" alt="Check vManage NMS Status" src="https://github.com/user-attachments/assets/0cc76fdc-bd17-4628-85a2-7d8d3da067a7" />

Verify that the **NMS Application Server** is running.

The status should show:

```text
NMS application server
Enabled: true
Status: running
```

<img width="366" height="57" alt="NMS Application Server Running" src="https://github.com/user-attachments/assets/94085a7e-b0e5-43d4-baad-0714086720b1" />

> [!IMPORTANT]
> Do not proceed with the vManage configuration until the **NMS Application Server** shows a `running` status.

---

## STEP 12 - Configure vManage

Once the NMS Application Server is running, configure the vManage appliance.

Copy and paste the following configuration into the **vManage CLI**:

```text
!@vManage
conf t
 system
  host-name Rivan-vManage
  site-id 10
  system-ip 10.1.10.2
  organization-name RIVANCORP
  vbond 172.16.10.3
  admin-tech-on-failure
 vpn 0
  int eth0
   ip add 172.16.10.2/29
   no shut
   tunnel-interface
    allow-service all
  ip route 0.0.0.0/0 172.16.10.6
 vpn 512
  int eth1
   ip add 10.69.255.13/30
   no shut
  ip route 0.0.0.0/0 10.69.255.14
  commit
  end
```

<img width="605" height="687" alt="vManage CLI Configuration" src="https://github.com/user-attachments/assets/309e8dac-8625-4e2c-a000-af5c3fed010e" />

> [!NOTE]
> After entering the configuration, verify that the `commit` operation completes successfully before proceeding.

---

## STEP 13 - Access the vManage GUI

After configuring vManage, open its web interface using a browser.

> [!NOTE]
> **Microsoft Edge is recommended** for accessing the vManage GUI in this lab.
>
> It may take approximately **10 minutes** after configuration before the vManage GUI becomes accessible.

Open the following URL:

```text
https://10.69.255.13:8443
```

Use the following credentials:

> **Username:** `admin`  
> **Password:** `C1sc0123`

Click **Log In**.

<img width="1440" height="790" alt="vManage GUI Login Page" src="https://github.com/user-attachments/assets/5f81037b-17f7-4839-83b5-4c6c13103c80" />

> [!TIP]
> If the GUI does not load immediately, wait a few minutes and refresh the browser. Make sure the host route configured in **Step 1** is still present.

---

## STEP 14 - Configure the vBond Controller

While waiting for the vManage GUI to initialize, access the **vBond-Validator** appliance through SecureCRT.

Use the following credentials:

> **Username:** `admin`  
> **Password:** `C1sc0123`

Copy and paste the following configuration into the **vBond CLI**:

```text
!@vBond
conf t
 system
  host-name Rivan-vBond
  site-id 10
  system-ip 10.1.10.3
  organization-name RIVANCORP
  vbond 172.16.10.3 local vbond
  admin-tech-on-failure
 vpn 0
  int ge0/0
   ip add 172.16.10.3/29
   no shut
   tunnel-interface
    encapsulation ipsec
    allow-service all
  ip route 0.0.0.0/0 172.16.10.6
  commit
  end
```

<img width="643" height="468" alt="vBond CLI Configuration" src="https://github.com/user-attachments/assets/3e272b23-ac80-410f-b963-d5702307126a" />

> [!NOTE]
> Verify that the configuration commits successfully before proceeding.

---

## STEP 15 - Configure the vSmart Controller

Access the **vSmart-Controller** appliance through SecureCRT.

Use the following credentials:

> **Username:** `admin`  
> **Password:** `C1sc0123`

Copy and paste the following configuration into the **vSmart CLI**:

```text
!@vSmart
conf t
 system
  host-name Rivan-vSmart
  site-id 10
  system-ip 10.1.10.1
  organization-name RIVANCORP
  vbond 172.16.10.3
  admin-tech-on-failure
 vpn 0
  int eth0
   ip add 172.16.10.1/29
   no shut
   tunnel-interface
    allow-service all
  ip route 0.0.0.0/0 172.16.10.6
  commit
  end
```

<img width="628" height="588" alt="vSmart CLI Configuration" src="https://github.com/user-attachments/assets/1e1af560-11e8-4e15-b818-10090df7f160" />

> [!IMPORTANT]
> Wait until the **SD-WAN controllers are stable** before proceeding with the vEdge devices.

---

## STEP 16 - Start the vEdge Nodes

While waiting for the vManage GUI and SD-WAN controllers to stabilize, start the following vEdge nodes:

1. **vEdge-LUZON**
2. **vEdge-VISAYAS**

Right-click each node in the EVE-NG topology and select **Start**.

<img width="767" height="167" alt="Start vEdge Luzon and Visayas Nodes" src="https://github.com/user-attachments/assets/50042b4b-1be6-44ab-bdba-180bd446a4dd" />

> [!NOTE]
> At this stage, the vEdge nodes may be powered on but are not yet expected to have full reachability to the SD-WAN controllers.

---

## STEP 17 - Verify the vManage GUI

Return to the **vManage GUI** in Microsoft Edge.

If necessary, refresh the browser:

```text
https://10.69.255.13:8443
```

Wait for vManage to finish initializing.

The vManage dashboard should load successfully, similar to the following expected output:

<img width="1440" height="727" alt="vManage Dashboard Expected Output" src="https://github.com/user-attachments/assets/1ca9ce51-a884-435c-8f87-6c29fad05182" />

> [!NOTE]
> The vEdge devices may still be unreachable at this stage. The **CLOUD node** must be configured to provide the required routing between the SD-WAN controllers and vEdge devices.

---

## STEP 18 - Access the CLOUD Node

Access the **CLOUD** node through SecureCRT using Telnet.

Use the following connection information:

| Setting | Value |
| --- | --- |
| Protocol | `Telnet` |
| IP Address | `208.8.8.187` |
| Port | `32902` |
| Device | `CLOUD` |

Enter privileged EXEC mode:

```text
enable
```

Enter the enable password when prompted:

```text
pass
```

---

## STEP 19 - Configure BGP on the CLOUD Node

Configure the CLOUD node to establish BGP connectivity with the vEdge devices.

Copy and paste the following configuration:

```text
!@Cloud (BGP Config)
conf t
 int lo8
  ip add 8.8.8.8 255.255.255.255
 router bgp 1
  bgp log-neighbor-changes
  neighbor 192.168.20.1 remote-as 100
  neighbor 192.168.20.5 remote-as 100
  neighbor 192.168.20.9 remote-as 100
  address-family ipv4
   neighbor 192.168.20.1 activate
   neighbor 192.168.20.5 activate
   neighbor 192.168.20.9 activate
   neighbor 192.168.20.1 as-override
   neighbor 192.168.20.5 as-override
   neighbor 192.168.20.9 as-override
   network 8.8.8.8 mask 255.255.255.255
   network 192.168.20.0 mask 255.255.255.0
   network 172.16.10.0 mask 255.255.255.248
   network 10.69.255.0 mask 255.255.255.248
   end
```

<img width="632" height="624" alt="CLOUD Node BGP Configuration" src="https://github.com/user-attachments/assets/84f81dba-b770-49a9-93bd-28cb4de3bd02" />

> [!IMPORTANT]
> The CLOUD node provides routing between the SD-WAN infrastructure and the vEdge devices. Make sure the BGP configuration is applied successfully before proceeding with the vEdge configuration.

---

## STEP 20 - Verify vEdge Reachability in vManage

After completing the BGP configuration on the **CLOUD** node, return to the **vManage GUI** and verify the status of the vEdge devices.

Refresh the vManage GUI if necessary:

```text
https://10.69.255.13:8443
```

Check the dashboard and confirm that the vEdge devices are now **reachable**.

The expected output should be similar to the following:

<img width="1440" height="723" alt="vManage vEdge Reachability Verification" src="https://github.com/user-attachments/assets/a296cc71-4043-4d59-88d7-8816dc02f627" />

> [!IMPORTANT]
> The vEdge devices should now appear as **reachable** in the vManage GUI. This confirms that the CLOUD node's BGP configuration is providing the required network reachability between the vEdge devices and the SD-WAN controllers.

> [!NOTE]
> If the vEdge devices are still unreachable, verify the **CLOUD BGP configuration**, BGP neighbor status, IP addressing, and routing before proceeding to the next step.

---




















