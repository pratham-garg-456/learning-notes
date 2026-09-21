---
title: Peripherals and Ports
---

# Peripherals and Ports

## What are connectors and peripherals?

A connector is a physical plug and socket that joins two devices together. Peripherals are any external devices you connect to your computer: keyboard, mouse, monitor, printer, phone, and so on.

Think of connectors like different plugs in your house (a wall outlet, a TV cable socket, a phone jack): each is designed for a specific purpose and not interchangeable.

## USB connectors

USB (Universal Serial Bus) is called "universal" because it was designed to replace the many different connector types of the 1990s with one standard. It became the most common connector in the world. USB does two things at once:

- transfers data between devices,
- delivers power to devices.

### USB Type A generations

These are the rectangular USB ports on computers:

- **USB 2.0**: black port, 480 Mbps. Still fine for keyboards, mice, and basic flash drives that don't move large files.
- **USB 3.0**: blue port, 5 Gbps. About 10 times faster than USB 2.0. Good for external hard drives and fast flash drives.
- **USB 3.1**: teal port, 10 Gbps. Twice as fast as USB 3.0. Used for high-speed external SSDs and demanding peripherals.

**Backwards compatibility** is an important feature: any USB device works in any USB port regardless of generation. If you plug a USB 3.0 device into a USB 2.0 port, it works but runs at USB 2.0 speed. The port and cable negotiate and settle on the fastest speed they both support, like two people speaking whatever language they both know.

### Smaller modern USB connectors

- **Micro USB**: the small connector used on older Android phones, cameras, and portable devices before USB-C. It could only be inserted one way, so you'd often fumble plugging it in.
- **USB-C**: the current modern standard. It is completely symmetrical, so you can plug it in either way up. It is also more capable:
    - transfers data at up to 20 Gbps
    - delivers much more power (can charge laptops, not just phones)
    - can carry a video signal (one USB-C cable can connect a monitor)
    - smaller and more durable than older connectors
- **USB4 (Thunderbolt)**: the fastest version, 40 Gbps. Uses the same physical USB-C connector with a much faster protocol underneath. Used for professional equipment, high-resolution external monitors, and ultra-fast external storage. Thunderbolt ports have a small lightning bolt icon.
- **Lightning port**: Apple's proprietary connector on iPhones and iPads (older models). Reversible and compact like USB-C, but exclusively Apple's. Apple has been moving to USB-C on newer devices, making Lightning gradually obsolete.

## Communication connectors

These connect devices to networks and the internet rather than to peripherals.

### POTS and RJ-11

POTS (Plain Old Telephone Service) is the traditional copper wire telephone network that has existed for over a century. It carries voice as analog electrical signals through twisted pairs of copper wire.

The **RJ-11** connector is the small 4-pin connector on landline telephone cables. Still used for:

- landline telephones
- old dial-up internet modems
- alarm systems
- fax machines

### DSL and RJ-45

DSL (Digital Subscriber Line) uses the same copper telephone wires as POTS but sends digital data at much higher frequencies, so internet and phone can share the same wire.

**RJ-45** is the connector for ethernet network cables. It looks like a wider RJ-11, with 8 pins instead of 4. It is the standard wired internet connection in offices, homes with wired networks, and data centers, and it is much more reliable than WiFi for stable high-speed connections.

### Cable internet and the F-type connector

Cable internet uses the same coaxial cable infrastructure originally built for cable TV. The **F-type connector** is the screw-on metal connector on the back of cable modems and TV cable boxes. You screw it clockwise to lock it in place, giving a very secure connection that doesn't accidentally unplug.

### Fiber optic

Fiber optic cables carry pulses of light through extremely thin glass fibers instead of electrical signals. Advantages over copper:

- massively higher speeds (terabits per second)
- much longer distances without signal degradation
- not affected by electrical interference
- more secure, since it is harder to tap

This is why major internet providers use fiber for their backbone infrastructure. When fiber reaches your home directly it is called FTTP (Fiber To The Premises), commonly marketed as "fiber broadband".

## Legacy device connectors

Legacy means old technology that is no longer the current standard but still exists in older equipment.

- **DB9**: a D-shaped connector with 9 pins, used for older peripherals like keyboards, mice, and joysticks before USB. You might still meet it on old industrial equipment, legacy point-of-sale systems, older networking equipment, and some scientific instruments. IT professionals need to recognize these because businesses sometimes still run old equipment.
- **Molex**: a large 4-pin power connector used inside computers to power internal components. Older HDDs, optical drives, and some fans used it. Modern drives mostly use SATA power connectors, but Molex still appears with some graphics card adapters and older components.

## Punch down blocks

A punch down block is specialized networking hardware used in professional settings such as offices, buildings, and data centers. It is a panel with rows of metal slots where you "punch down" bare copper wire using a special tool. The slot's metal teeth bite through the insulation and make a reliable electrical connection without stripping wires or using screws.

Used for:

- telephone systems: connecting many phone lines in an office
- ethernet networks: organizing and distributing network cables throughout a building
- structured cabling systems in data centers

Think of it as a central junction box: all the individual cable runs from offices and rooms come back to a punch down block, where they are organized and connected to the network equipment.

IT professionals use these when setting up office phone systems, installing or expanding ethernet networks, moving a connection from one location to another, and troubleshooting network connectivity.

## Summary table

| Connector | Used for | Speed / purpose |
| --- | --- | --- |
| USB 2.0 | Keyboards, mice, basic drives | 480 Mbps |
| USB 3.0 | External drives, fast peripherals | 5 Gbps |
| USB 3.1 | High-speed external storage | 10 Gbps |
| USB-C | Modern phones, laptops, monitors | 20 Gbps + power |
| USB4/Thunderbolt | Professional equipment | 40 Gbps |
| Lightning | Apple devices only | Charging + data |
| RJ-11 | Landline phones, dial-up | Voice / slow data |
| RJ-45 | Wired ethernet internet | Network connection |
| F-Type | Cable TV, cable modems | Cable internet |
| Fiber optic | Internet backbone, fast broadband | Extremely high speed |
| DB9 | Legacy old peripherals | Obsolete |
| Molex | Internal power delivery | Power only |
| Punch down | Office phone and network wiring | Organization and connection |

## Practice Questions

??? question "1. Why is USB called universal, and what two things does it do?"

    It was designed to replace the many different connector types of the 1990s with one standard. It transfers data and delivers power.

??? question "2. What are the speeds and port colors of USB 2.0, 3.0, and 3.1?"

    USB 2.0 is black at 480 Mbps, USB 3.0 is blue at 5 Gbps, and USB 3.1 is teal at 10 Gbps.

??? question "3. What happens if you plug a USB 3.0 device into a USB 2.0 port?"

    It works, but at USB 2.0 speed. USB is backwards compatible: the port and cable settle on the fastest speed both support.

??? question "4. What makes USB-C better than Micro USB?"

    It is symmetrical (plugs in either way), faster (up to 20 Gbps), delivers far more power (can charge laptops), can carry video, and is smaller and more durable.

??? question "5. What is the difference between RJ-11 and RJ-45?"

    RJ-11 is the small 4-pin connector for landline phones, dial-up modems, alarms, and fax machines. RJ-45 is the wider 8-pin connector for ethernet network cables.

??? question "6. Why is fiber optic better than copper?"

    It carries light instead of electricity, so it has far higher speeds, longer distances without degradation, immunity to electrical interference, and better security. That is why it is used for internet backbones.

??? question "7. What is a punch down block used for?"

    Connecting bare copper wires by punching them into metal slots, to organize and distribute phone and ethernet cabling in offices and data centers.
