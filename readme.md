# vpnc-script
-----------------------------------------------------

Original : https://gitlab.com/openconnect/vpnc-scripts/-/raw/92fe06f6589dcc21725c51b8f86051482bf3b1bd/vpnc-script
Updated : https://gitlab.com/openconnect/vpnc-scripts/-/blob/master/vpnc-script?ref_type=heads

## Issues
1. Some of statments used by `vpnc-script` are not compatible with iptable 2 or higher.
2. Routes are not restored correctly after stopping openconnect client by peressing ctrl+c or stopping the service (if it is used as service).

## Fixations
* There is an updated version of `vpnc-script` [here](https://gitlab.com/openconnect/vpnc-scripts/-/blob/master/vpnc-script?ref_type=heads) that someone had worked to fix iptable issues. The patch fixs only a part of iptable issues but not all of them, for example restoring default routes still had some issues (Errors can be ssen on logs of the openconnect).
* Issues related to restoring default routes were fixed by updating some of `vpnc-script` functions.
* The script had some other issues when the openconnect was run on a system with more than one network interface. In fact the script at the beginning updated routes for all interfaces but in the cleaning part that was called at the end, only routes related to the first interface was cleaned. The script was updated to support multi interfaces for both adding and removing routes.

## Limitations of the fixations 
* If the local network ip range is defined as `no-route` from the server side, cleaning routes is not work correctly. For example if the local network is used 192.168.1.0/24 and that range is specified as no-route by the server, at the end of running openconnect client some routes related to 192.168.1.0/24 are not restored correctly.
* The current fixations fix only ipv4 parts, not ipv6. ipv6 is not covered by this patch. It can be fixed separately when it needs.
* The patch has been tested only on , macOS, Debinan 11, Ubuntu 20.04 and 22.04, and Alpine 3.12