# Linux Networking

Here we discuss TCP over IPv4 over Ethernet connections.

Transmission

```
Session Layer 5: sockets and files: write() / sendto() / sendmsg()
                                    __sock_sendmsg()
Transport Layer 4: TCP              tcp_sendmsg()
                                    skb_add_data()       // copying data to kernel space
                                    tcp_transmit_skt()
Network Layer 3:  IPv4              ip_queue_xmit()      // routing
                                    nf_hook()            // filtering
                                    ip_output()          // post-routing filtering
                                                         // send to output device
Link Layer 2: Ethernet              dev_queue_xmit()
```

Receive

```
Link Layer 2:  Ethernet             netif_receive_skb()
Network Layer 3: IPv4               ip_rcv() 
Transport Layer 4: TCP              tcp_v4_rcv()
```
