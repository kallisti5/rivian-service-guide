# Rivian Service Guide

Welcome to the unofficial Rivian Service Guide!
Here I'll document the things not in the user manual until Rivian makes a Service Manual available.

**If you use or enjoy this, please consider donating some cash via [ko-fi](https://ko-fi.com/kallisti5)!**

Best viewed here: https://github.com/kallisti5/rivian-service-guide/blob/main/README.md

# Repair

## Service Menu

This section exists because consumers deserve the right to service their own vehicles.

> Disclaimer: You can mess up your vehicle calibrations, or cause non-warranty covered damage
> playing around in the service menu. RiDE is not a toy. If you don't know what you're doing,
> don't change anything.

[Support right-to-repair today](https://www.nytimes.com/wirecutter/blog/what-is-right-to-repair/)

> Rivian employees: If you read this, please make service manuals available to the general public.
> we love our amazing vehicles, and want to have options other than waiting 6 months for a service
> appointment.

**Provides:**

Gives access to detailed diagnostic information about your vehicle, and allows basic
service-related actions such as re-calibrations of motor limits.

**Process:**

* Tap on the top black bar five times.
* Bring up the bottom menu.
* Tap the new "R (RiDE)" icon.
* A quote will show up on screen.
  * Earlier 4 digit versions were "7433"  (Ride)
  * Later 5 digit versions are "33748"

These service pin numbers were located by a long chain of random internet strangers.
There's no direct connection to this repository, and where they came from.

Rivian has the ability to change these service pin numbers at any time via OTA updates.

## ODB2 Port

Now the meaty bits.   The ODB2 port on the Rivian R1T seems to not offer standard CAN communications
(as CAN is no longer required for electric vehicles).

The Rivian ODB2 port does however offer a standard DoIP interface (used by the likes of BMW, etc)

I've attached to this DoIP interface, gotten an ethernet link, and sniffed activity with Wireshark
(which should be DoIP aware).

My system spamming DHCP client requests off into the ether of the Rivian saw zero traffic returned.

Thoughts:
  * The standard 510 Ohm resistor in the BMW adapters isn't the correct value to give access to DoIP.
  * You have to activate something in the (no longer accessible) RiDE diagnostic screen to activate DoIP.
  * You have to provide a certificate to some silent network endpoint to authenticate for access.

Someone sniffing the communications from the Rivian diagnostic equipment to the Rivian with Wireshark
and an ethernet hub would be infinitely useful here... however given the limited access to such diagnostic
hardware, this is a big lift.

Right-to-repair laws however may improve access to such hardware.

## Resets

### Sleep Reset

**Fixes:**
Can fix minor issues... however not very useful for larger issues.

**Process:**

* Nothing plugged into USB ports.
* Exit the vehicle, all seatbelts unbuckled.
* Vehicle not charging.
* Close the doors, lock.
* Leave it alone for 30 minutes.

### Soft Infotainment Reset

**Fixes:**
Can fix screen glitches, hotspot glitches, navigation issues, etc.

**Process:**
Hold the far left and right buttons on the steering wheel for around 15 seconds.

### Full Reset

**Fixes:**
Full computer restart. 

**Warning:**
Your vehicle will be out of service for 30 - 60 full minutes as the car boots up. DO NOT REBOOT
AGAIN FOR AT LEAST 1-2 hours!!!

**Process:**
Hold the far left steering wheel button and the emergency flasher for 15 seconds.

# Process

## Changing Ownership

As of Jan 2023, If you purchase a Rivian from a third-party you must email Rivian a copy of the
bill of sale and a copy of your drivers license. The process takes 7-10 days.. so do it ASAP after
purchase.

## Service Technician

Currently, costs for a mobile Rivian Service Technician to show up for a non-warranty covered
trip are a steep $700+.  Talk to customer service and make sure your work is covered by warranty.

## Tire Rotation

> TIP: If you have a full size spare, be sure to rotate your spare into the mix before 8k miles!
> This will give you 25% more tire life. After around 10k miles of wear, the tread difference
> generally gets too great to perform a 5-tire rotation.

Be sure to set the highest off-road ride-height, and enable tire change mode in the service menu!
It's recommended to have at least two jack methods to enable you access to two tires at a time.

### Conserve Mode

Conserve mode will consume your front tires at a faster rate than your rear. (conserve is front
wheel drive). Be extra sure to practice good tire rotation when using conserve mode!

### Lug Nut Torque

Lug nuts should be torqued to 190 Nm / 140 Ft Lb in a standard star pattern

### TPMS Sensors

The Rivian vehicles auto-learn the TPMS sensor positions after a tire rotation. Rivian support
has confirmed this only takes 10-15 minutes of driving. No tool needed.

# Known Problems

## Automatic Tonneau Cover

The automatic Tonneau cover sold on early vehicles *will* jam and fail with dirt + age.
Rivian is currently working on a free fix for existing vehicles.

Until then, if your Tonneau cover works today and hasn't been locked out by Rivian. Take these
steps ASAP while it is still functional.

* Buy a can (or two) of WD-40 Specialist Dry Lube with PTFE.
* Clean off any grime or debris with Tonneau closed.
* Spray in-between each panel section with the straw nozzle.
* Open the Tonneau.
* Spray the tracks on either side using the straw nozzle.
* Spray around the front edge of the Tonneau track on either side.
* Wipe off excess. Close the Tonneau.
* Repeat every month or two to buy yourself time.

If your Tonneau jams, contact Rivian service. They'll open it fully and lock it out until
the final solution is released.

[RSB-60-22-001-1](https://static.nhtsa.gov/odi/tsbs/2022/MC-10228730-0001.pdf) -- Disable

## Customer Satisfaction Campaigns

> TODO: Cover before DEC 2 2022

|Model     |Mfg Date           | ID                                                                            | Thing               | Notes                                                      |
|----------|:------------------|:------------------------------------------------------------------------------|:--------------------|:-----------------------------------------------------------|
| R1T      | Aug 21 - May 22   |[RCA-56-22-011-1](https://static.nhtsa.gov/odi/tsbs/2022/MC-10228721-0001.pdf) | Closures            | Bed storage compartment seal. Cold weather stick           |
| R1T      | Aug 21 - Nov 22   |[RCA-64-22-006-1](https://static.nhtsa.gov/odi/tsbs/2022/MC-10228723-0001.pdf) | Interior            | Upper C-Pillar trim panel adjustment                       |
| R1T,R1S  | Aug 21 - Aug 22   |[RCA-78-22-015-1](https://static.nhtsa.gov/odi/tsbs/2022/MC-10228727-0001.pdf) | Low voltage elec.   | Firmware fix, automatic seat and steering wheel adjust.    |
| R1T      | Aug 21 - Jan 22   |[RCA-56-22-008-1](https://static.nhtsa.gov/odi/tsbs/2022/MC-10228719-0001.pdf) | Closures            | Exterior door handle levers, water intrusion               |
| R1T      | Aug 21 - Feb 22   |[RSB-64-23-001-1](https://static.nhtsa.gov/odi/tsbs/2023/MC-10243561-0001.pdf) | Interior            | Tailgate trim panel, update with rubber                    |
| R1T      | Dec 21 - Feb 22   |[RCA-30-22-001-1](https://static.nhtsa.gov/odi/tsbs/2022/MC-10228717-0001.pdf) | HV Battery          | Apply sealant to HV battery                                |
| R1T,R1S  | Mar 22 - Sep 22   |[RSB-56-23-001-1](https://static.nhtsa.gov/odi/tsbs/2023/MC-10232188-0001.pdf) | Closures            | Front door, fixed glass molding separation                 |
| R1T      | Aug 21 - Sep 21   |[RCA-86-23-001-1](https://static.nhtsa.gov/odi/tsbs/2023/MC-10241958-0001.pdf) | Driver Assistance   | Update firmware for dash, unable to receive HD map info    |
| R1T,R1S  | Aug 21 - May 22   |[RCA-96-23-001-1](https://static.nhtsa.gov/odi/tsbs/2023/MC-10241957-0001.pdf) | Supplemental        | Tire sealant kit leaking                                   |
| R1T      | Aug 21 - Oct 21   |[RCA-56-22-001-1](https://static.nhtsa.gov/odi/tsbs/2022/MC-10207696-0001.pdf) | Body                | Hood flutter at speed, insufficient adhesive               |
| R1T,R1S  | Aug 21 - Feb 22   |[RCA-38-23-003-2](https://static.nhtsa.gov/odi/tsbs/2023/MC-10240312-0001.pdf) | Front drive unit    | Fluid leak, test for drive unit damage                     |
| R1T,R1S  | Aug 21 - May 22   |[RCA-38-23-001-1](https://static.nhtsa.gov/odi/tsbs/2023/MC-10235543-0001.pdf) | Front drive unit    | Halfshaft bolts backing out                                |
| R1T      | Oct 21 - Dec 21   |[RCA-78-23-004-1](https://static.nhtsa.gov/odi/tsbs/2023/MC-10235546-0001.pdf) | Low voltage elec.   | Replace door mid-woofer speakers, corrosion                |
| R1T      | Oct 21 - Jun 22   |[RCA-30-23-001-1](https://static.nhtsa.gov/odi/tsbs/2023/MC-10232189-0001.pdf) | HV Battery          | Update BMS firmware, broken OTA updates                    |
| R1T,R1S  | May 22 - Nov 22   |[RCA-38-23-002-2](https://static.nhtsa.gov/odi/tsbs/2023/MC-10240310-0001.pdf) | Front drive unit    | Halfshaft washers to prevent bolts from backing out        |
| R1T,R1S  | Aug 21 - Apr 23   |[RSB-10-23-001-1](https://static.nhtsa.gov/odi/tsbs/2023/MC-10238719-0001.pdf) | Steering            | Steering wheel vibration                                   |
| R1T,R1S  | Jan 22 - Mar 23   |[RCA-10-23-002-1](https://static.nhtsa.gov/odi/tsbs/2023/MC-10235683-0001.pdf) | Steering            | Steering wheel misalignment                                |
| R1T,R1S  | Dec 22 - Mar 23   |[RCA-34-23-002-1](https://static.nhtsa.gov/odi/tsbs/2023/MC-10237165-0001.pdf) | High voltage dist.  | Unable to AC charge, faulty component                      |


# Consumables

* Windshield Wiper Blades
  * Front Right: 18"
  * Front Left: 24"
* Cabin Air Filter
  * OEM: MANN FP 23 024   210mm x 227mm x 30mm
  * Notes: Available in the [Gear Shop](https://rivian.com/gear-shop/p/cabin-air-filter).
  * Compatible: 2008 Dodge Grand Caravan
    * Part Number: CF10743
    * 10mm too short in one direction, but "close enough"
    * 199mm x 228mm x 30mm

# Legal

Rivian is a registered trademark of [Rivian](https://rivian.com).

This guide is unofficial and has no direct relationship with Rivian.
The authors will accept no responsibility if the steps in this guide break your vehicle or void your warranty.
