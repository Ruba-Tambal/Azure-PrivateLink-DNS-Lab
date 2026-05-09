Verification & Testing

✅ Test Results

1. Public DNS Test
- **URL**: `http://app.ruba-demo.com`
- **Status**: Working (if Public IP is assigned to VM)

2. Private DNS Resolution
```powershell
nslookup rubaprivatestorage.blob.core.windows.net
Expected Output: Returns Private IP (e.g., 10.2.1.5)
3. Private Link Connectivity Test
PowerShellTest-NetConnection rubaprivatestorage.blob.core.windows.net -Port 443
Expected Output: TcpTestSucceeded : True
4. Storage Account Security Check

Public network access = Disabled
Only accessible via Private Endpoint
