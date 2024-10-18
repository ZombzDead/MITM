## MITM6
mitm6 is a pentesting tool that exploits the default configuration of Windows to take over the default DNS server. It does this by replying to DHCPv6 messages, providing victims with a link-local IPv6 address and setting the attackers host as default DNS server. As DNS server, mitm6 will selectively reply to DNS queries of the attackers choosing and redirect the victims traffic to the attacker machine instead of the legitimate server.

Author - https://github.com/dirkjanm/mitm6

### Initial Install

    $ sudo git clone https://github.com/dirkjanm/mitm6.git
    $ cd mitm6
    $ sudo pip install -r requirements.txt
    
### Usage

    $ cd /opt/tools/mitm6
    $ sudo pipenv run mitm6 -d <Target_Domain>

WARNING - THIS WILL CAUSE NETWORK CONGESTION. SYSTEMS MAY NEED TO BE RESTARTED 

Man Page:
usage: mitm6.py [-h] [-i INTERFACE] [-l LOCALDOMAIN] [-4 ADDRESS] [-6 ADDRESS][-m ADDRESS] [-a] [-v] [--debug] [-d DOMAIN] [-b DOMAIN] [-hw DOMAIN] [-hb DOMAIN] [--ignore-nofqdn]
