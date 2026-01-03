# DIY External Feeder–Assisted Filament Change for Bambu Lab A1 (Experimental)

![DIY AMS](images/placeholder.png) <!-- Optional image -->

## Overview

This project provides an *AMS-like filament change workflow* for the *Bambu Lab A1* using an *external feeder*, without relying on the AMS port, AMS firmware, or internal printer hardware.  

It is currently *experimental* — movements simulate filament changes, but no external hardware is required yet. Use this G-code at your own risk; it has been tested in simulation and on PLA/PETG filament for multi-material workflows.

---

## Features

- *External Feeder Integration (mocked)* – the printer executes filament change movements compatible with an external feeder.
- *Supports up to 31 filaments* – customizable X-slot positions for up to 31 spools.
- *Pressure Relief and Purge Logic* – pulsatile extrusion ensures clean filament transitions.
- *Multi-material Testing* – tested with PLA and PETG (I learned that these two materials don't like each other but I tested if it would change the nozzle temp).
- *Firmware-safe* – does not modify printer firmware or require AMS modules.

---

## Disclaimer

- *Experimental*: This G-code is not hardware-ready. Movements are mocked; the external feeder is in WIP.
- *Safety First*: Do not run on a live printer with AMS hardware unless you implement the feeder logic and sensors.
- *Filament Compatibility*: Tested with PLA and PETG only. Other materials are untested and may cause clogging or printing issues.
- *Credit*: Original filament change logic by [avatorl](https://github.com/avatorl/bambu-a1-g-code).

---

## How It Works

1. *Initialization*: Disables clog detection, sets acceleration, lifts the nozzle above the highest layer.
2. *Filament Cut & Wipe*: Retracts filament, simulates cutter movements, and performs a purge wipe.
3. *Unload / Load*: Printer waits for the external feeder to remove old filament and insert new filament (currently a timed mock pause).
4. *Filament Type Update*: Communicates new filament type to firmware with M1002 commands.
5. *Purge & Wipe*: Ensures clean transitions before resuming printing.
6. *Resume Print*: Restores acceleration, nozzle fan, and continues the print.

---

## Installation / Usage

1. Copy the G-code file into your slicer's change_filament directory.
2. Adjust any filament lengths, temperatures, or feedrates according to your printer setup.
3. Use the next_extruder variable to define which filament slot is active.
4. *Simulation recommended first* – verify that all movements and pauses match your workflow.

---

## Planned Hardware Integration

- External feeder for automated loading/unloading
- Magnetic or hall-effect sensors for filament presence detection
- PTFE guide tubes with smooth bearings for frictionless spool movement

---

## Notes

- Movements are currently *mock only*; no real feeder is integrated yet.
- Multi-material experiments (PLA & PETG) confirmed *temperature adjustments work*, but adhesion between different filament types fail.
- Up to *31 filaments supported*, but would really need it?

---

## Contributions

Contributions are welcome! If you implement hardware support, improved logic, or new materials, please fork this repository, make changes, and submit a pull request.

---

## License

This project inherits the license and credit from [avatorl’s original repository](https://github.com/avatorl/bambu-a1-g-code). This derivative work is open for experimental use and contribution.
