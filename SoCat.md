# SoCat
The socat utility is a relay for bidirectional data transfers between two independent data channels. This tool is regarded as the advanced version of netcat. They do similar things, but socat has more additional functionality, such as permitting multiple clients to listen on a port, or reusing connections.  

### Connect TCP-Port 80

    $ socat [options] <address> <address>
    $ socat - TCP4:www.example.com:80

In this case, socat transfers data between STDIO (-) and a TCP4 connection to port 80 on a host named www.example.com. 

### Use socat as a TCP port forwarder: 

- For a single connection, enter:

      $ socat TCP4-LISTEN:81 TCP4:192.168.1.10:80 

- For multiple connections, use the fork option as used in the examples below: 

      $ socat TCP4-LISTEN:81,fork,reuseaddr TCP4:TCP4:192.168.1.10:80 
  This example listens on port 81, accepts connections, and forwards the connections to port 80 on the remote host. 

      $ socat TCP-LISTEN:3307,reuseaddr,fork UNIX-CONNECT:/var/lib/mysql/mysql.sock
  The above example listens on port 3307, accepts connections, and forwards the connections to a Unix socket on the remote host. 

### Implement a simple network-based message collector: 

    $ socat -u TCP4-LISTEN:3334,reuseaddr,fork OPEN:/tmp/test.log,creat,append 
  When a client connects to port 3334, a new child process is generated. All data sent by the clients is appended to the file /tmp/test.log. If the file does not exist, socat creates it. The option reuseaddr allows an immediate restart of the server process. 

### Send a broadcast to the local network: 

    $ socat - UDP4-DATAGRAM:224.255.0.1:6666,bind=:6666,ip-add-membership=224.255.0.1:eth0
  In this case, socat transfers data from stdin to the specified multicast address using UDP over port 6666 for both the local and remote connections. The command also tells the interface eth0 to accept multicast packets for the given group. 

### Custom

    $ socat TCP4-LISTEN:<port>,fork TCP4:<ip:port> 
"Listen on my local IP on <port>, then fork any connections I get (new stream so I can handle multiple connections), and forward to a new <ip:port>"
