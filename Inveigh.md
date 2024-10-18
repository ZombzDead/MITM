# Inveigh
Inveigh is a cross-platform .NET IPv4/IPv6 machine-in-the-middle tool for penetration testers. This repo contains the primary C# version as well as the legacy PowerShell version. Inveigh conducts spoofing attacks and hash/credential captures through both packet sniffing and protocol specific listeners/sockets. 

### Intial Usage

    PS C:\Tools\Inveigh > Import-Module .\Inveigh.ps1

### Inveigh running with elevated privilege
    
    PS C:\Tools\Inveigh > Invoke-Inveigh -ConsoleOutput Y -NBNS Y -mDNS Y -HTTPS Y -Proxy Y

### Inveigh running without elevated privilege

    PS C:\Tools\Inveigh > Invoke-Inveigh -ConsoleOutput Y -NBNS Y

Reference: https://github.com/Kevin-Robertson/Inveigh
