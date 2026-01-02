# Diagnostics

> WIP: This is a heavy work in progress. Physical access to the services won't get you very far until owners can authenticate to the vehicle.

Rivian vehicles offer UDS (Unified Diagnostic Services) over an Ethernet connection available within
the ODB2 connector.

The vehicles require authentication to communicate with the various UDS capabilities.

> A https://www.crowdsupply.com/dissecto/hydralink may be helpful in better reverse engineering the RiDE interface

## Hardware Connection

Standard BMW eNet ethernet adapters work just fine. Obviously BMW coding tools (bimmercode, e-Sys, etc) won't work.

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

### Example response without auth
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
> but it does make the vehicle repond differently

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
