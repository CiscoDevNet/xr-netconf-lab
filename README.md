# xr-netconf-lab

_Understand NETCONF/YANG and build your first NETCONF client with Python to interwork with IOS-XR_

<img src="images/model-driven programmability.png">
 
## Use Case Description

This laboratory comes with a Jupyter lab for practising the NETCONF functionalities of Cisco IOS XR. A set of Docker containers is used for collecting and monitoring model-driven telemetry data, as traffic is being generated.

## Installation

### Dependencies

- Python 3
- [Ncclient](https://github.com/ncclient/ncclient) library
- Jupyter lab
- Docker
- Docker-compose
- Iperf
- IOS XR

### Configure

1. Deploy the stack of containers for monitoring of telemetry data by following these [instructions](monitoring/README.md).

2. Load the _Traffic Monitoring_ dashboard in Chronograf.

## Configuration

The details for the connection and authentication to the IOS XR can be found in the [`workshop-configuration.ini`](./workshop-configuration.ini) file.

This laboratory assumes the following:

- the host of the Jupyter lab and the docker containers is `198.18.134.50` and is a Linux host
- the Jupyter notebook is exposed on port `8443`
- the Chronograf web application is exposed on port `8888`
- the IOS XR is reachable at `198.18.134.72` with username `cisco` and password `cisco`
- the Linux host has Iperf installed on it
- the IOS XR has Iperf installed on it
- the IOS XR has the following configuration:
  ```
  telemetry model-driven
   destination-group DGroup1
    address-family ipv4 198.18.134.50 port 57777
     encoding self-describing-gpb
     protocol grpc no-tls
    !
   !
   sensor-group SGroupGeneric1
    sensor-path Cisco-IOS-XR-ifmgr-oper:interface-properties/data-nodes/data-node/system-view
   !
   subscription Subscription1
    sensor-group-id SGroupGeneric1 strict-timer
    sensor-group-id SGroupGeneric1 sample-interval 10000
    destination-id DGroup1
   !
  !
  tpa
   vrf default
    address-family ipv4
     update-source dataports Loopback0
    !
   !
  !
  netconf-yang agent
   ssh
  !
  interface Loopback0
   ipv4 address 1.1.1.1 255.255.255.255
   shutdown
  !
  ```

## Usage

Access the lab at https://198.18.134.50:8443.

Start with the [`workshop`](./workshop.ipynb) lab.
To run a section of the laboratory, select the cell and press `Shift+Enter`.


## How to test the software

This laboratory was tested in an environment that had the following software installed:

| Software  | version |
| ------------- | ------------- |
|  python  | `3.6.8`  |
|  ncclient  | `0.6.6` |
| jupyter lab | `1.2.3` |
| docker | `19.03.5` |
| docker-compose | `1.23.2` |
| iperf (server) | `2.0.5` |
| iperf (client) | `2.0.13` |
| IOS XR | `7.0.x` |

## Getting help

If you have questions, concerns, bug reports, etc., please create an issue against this repository.

## Getting involved

Feedback, bug fixes and feature enhancements or additions are encouraged. Please see the [CONTRIBUTING](./CONTRIBUTING.md) file for more information.

## Author(s)

This project was written and is maintained by the following individuals:

* cprecup <cprecup@cisco.com>