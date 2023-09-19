# ARP Observation

## notes&#x20;

Default gateway: 192.168.3.250&#x20;

## Step 1

I log into my Kali Linux virtual machine. I open a terminal and enter the command `ip route`. I make note of my default gateway: 192.168.3.250

<figure><img src="../../.gitbook/assets/image (3).png" alt=""><figcaption><p>ip route</p></figcaption></figure>

I then enter the command `sudo ip neigh flush all`. Sudo elevates my user privileges, and the rest of the command erases any saved ARP results from my cache.

## Step 2

I open Wireshark in Kali and capture the results of pinging the course instructor's workstation (192.168.3.100). In the Wireshark capture, I can see two ARP packets relating to my ping.

<figure><img src="../../.gitbook/assets/image (5).png" alt=""><figcaption><p>wireshark capture</p></figcaption></figure>

The image above is the first packet. It is the ARP request. My machine is broadcasting a request for the MAC address of IP 192.168.3.100 to all other machines in the network. The exact message is "Who has 192.168.3.100? Tell 192.168.3.29". &#x20;

<figure><img src="../../.gitbook/assets/image (6).png" alt=""><figcaption><p>wireshark capture</p></figcaption></figure>

The image above is the second packet. It is the ARP reply. The instructor's machine is responding to my broadcast, acknowledging that it has that IP address, so it responds with its MAC address. The exact message is "192.168.3.100 is at 48:21:0b:33:74:f7".

## Step 3

I flush the ARP cache again with the same command as before. I'm setting up for one more wireshark capture. I ping 8.8.8.8 (google's DNS server) while a wireshark capture is going. In the Wireshark capture, I can see 2 ARP packets relating to my ping.&#x20;

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption><p>wireshark capture 2</p></figcaption></figure>

The image above is the first packet. It is the ARP request. My machine is broadcasting a request for the MAC address of IP 192.168.3.250 to all other machines in the network. The exact message is "Who has 192.168.3.250? Tell 192.168.3.29".

<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption><p>wireshark capture v2 </p></figcaption></figure>

The image above is the second packet. It is the ARP reply. The default gateway (192.168.3.250) is responding to my broadcast, acknowledging that the requested MAC address of IP 8.8.8.8 is outside of the local network. Since ARP only works throughout local networks, google's DNS server never receives the broadcast. The closest network device to that is the default gateway (the path to distant networks).