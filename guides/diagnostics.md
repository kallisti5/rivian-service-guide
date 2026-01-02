# Diagnostics

Rivian vehicles offer [UDS (Unified Diagnostic Services)](https://en.wikipedia.org/wiki/Unified_Diagnostic_Services) over an Ethernet connection available within the ODB2 connector.

The vehicles require authentication to communicate with the various UDS capabilities.

> Wireguard sniffing the communication of the official RiDE software to the vehicle
> should be possible from systems interacting with the vehicle (running the official software)
> or with a 3rd device + an old network hub (not switch).

> RiDE to vehicle communication happens over clear text http, so any authentication tokens
> should be visible (these are short lived though and likely licensed user specific)

# Official Diagnostic Software (Full Service Center RiDE)

  * Rivian Technicians leverage Windows-based laptops
    * Technician connects to their service vehicle or service center wifi network
    * Rivian technician connects to a corporate Rivian Palo Alto VPN
  * Rivian technician connects their laptop to the vehicle via an ethernet interface over the ODB2 port (hardware below)
  * A web-based diagnostic software system (RiDE) on an internal goriv.co domain is accessed
  * The web-based diagnostic software communicates to the vehicle via a private IP (172.28.2.64:8000) over the ODB2 port
  * The web-based diagnostic software authenticates to the vehicle via the presented API
  * RiDE seems to issue UDS (Unified Diagnostic Services) API calls to vehicle

Rivian has extremely detailed historical metrics / graphs about the state of every subsystem in your vehicle
down to control pins being high or low. These metrics are retained for around 85-90 days.

Looks like standard Grafana dashboards for the most part. (and available to service advisors)

## Hardware Connection

Standard BMW eNET ethernet adapters work just fine. Obviously BMW coding tools (bimmercode, e-Sys, etc) won't work.

**Required:**

|ODB2 Pin | Ethernet Pin | Notes                                                                   |
| ------: | :----------- | :---------------------------------------------------------------------- |
|       3 | 1            | Ethernet RX+                                                            |
|      11 | 2            | Ethernet RX-                                                            |
|      12 | 3            | Ethernet TX+                                                            |
|      13 | 6            | Ethernet RX-                                                            |
|  8 + 16 | -            | Resistor between +12v and pin 8. 510 Ohm. May not be required on Rivian |

**Optional:**

> These are listed because they're common on BMW eNET cables, however they likely serve no purpose on Rivian vehicles

|ODB2 Pin | Ethernet Pin | Notes                                                                               |
| ------: | :----------- | :---------------------------------------------------------------------------------- |
|   4 + 5 | 8            | Signal Ground tied to chassis ground. Commonly tied to ethernet pin 8 for "reasons" |

## Software Connection

* Upon bringing up the ethernet interface, you should be assigned an IP within the 172.28.2.0/24 network
* The vehicle should respond on 172.28.2.64 on port 8000 (and redirect you to a status endpoint at /api/v1/status)
  * /api/v1/status offers information on the UDS capabilities currently supported. (see example below)
  * Example: "@dtc/ReportDtcSnapshotId" is http://172.28.2.64:8000/api/v1/@dtc/ReportDtcSnapshotId

### Interesting Observations

* The vehicle appears to run a Python-based web server
  * Python/3.9 (Pretty recent!), aiohttp/3.9.5 [CVEs](https://nvd.nist.gov/vuln/detail/CVE-2024-23334)
  * (psst, Rivian, don't expose internal software versions if you're worried about security here!)
 
### Example Status Output
**Example output from /api/v1/status**
```json
{
  "onboard": true,
  "version": "2025.38.0+bd6a3a117133-0055b258698f",
  "status": "ok",
  "currtime": 1767309239.3525007,
  "security": {
    "api_keys_allowed": false
  },
  "os": {
    "sysname": "Linux",
    "sysrel": "5.10.72-lts-5.10.y+g667464c9c861",
    "machine": "imx8qm-tcm",
    "id": "",
    "name": "NXP i.MX Release Distro",
    "version": "6.164.0",
    "version_id": "",
    "pretty_name": "NXP i.MX Release Distro 5.10-hardknott (hardknott)",
    "release_version": "release/6.164.0",
    "build_time": "20251023043041",
    "release_commit": "cfadcc78",
    "hwid": "OMITED",
    "bootloader_version": "0x3243",
    "bootloader_date": "2025/2/3"
  },
  "version_extra": "commit 0055b2586",
  "version_built": 1761192515461,
  "capabilities": {
    "@dtc/ReportDtcSnapshotId": true,
    "@dtc/ReportDtcSnapshotRecordByDtcNumber": true,
    "@dtc/ReportDtcExtDataRecordByDtcNumber": true,
    "@uds/TesterPresent/responseRequired": true,
    "@uds/iocbi/get": true,
    "@uds/IoControl/ControlType": true,
    "rdx": true,
    "@tasks/timeout": true,
    "@ota/deployments/guid": true,
    "@deployments/upload/path": true,
    "@config/vehicle/write": true,
    "@config/vehicle/read": true,
    "@config/tcm/clear": true,
    "@config/ecu/write/cgm": true,
    "@config/ecu/read/cgm": true,
    "@config/ecu/write/bcm": true,
    "@config/ecu/read/bcm": true,
    "@config/ecu/write/tmm": true,
    "@config/ecu/read/tmm": true,
    "@config/ecu/write/vdm": true,
    "@config/ecu/read/vdm": true,
    "@config/ecu/write/rzc": true,
    "@config/ecu/read/rzc": true,
    "@config/ecu/write/bms_p": true,
    "@config/ecu/read/bms_p": true,
    "@config/ecu/write/asm_a": true,
    "@config/ecu/read/asm_a": true,
    "@config/ecu/read/asm_b": true,
    "@config/ecu/write/acm_a": true,
    "@config/ecu/read/acm_a": true,
    "@config/ecu/read/acm_b": true,
    "@config/ecu/read/acm_ls2": true,
    "@config/ecu/write/pab_a": true,
    "@config/ecu/read/pab_a": true,
    "@config/ecu/read/pab_b": true,
    "@config/ota/read": true,
    "@config/cloud/read": true,
    "@ota/deployments/ride_swappable": true,
    "@flash/acm_orin/overwrite_upload": true
  },
  "version_firmware_commit_hash": "0055b258698fe117a8bd8034bb80a00bc6421997"
}
```

### Example response without authentication
```json
# curl http://172.28.2.64:8000/api/v1/@dtc/ReportDtcSnapshotId -v
*   Trying 172.28.2.64:8000...
* Connected to 172.28.2.64 (172.28.2.64) port 8000 (#0)
> GET /api/v1/@dtc/ReportDtcSnapshotId HTTP/1.1
> Host: 172.28.2.64:8000
> User-Agent: curl/7.88.1
> Accept: */*
> 
< HTTP/1.1 401 Unauthorized
< Content-Type: text/plain; charset=utf-8
< Content-Length: 23
< Date: Thu, 01 Jan 2026 23:39:09 GMT
< Server: Python/3.9 aiohttp/3.9.5
< 
* Connection #0 to host 172.28.2.64 left intact
```

### Example Response with invalid bearer token

> Note: I'm not sure if a Bearer token is the way to authenticate,
> but it does make the vehicle respond differently

```json
# curl http://172.28.2.64:8000/api/v1/@dtc/ReportDtcSnapshotId -H "Authorization: Bearer HelloRivian" -v
*   Trying 172.28.2.64:8000...
* Connected to 172.28.2.64 (172.28.2.64) port 8000 (#0)
> GET /api/v1/@dtc/ReportDtcSnapshotId HTTP/1.1
> Host: 172.28.2.64:8000
> User-Agent: curl/7.88.1
> Accept: */*
> Authorization: Bearer HelloRivian
> 
< HTTP/1.1 500 Internal Server Error
< Content-Type: text/plain; charset=utf-8
< Content-Length: 55
< Date: Thu, 01 Jan 2026 23:37:42 GMT
< Server: Python/3.9 aiohttp/3.9.5
< Connection: close
< 
500 Internal Server Error

* Closing connection 0
```

# Other tools

* https://www.crowdsupply.com/dissecto/hydralink - Sniffing high-speed vehicle Ethernet traffic
