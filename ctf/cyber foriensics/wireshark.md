wiresark is used to watch the network traffic 
The network traffic displayed initially shows the packets in order of which they were captured. You can filter packets by protocol, source IP address, destination IP address, length, etc.

Filters can be chained together using '&&' notation. In order to filter by IP, ensure a double equals   == is used

Wiresarrk Core Features

-    Capture live packet data
-    Import packets from text files
-    View packet data and protocol information
-    Save captured packet data
-    Display packets
-    Filter packets
-    Search packets
-    Colorize packets
-    Generate Statistics
### Promiscuous Mode
If you want to develop an overhead view of your network packet transfers, then you need to activate ‘promiscuous mode’.Promiscuous mode is **an interface mode where Wireshark details every packet it sees**. When this mode is deactivated, you lose transparency over your network and only develop a limited snapshot of your network (this makes it more difficult to conduct any analysis).

### Capture Filters and Display Filters
Capture Filters
are used to reduce the size of incoming packet capture, essentially filtering out other packets during live the packet capturing. As a result, capture filters are set before you begin the live capture process.
Display Fliters
can be used to filter data that has already been recorded. Capture Filters determine what data you capture from live network monitoring, and Display Filters dictate the data you see when looking through previously captured packets.

Digital filters comparison operators:

![[digitalfliters.png]]


### Statistics Menu Selections
-   **Protocol Hierarchy** – The Protocol Hierarchy option raises a window with a complete table of all captured protocols. Active display filters are also displayed at the bottom.
-   **Conversations** – Reveals the network conversation between two endpoints (For example exchange of traffic from one IP address to another).
-   **Endpoints** – Displays a list of endpoints (a network endpoint is where protocol traffic of a specific protocol layer ends).
-   **IO Graphs** – Displays user-specific graphs, visualizing the number of packets throughout the data exchange.
-   **RTP_statistics** – Allows the user to save the content of an RTP audio stream directly to an Au-file.
-   **Service Response Time** – Displays the response time between a request and the network’s response.
-   **TcpPduTime** – Displays the time taken to transfer data from a Protocol Data Unit. Can be used to find TCP retransmissions.
-   **VoIP_Calls** – Shows VoIP calls obtained from live captures.
-   **Multicast Stream** – Detects multicast streams and measures the size of bursts and the output buffers of certain speeds.





