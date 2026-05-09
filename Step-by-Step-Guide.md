🛠️ Full Step-by-Step Lab
STEP 1 — Create Resource Group

Go to Resource groups → + Create
Settings:
Name: rg-private-connectivity
Region: UAE North

Click Review + create → Create

STEP 2 — Create Virtual Network

Search for Virtual networks → + Create
Basics:
Resource group: rg-private-connectivity
Name: vnet-private
Region: UAE North

IP Addresses:
Address space: 10.2.0.0/16
Delete default subnet

Click Create

STEP 3 — Create Subnet
Inside vnet-private:

Name: subnet-app
Address range: 10.2.1.0/24
Click Save

STEP 4 — Create Virtual Machine
Create a VM named vm-app with:

Region: UAE North
Image: Windows Server 2022 Datacenter (recommended) or Ubuntu
Size: Standard_D2s_v3
Virtual network: vnet-private
Subnet: subnet-app
Public IP: Enabled


STEP 5 — Create Public DNS Zone

Search DNS zones → + Create
Name: ruba-demo.com (or any name you like)
Resource group: rg-private-connectivity
Create

STEP 6 — Create DNS A Record
Inside the DNS zone:

Click + Record set
Settings:
Name: app
Type: A
IP address: Public IP of vm-app

Add


STEP 7 — Create Storage Account

Search Storage accounts → + Create
Basics:
Name: rubaprivatestorage (must be globally unique)
Region: UAE North
Performance: Standard
Redundancy: LRS

Networking tab → Public network access: Enabled (temporary)
Create

STEP 8 — Configure Service Endpoint

Go to vnet-private → Subnets → subnet-app
Under Service endpoints → + Add
Select: Microsoft.Storage
Click Add → Save

STEP 9 — Restrict Storage Account (Firewall)

Open Storage Account → Networking
Change to Selected networks
Add:
Virtual network: vnet-private
Subnet: subnet-app

Save

STEP 10 — Create Private DNS Zone

Search Private DNS zones → + Create
Name: privatelink.blob.core.windows.net
Create

STEP 11 — Link Private DNS Zone to VNet

Inside Private DNS zone → Virtual network links → + Add
Settings:
Name: link-vnet-private
Virtual network: vnet-private
Auto registration: Disabled

Create

STEP 12 — Create Private Endpoint

Search Private endpoints → + Create
Basics:
Name: pe-storage-blob
Region: UAE North

Resource tab:
Resource type: Microsoft.Storage/storageAccounts
Resource: rubaprivatestorage
Target sub-resource: blob

Virtual Network tab:
VNet: vnet-private
Subnet: subnet-app

DNS tab:
Integrate with private DNS zone: Yes
Private DNS zone: privatelink.blob.core.windows.net

Review + Create

STEP 13 — Disable Public Access

Go to Storage Account → Networking
Set Public network access to Disabled
Save

STEP 14 — Testing

Test 1: Open browser →test DNS
Test 2: On vm-app run:PowerShell
command line: Test-NetConnection rubaprivatestorage.blob.core.windows.net -Port 443
result Success Criteria:
nslookup returns Private IP (10.2.1.x)
TcpTestSucceeded : True
