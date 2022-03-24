# pcap-server-release
BOSH release of the pcap-server CF add-on

## Architecture
![alt text](docs/tcpdump-for-cf.svg "tcpdump in cf architecture")
While pcap-server-api should be deployed on its own vm, the pcap-server is co-located on diego cells.
pcap-server-api needs to register its route via route-registrar, part of the cf-routing-release.

Requests to pcap-server-api need an authorization header including the oauth token from cf uaa.
This token is used to gather information about the app from the cloud-controller.
The pcap-api-server makes requests to the pcap-server on corresponding diego.

The pcap server starts a tcptrace using libpcap and streams the results.



## Jobs

### pcap-server-api




