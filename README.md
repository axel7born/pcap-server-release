# pcap-server-release
BOSH release of the pcap-server CF add-on

## Architecture

* pcap-server-api is deployed on its own vm.
* pcap-server is co-located on diego cells.
* pcap-server-api needs to register its route via route-registrar, part of the cf-routing-release.
* Requests to pcap-server-api need an authorization header including the oauth token from UAA.
  This token is used to gather information about the app from the cloud-controller.
* The pcap-api-server makes requests to the pcap-server on corresponding diego cell.

* The pcap server starts a tcptrace using libpcap and streams the results.

![alt text](docs/tcpdump-for-cf.svg "tcpdump in cf architecture")

## Jobs

### pcap-server-api

* Check if token is valid by requesting app information from CC
* Get diego cell address for app instance from CC
* Connect to pcap server on diego-cell
* Stream packets back to client

### pca-server

* Find container PID for app id
* enter container network namespace
* capture packets and stream back to client






