# Replacing the 12V Low Voltage battery

![wip](../../status_wip.png)

> WARNING: This article is a work in progress based on limited information. Only advanced users should
> follow these steps until they are better defined.

**Difficulty:** 2/5

## Applies

  * 2022-2026 Rivian R1T / Rivian R1S

## Diagnosis

![Replace 12V Battery](warning-12v.jpg)

  * "Replace 12V Battery" on driver display
  * Unresponsive vehicle refusing to unlock? See [12V emergency power](emergency-jump.md)

## Cause

  * One or more (depending on build date) of the 12V batteries are failing.

## Parts

> Early R1 vehicles (Built 3/23 and before) require two batteries. Later builds
> use a capacitor on the passenger-side, and a single battery.

* Replacement Battery
  * **Drop-in Third Party:** [OHMMU BT19](https://www.ohmmu.com/product-page/12v-lithium-battery-for-r1t-r1s)
  * **Universal / local Third Party:**
    * [12v, Deep Cycle](https://www.batteriesplus.com/productdetails/sladc12=20c)
    * [Reusable Post Relocator](https://soonishev.com/products/battery-post-relocator)
    * [Extended M5 bolt](https://amzn.to/4p4BCfF)
    * [10mm spacer, 5mm ID, 10mm OD](https://amzn.to/3LVKuWo)
  * **OEM:** C&D DCS-18UNC
    * May be able to purchase from a [dealer](https://www.cdtechno.com/contact-us/locations)
* Blue painters tape

> Note: If you choose to replace the Lead Acid, 12V AGM battery with a LifePo4 battery, take note that charging a LifePo4 battery in freezing conditions **WILL** damage it.  Only use **heated** LifePo4 batteries such as the Ohmmu.

## Tools

  * [Mechanic gloves](https://amzn.to/3LwpO7d)
  * [Electrical tape](https://amzn.to/4oIQMqM)
  * [10mm socket, 13mm socket, and wrench](https://amzn.to/47crE5V) (insulated handle nice to have, but not required)
  * [Plastic clip remover (optional)](https://amzn.to/3L8OWAW)

## Context

### Dual Battery (Early R1, 3/23 and before)

![Dual Battery](12v-dual.jpg)

  1. DC/DC Converter Primary (low voltage power from high voltage battery)
  2. Power Distribution Primary
  3. DC/DC Converter Secondary (low voltage power from high voltage battery)
  4. Power Distribution Secondary
  5. Electric Power Assisted Steering Primary
  6. Electric Power Assisted Steering Secondary

#### Observations

  * Appears that most low voltage vehicle power "passes through" this area.
  * 13A from terminal 3 to terminal 4 while HVAC running and vehicle idle

### Single Battery (Later R1)

> TODO

## Procedure

### Validate Number of 12V Batteries

> TODO photo

  1. Open the front trunk, remove the plastic cover at the top of the space by lifting each edge to unsnap it.
  2. Locate the batteries at the center of the space (just behind the frunk compartment wall)
  3. If in question, determine if you have a single or dual battery design by examining the passenger side.
     1. If the passenger side terminal is black, you have an older build with two batteries. Follow **Passenger Side Battery** and **Drivers Side Battery** below.
     2. if the passenger side terminal is red, you have a later build with a non-replaceable capacitor on the passenger side. Jump to **Drivers Side Battery** below.

### Preparation

  1. Ensure the vehicle is on stable, level ground.
  2. Ensure doors are unlocked, and the frunk is open.
  3. Place the vehicle into service mode.
  4. Locate the red high voltage disconnect cable in the top right portion of the frunk.  Release the clip and pull the loop connector.
  5. Using a flat-head screwdriver, carefully remove the plastic red covers from the top of the battery terminals.
  6. Take a clear photo of your batteries, notating where all wires go.

### Passenger Side Battery (Dual Battery)

> TODO photos

> You may need to remove both batteries at once

  1. Remove the negative terminal from the battery, and place blue painters tape over it.
  2. Remove the positive terminal from the battery, and place tape over the top of the battery terminal.
  3. Remove the DC/DC converter wire from the terminal block, as well as the wires from the top of the block. Tape each one.
  4. Remove the bracket retaining the battery.
  5. Remove the old battery.
     1. You may need to also remove the drivers side battery at this point to fit the new batteries into the small space.
  6. Install the new battery, Negative on the passenger side.
  7. Secure the battery down with the bracket.
  8. Attach the positive terminal block to the battery.
     1. You may need to "rotate" post relocators, if you do ensure the battery terminal is snug before continuing.
  9. Re-attach all positive wires unwrapping them one by one.
  10. Carefully attach the negative terminal. It may spark.
  11. Ensure all terminals are snug.


### Drivers Side Battery

> TODO photos

  1. Remove the negative terminal from the battery, and place blue painters tape over it.
  2. Remove the positive terminal from the battery, and place tape over the top of the battery terminal.
  3. Remove the DC/DC converter wire from the terminal block, as well as the wires from the top of the block. Tape each one.
  4. Remove the bracket retaining the battery.
  5. Remove the old battery.
  6. Install the new battery, Negative on the drivers side.
  7. Secure the battery down with the bracket.
  8. Attach the positive terminal block to the battery.
     1. You may need to "rotate" post relocators, if you do ensure the battery terminal is snug before continuing.
  9. Re-attach all positive wires unwrapping them one by one.
  10. Carefully attach the negative terminal. It may spark.
  11. Ensure all terminals are snug.
  12. Carefully re-attach the HV disconnect loop and secure the clip.

### Recovery.

> TODO photos

  1. Once the batteries are in the vehicle, enter the cabin and perform a hard reset. (hold the left-most steering wheel button and the emergency blinker button)
  2. Once the vehicle recovers, go into RiDE and perform a 12v low-voltage reset.

