# Diagnostics

> WIP: This is a heavy work in progress

A https://www.crowdsupply.com/dissecto/hydralink may be helpful in better reverse engineering the RiDE interface

## NOTES

* An adapter is attached to the ODBII port under the dash, and communicates on an ethernet-like DOIP interface
* An HTTP API is available from the vehicle on http://172.28.2.64:8000
* An authentication token (likely a Bearer token) is required to manupilate or interact with the API.
* Examples seem to indicate some kind of ISO-14229 implementation (UDS)
  * https://pypi.org/project/py-uds/ looks helpful.
  * https://172.28.2.64:8000/api/v1/@dtc/ReportDtcSnapshotRecordByDtcNumber

### Output example
```{
    "onboard": true,
    "version": "2023.50.01-pre+d30627237970-b06bdee1ac1f",
    "status": "ok",
    "currtime": 1706129898.688843,
    "security": {
        "api_keys_allowed": false
    },
    "os": {
        "sysname": "Linux",
        "sysrel": "5.10.72-lts-5.10.y+g0bc408190625",
        "machine": "aarch64",
        "id": "",
        "name": "NXP i.MX Release Distro",
        "version": "6.73.0",
        "version_id": "",
        "pretty_name": "NXP i.MX Release Distro 5.10-hardknott (hardknott)",
        "release_version": "release/6.73.0",
        "build_time": "20240105040529",
        "release_commit": "b06bdee1",
        "hwid": "REDACTED",
        "bootloader_version": "0x2f53",
        "bootloader_date": "2023/10/19"
    },
    "version_extra": "commit b06bdee1a",
    "version_built": 1704427190155,
    "capabilities": {
        "@dtc/ReportDtcSnapshotId": true,
        "@dtc/ReportDtcSnapshotRecordByDtcNumber": true,
        "@dtc/ReportDtcExtDataRecordByDtcNumber": true,
        "@uds/TesterPresent/responseRequired": true,
        "@uds/iocbi/get": true,
        "@uds/IoControl/ControlType": true,
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
        "@ota/deployments/ride_swappable": true
    }
}
```
