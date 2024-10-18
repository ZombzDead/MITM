## HPing
Hping is a command-line oriented TCP/IP packet assembler/analyzer. The interface is inspired to the ping(8) unix command, but hping isn't only able to send ICMP echo requests. It supports TCP, UDP, ICMP, and RAW-IP protocols, has a traceroute mode, the ability to send files between a covered channel, and many other features. It is one kind of tester for network security and one of the de-facto tools for security auditing and testing of firewalls and networks. It was used to exploit the idle scan scanning technique, which now is implemented in the Nmap scanner as well.

usage: hping3 host [options]

Testing Examples:

    $ hping3 -1 -c 1 <Target_IP>

The –1 in this command tells hping3 to use ICMP, which sends an Echo Reply.
The -c 1 states that we only want to send 1 packet, and the 192.168.1.12 is our target. From the command output, we see that 1 packet was sent and received.

 
We going to test a well-known port 80 (HTTP). Since SYN is the first step in the three-way handshake of a TCP connection (SYN, SYN-ACK, ACK), if the port is open, we would receive the proper SYN-ACK response due to the target attempting to complete the connection. This is a popular technique used in port-scanning known as a “half-open connection.” 

    $ hping3 -S -c 1 -s 5151 -p 80 <Target_IP> 

In the result, we should see that our target has responded, and the output shows “flags=SA,” confirming that we have received an SYN-ACK packet. Since our target responded with an SYN-ACK (marked by [S.] and ‘ack‘), we know that our target’s port 80 is open and accepting connections.

We saw in the previous example that when we send an SYN packet to an open port, we receive an SYN-ACK. So, let’s see what kind of response we get when we send an ACK packet (the final part of the three-way handshake).

    $ hping3 -A -c 1 -s 5151 -p 80 <Target_IP>

In the server response, we can see that our target responded, but this time with the RST flag set. We have successfully tested a host, set up rules to correct the issues we’ve found, and retested for proper functionality.
