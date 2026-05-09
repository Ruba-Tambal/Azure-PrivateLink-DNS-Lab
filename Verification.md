Verification & Testing

 ✅ Test Results

 1. Public DNS Test
- **URL**: `http://app.ruba-demo.com`
- **Status**: Working (if Public IP is assigned to the VM)

2. Private DNS Resolution
```powershell
nslookup rubaprivatestorage.blob.core.windows.net

Expected Output:

Returns a Private IP address (Example: 10.2.1.5)


