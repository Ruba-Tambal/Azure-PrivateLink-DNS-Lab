# Verification & Testing

## ✅ Test Results

1. Public DNS Test
- URL: your URL
- Status: Working (if Public IP is assigned to VM)

2. Private DNS Resolution
```powershell
nslookup rubaprivatestorage.blob.core.windows.net

3. Private Link Connectivity Test
```powershell
Test-NetConnection rubaprivatestorage.blob.core.windows.net -Port 443

Expected: TcpTestSucceeded : True
