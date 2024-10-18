## ETTERCAP
Ettercap is a comprehensive suite for man in the middle attacks. It features sniffing of live connections, content filtering on the fly and many other interesting tricks. It supports active and passive dissection of many protocols and includes many features for network and host analysis.

Usage: ettercap [OPTIONS] [TARGET1] [TARGET2]
TARGET is in the format MAC/IP/IPv6/PORTs (see the man for further detail)

Use the console interface and do not put the interface in promisc mode. You will see only your traffic.
      
    $ ettercap -Tp

Use the console interface, do not ARP scan the net and be quiet. The packet content will not be displayed, but user and passwords, as well as other messages, will be displayed.

    $ ettercap -Tzq

Will load the hosts list from /tmp/victims and perform an ARP poisoning attack against the two target. The list will be joined with the target and the resulting list is used for ARP poisoning.
 
    $ ettercap -T -j /tmp/victims -M arp /<Target_IP1>/ /<Target_IP2>/

Perform the ARP poisoning attack against all the hosts in the LAN. BE CAREFUL!

    $ ettercap -T -M arp // //

Perform the ARP poisoning against the gateway and the host in the lan between 2 and 10. The 'remote' option is needed to be able to sniff the remote traffic the hosts make through the gateway.

    $ ettercap -T -M arp:remote /<Target_IP>/ /<Target_IP_Range 2-10>/

Sniff only the pop3 protocol from every hosts.

    $ ettercap -Tzq //110

Sniff telnet, ftp and ssh connections to Target IP.

    $ ettercap -Tzq /<Target IP>/21,22,23

Prints the list of all available plugins 

    $ ettercap -P list

Ettercap GUI
    
    1. Select "Unified Sniffing" under Sniff on the top bar
    2. Select eth0
    3. open the menu “Sniff”
    4. select “Unified sniffing”
    5. open the “Start” menu, and select “Start sniffing”
    6. open the “View” menu, and select “Profiles”
