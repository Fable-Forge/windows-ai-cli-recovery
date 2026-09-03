# Windows AI CLI Checks

## Command Lookup

```powershell
Get-Command claude -All -ErrorAction SilentlyContinue
Get-Command codex -All -ErrorAction SilentlyContinue
npm config get prefix
Get-ChildItem "$env:APPDATA\npm" -Filter "claude*"
Get-ChildItem "$env:APPDATA\npm" -Filter "codex*"
```

## PATH Refresh

Temporary refresh for the current PowerShell:

```powershell
$env:Path = [Environment]::GetEnvironmentVariable('Path','Machine') + ';' + [Environment]::GetEnvironmentVariable('Path','User')
```

Add npm global bin to user PATH only when missing:

```powershell
$npmBin = Join-Path $env:APPDATA 'npm'
$userPath = [Environment]::GetEnvironmentVariable('Path','User')
if ($userPath -notlike "*$npmBin*") {
  [Environment]::SetEnvironmentVariable('Path', "$userPath;$npmBin", 'User')
}
```

## PowerShell Execution Policy

If `<tool>.ps1` is blocked, try the `.cmd` shim first:

```powershell
claude.cmd --version
codex.cmd --version
```

Do not loosen execution policy unless the user explicitly requests it and understands the tradeoff.

## Local Proxy Discovery

```powershell
Get-NetTCPConnection -State Listen |
  Where-Object { $_.LocalAddress -in @('127.0.0.1','0.0.0.0','::1','::') } |
  Sort-Object LocalPort |
  Select-Object LocalAddress,LocalPort,OwningProcess
```

Then confirm the process:

```powershell
Get-Process -Id <pid> -ErrorAction SilentlyContinue | Select-Object Id,ProcessName,Path
```

Short TCP check:

```powershell
$client = New-Object System.Net.Sockets.TcpClient
$async = $client.BeginConnect('127.0.0.1',7897,$null,$null)
$ok = $async.AsyncWaitHandle.WaitOne(1500,$false)
if ($ok) { $client.EndConnect($async); 'OK' } else { 'TIMEOUT' }
$client.Close()
```

## Codex Proxy File

Expected path:

```text
C:\Users\<user>\.codex\.env
```

Expected contents:

```env
HTTP_PROXY="http://127.0.0.1:<port>"
HTTPS_PROXY="http://127.0.0.1:<port>"
```
