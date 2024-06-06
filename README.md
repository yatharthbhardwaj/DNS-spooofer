This script intercepts and manipulates DNS packets to spoof DNS responses for a specific domain. It utilizes the `netfilterqueue` library to interface with the Netfilter queue in the Linux kernel and the `scapy` library to handle and modify the network packets. The `process_packet` function processes each intercepted packet, checking if it contains a DNS response. If the DNS query name matches "winzip.com", the script alters the response to redirect the request to the IP address "192.168.179.149". It modifies the DNS answer section and recalculates the necessary checksums before reinjecting the packet back into the network stack. The script sets up a Netfilter queue, binds it to the `process_packet` function, and starts the queue to process packets. Ensure you have the required libraries installed (`netfilterqueue` and `scapy`) and run the script with root privileges due to its interaction with network packets.

To use the script, follow these steps:

1. **Install Dependencies:** Ensure `netfilterqueue` and `scapy` are installed using pip:
   ```
   pip install netfilterqueue scapy
   ```

2. **Enabling Port forwarding on Kali Linux**:
   ```
    echo 1 >/proc/sys/net/ipv4/ip_forward
   ```

3. **Creating the NFQUEUE on Kali Linux**:
   ```
   iptables -I FORWARD -j NFQUEUE --queue-num 0
   ```

4. **Turning on your apache2 server(ensure you have one) in Kali linux:**:
   ```
   service apache2 start
   ```
5. **Running the ARP Spoofer**:
   ```
   python3 arp_spoof.py
   ```
6. **Running the DNS_Spoofer**:
   ```
   python dns_sniffer.py
   ```
7. Go to the target machine's web browser and type in "winzip.com"
8. **Quit both the scripts running**
9. **Flush Ip tables**
    ```
    iptables --flush
    ```







   
