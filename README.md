# Rivian Service Guide

Welcome to the unofficial Rivian Service Guide!

**If you use or enjoy this, please consider donating some cash via [ko-fi](https://ko-fi.com/kallisti5)!**

Best viewed here: https://github.com/kallisti5/rivian-service-guide/blob/main/README.md

> Warning: Under warranty still?
> It is strongly advised that all service occurs through Rivian Service centers while
> your vehicle is under comprehensive warranty coverage.

# Legal

Rivian is a registered trademark of [Rivian](https://rivian.com).

This guide is unofficial and has no direct relationship with Rivian.
The authors will accept no responsibility if the steps in this guide break your vehicle or void your warranty.

## Quick Lookup

Things you may be quickly searching for :-)

* **R1T/R1S Wiper blades**
  * **Front Right:** 18" "hook".  [Amazon](https://amzn.to/4oCSV79)
  * **Front Left:** 24" "hook". [Amazon](https://amzn.to/3JlHAJS)
* **Cabin Air Filter**
  * **OEM:** MANN FP 23 024
  * **3rd party**   210mm x 227mm x 30mm
    * rare. Won't be carried at O'Reilly, Auto Zone, etc.
    * [Amazon HEPA](https://amzn.to/43yubF2)
* **Lug Nuts**
  * Should be torqued to 190 Nm / 140 Ft Lb in a standard star pattern
* **RiDE Service Menu** - NOT A TOY.
  * Settings -> Service -> Enable Service Mode
  * Tap top bar 5 times. Tap on quote 5 times.
    * Recent Firmware (5 digit): 33748
    * Old Firmware (4 digit): 7433
* **Soft Reset** - Can fix screen glitches, hotspot glitches, navigation issues, etc.
  * Hold the far left and right buttons on the steering wheel for around 15 seconds.
* **Hard Reset** - Full computer restart.
  * **Warning**: Vehicle will be unavailable for up to 60 minutes.
  * **Warning**: Do not perform another reboot for 1-2 hours after performing this.
  * Hold the far left steering wheel button and the emergency flasher for 15 seconds
* **ODB2 Port**
  * No CAN bus available (not required on Electric Vehicles)
  * Generic ODB2 / Serial CAN / ELM327 diagnostic adapters will *not* work.
  * DoIP / Unified Diagnostic Services over Ethernet only.

# Official Service Manual and Tools

Rivian offers their official service manual and tools to 3rd party shops for a standard shop fee.

**Unfortunately Rivian does *NOT* offer DIY / consumer-focused Service Manuals
or Diagnostic tooling (which even GM provides) which may violate several US
states "Right to Repair" laws.**

> Using Texas as an example, HB 2963 requires:
>
> "manufacturers provide spare parts, manuals, and required tools for products sold or
> used in Texas", effective Sept, 1, 2026

[Support right-to-repair today](https://www.nytimes.com/wirecutter/blog/what-is-right-to-repair/)

## Rivian Annual Subscription Rates per User:

  * SUBSB2B201 - Part Catalog for Parts Purchase - NO CHARGE
  * SUBSB2B202 - Part Catalog + Service Manual + Online Training  = $2,500/year
  * SUBSB2B203 - Part Catalog + Service Manual + Online Training + Rivian Diagnostic Tools (RiDE) = $5,500/year
  * SUBSB2B301 - Online Training Only = $500/year

These can be subscribed to via a single-use Shopify link and password by contacting
aftersalessupport@rivian.com directly for access.

The shopify store is at https://rivian-service-subscription.myshopify.com, however you will
need the one-time link to login.

# Guides

## General

  * [Process Information](guides/process.md)
  * [General Maintenance](guides/maintenance.md)

## Diagnostics

  * [Diagnostics / ODB2 / RiDE](guides/diagnostics.md)
  
## Low Voltage Subsystems

  * [12V Battery Replacement](guides/low-voltage/12v-replacement.md)
  * [12V Pyrofuse Replacement](guides/low-voltage/12v-pyrofuse.md)
  * [Emergency Jump](guides/low-voltage/emergency-jump.md)

