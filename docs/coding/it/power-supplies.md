---
title: Power Supplies
---

# Power Supplies

## What a power supply actually does

Every device in a computer (CPU, RAM, storage drives, fans, graphics card) needs electricity to run. But the electricity from a wall outlet is completely different from what computer components need.

**Wall outlet electricity:**

- AC (Alternating Current): the current constantly reverses direction, switching back and forth 50 to 60 times per second.
- High voltage: 120V in North America, 220 to 240V in Europe.

**Computer components need:**

- DC (Direct Current): current flows in one steady direction only.
- Low voltage: typically 3.3V, 5V, or 12V depending on the component.

The **Power Supply Unit (PSU)** sits in between and does the conversion, taking the high voltage AC from the wall and transforming it into the low voltage DC that components can safely use.

Think of a water treatment plant: raw water isn't safe to drink directly, so it is processed and cleaned before reaching your tap. The PSU processes raw wall electricity before it reaches your components.

## Physical components of a PSU

- **Fan**: the conversion generates heat, so every PSU has a built-in fan. Some modern PSUs only spin the fan when the unit gets hot enough, staying silent during light use.
- **Voltage information label**: a sticker on the side listing exactly what voltages and currents the PSU outputs on each rail. Important for checking that it meets your system's requirements.
- **Cables**: multiple cables connect to different components:
    - Main 24-pin cable → motherboard
    - 8-pin CPU cable → processor
    - SATA power cables → storage drives
    - PCIe power cables → graphics card
    - Molex connectors → older devices, case fans
- **Modular vs non-modular**: some PSUs have fixed cables (all attached permanently), while modular PSUs let you connect only the cables you need, reducing clutter inside the case.

## Electricity concepts

### Voltage

Voltage is electrical pressure: the force that pushes electricity through a circuit. In the water analogy, voltage is the water pressure in the pipe.

- Too low voltage: components don't get enough power to function, and the system becomes unstable or won't start.
- Too high voltage: components get damaged or burn out.
- Correct voltage: everything runs perfectly.

This is why you can't plug any device into any power source: a device designed for 5V will be destroyed by 12V, just like a garden hose designed for low pressure would burst under fire hydrant pressure.

Different components need different voltages:

- RAM and some motherboard circuits: 3.3V
- USB ports, some drives: 5V
- CPU, graphics card, motors: 12V

### Current (amperage)

If voltage is pressure, current is the actual flow: how much electricity moves through the wire per second, measured in **amps (A)**. In the water analogy, it is gallons per minute flowing through the pipe.

Current affects:

- How fast a device charges (higher current means faster charging, which is why fast chargers advertise higher amperage).
- How much work a device can do simultaneously.
- How thick wires need to be: higher current requires thicker wires, just like high flow water needs wider pipes. Thin wires carrying too much current overheat and can cause fires.

### Wattage

Wattage is voltage multiplied by current:

**Watts = Volts × Amps**

It represents the total power being consumed or delivered, combining pressure and flow into one number.

- A basic office PC might use 200 to 300 watts.
- A gaming PC with a powerful graphics card might use 500 to 800 watts.
- A high-end workstation might use 1000+ watts.

Wattage is the number you care about most when choosing a PSU: its rating must exceed your system's total power consumption.

## Power requirements

### Choosing the right wattage

Every component consumes a certain amount of watts. Add them up:

- CPU: 65 to 250W depending on model
- Graphics card: 100 to 450W for high-end cards
- RAM: 2 to 5W per stick
- Storage drives: 2 to 10W each
- Motherboard: 20 to 80W
- Fans and cooling: 5 to 30W

Then add a buffer, typically 20 to 30% headroom above the calculated total. If your components need 500W, a 650W PSU is appropriate.

**Why headroom matters:**

- PSUs run most efficiently and coolest at around 50 to 80% load.
- It leaves room for power spikes when components suddenly work hard.
- It allows future upgrades without replacing the PSU.

### Can a PSU give too much power?

A common misconception: a larger PSU does **not** force extra power into components. Components only draw what they need. A 1000W PSU powering a 300W system just runs very efficiently at low load, like a powerful engine you don't have to floor. The danger is only in the other direction: a PSU that is too small gets pushed beyond its limits.

## Power supply failures

PSUs are one of the more commonly failing components. Several things can kill them:

- **Burnout**: running a PSU at or near maximum capacity for extended periods generates enormous heat and degrades internal components over time. Adequate headroom extends its lifespan.
- **Power surges**: a sudden voltage spike from the wall (lightning, grid fluctuations, large appliances switching on) can overwhelm a PSU's internal components instantly. Quality PSUs have built-in surge protection and sacrifice themselves to protect your components, like a fuse.
- **Lightning strikes**: a direct or nearby strike can send an enormous spike through your power line. Even surge protectors sometimes can't handle a direct strike, which is why unplugging computers during electrical storms is still the safest option.
- **Capacitor aging**: PSUs contain capacitors that store and regulate electrical charge. They degrade over years of use, causing increasingly unstable power, leading to random crashes, freezes, and eventually failure.

**Signs a PSU is failing:**

- Random system crashes or restarts with no other explanation
- The computer won't start but other components seem fine
- A burning smell from the PSU
- Instability only under heavy load
- Visible burn marks or bulging on the PSU

**Why PSU diagnosis is an important IT skill.** A failing PSU can cause symptoms that look like other problems: random crashes might look like a software issue, and failure to start might look like a motherboard problem. An experienced technician checks the PSU early because it affects every component. A bad PSU can also damage other components by delivering unstable or incorrect voltages, which makes early diagnosis even more critical.

## Practice Questions

??? question "1. What does a PSU do?"

    It converts high-voltage AC from the wall into the low-voltage DC (3.3V, 5V, or 12V) that computer components can safely use.

??? question "2. Explain voltage, current, and wattage with the water analogy."

    Voltage is the water pressure, current (in amps) is how much water flows per second, and wattage is pressure times flow: Watts = Volts × Amps, the total power delivered.

??? question "3. How do you choose a PSU wattage?"

    Add up the wattage of all components, then add 20 to 30% headroom. If the components need 500W, a 650W PSU is appropriate. Headroom keeps the PSU efficient and cool, covers power spikes, and allows upgrades.

??? question "4. Does a much larger PSU force extra power into your components?"

    No. Components only draw what they need. The danger is a PSU that is too small.

??? question "5. What can kill a PSU, and what are the signs of a failing one?"

    Burnout from running near maximum capacity, power surges, lightning strikes, and capacitor aging. Signs: random crashes or restarts, not starting, a burning smell, instability under load, and burn marks or bulging.

??? question "6. Why should an IT technician check the PSU early?"

    A failing PSU can mimic software or motherboard problems, and it can damage other components with unstable voltage.
