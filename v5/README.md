# OBD Reader Extra

A read-only Wi-Fi dashboard for the **Ather 450 & Rizta**, running on an **ESP32 based TWAI Board** with a CAN transceiver (SN65HVD230).

This version adds one new tab, **Extra**, which shows more live details from the scooter's battery and vehicle systems.

The device only **listens** to the scooter. It never sends anything to it.

---

## Using the dashboard

1. Connect the board to the scooter as described in the original project.
2. Turn the scooter's key on.
3. Join the board's Wi-Fi network from your phone or laptop.
4. Open the dashboard in your browser (`192.168.4.1`) and tap the **Extra** tab.

The Extra tab refreshes about every 1.5 seconds while it is open. A value shows `--` or `0` until the scooter has sent that information for the first time.

---

## What the Extra tab shows

The tab is split into cards. Each card is explained below.

### Temperatures & Humidity

| Item | What it means |
|---|---|
| **Cell Temp 1 – 4** | Temperature readings from the sensors placed on the battery cells, in °C. |
| **Cell Temp 5 (unused on NMC)** | A fifth sensor input. It normally reads 0 in NMC pack because no sensor is connected. |
| **AFE Die Temp** | Temperature of the battery-monitoring chip (the analog front end) that measures the cells. |
| **BMS Ambient Temp** | Temperature of the air inside the battery management system (BMS) enclosure. |
| **Humidity** | Relative humidity measured inside the BMS, in %. |
| **FET Temp (probable)** | Temperature of the power switches (MOSFETs) that connect the battery to the scooter. |
| **ECI Temp (probable)** | Another internal BMS temperature reading. |
| **Sense Resistor Temp (probable)** | Temperature of the resistor the BMS uses to measure current. |



### Battery (Additional)

| Item | What it means |
|---|---|
| **Pack Current** | Current flowing in or out of the battery pack, in amps. At standstill it stays close to zero because only the scooter's own electronics draw power. |
| **State of Energy (SoE)** | How much usable energy is left, in %. This can differ slightly from the state of charge. |
| **SoC (EKF)** | State of charge worked out by the BMS with a more advanced estimation method (an extended Kalman filter). |
| **Max SoC** | State of charge of the fullest cell. |
| **Min SoC Est** | Estimated state of charge of the emptiest cell. |
| **Min V1 Est / Min V2 Est** | Internal estimates used by the BMS in its charge calculations. They are very small numbers near zero and are mainly useful for diagnostics. |

### Current Limits

These show how much current the BMS currently allows. They can be reduced automatically for temperature or battery state.

| Item | What it means |
|---|---|
| **Derated Discharge Current** | The maximum current the battery can deliver to the motor right now, in amps. |
| **Derated Charge Current** | The maximum current allowed into the battery while charging. |
| **Derated Regen Current** | The maximum current allowed back into the battery during regenerative braking. |
| **Discharge Limit (Temp)** | The discharge limit set by battery temperature. |
| **ChgAlg I CellRule** | Charging-current limit from the cell-level rule of the charging algorithm. |
| **ChgAlg I Cmd Rate Limited** | The charging current command after the rate limiter has been applied. |
| **ChgAlg I Post Quantizer** | A small correction value from the charging algorithm. It is mostly meaningful while charging. |

### Vehicle & Firmware

| Item | What it means |
|---|---|
| **Odometer** | Total distance the scooter has travelled, in km. |
| **BMS HW Version** | Hardware revision of the battery management board. |
| **BMS FW** | Firmware version of the battery management system. |
| **BCM FW** | Firmware version of the body control module (lights, switches and similar). |
| **Gateway FW** | Firmware version of the gateway that links the scooter's modules. |
| **Motor FW** | Firmware version of the motor controller. |
| **Battery BIN** | The battery pack's identification number. |

Firmware versions are shown as `major.minor.patch`, for example `3.12.6`.

> **Note about Battery BIN:** This data can take up to about **3 minutes** to update properly.
>
> **Why:** The scooter does not send this information continuously. The battery identification number is broadcast only now and then in the background, because it never changes while you ride. After you connect, the dashboard has to wait until the scooter sends it again, so the field may stay at `--` for a while. Keep the scooter on and the Extra tab open until it appears.

### Cell State of Charge

A table with the state of charge of each of the 14 battery cells (C1 – C14), in %.

In a healthy pack the cells are very close to each other, usually within a few tenths of a percent. A cell that is consistently far from the others can point to a balance problem.

---

## Good to know

- Values come straight from the scooter and are shown as received. Small differences from the scooter's own diagnostic screen are normal because the two are read at slightly different moments.
- Some items update more slowly than others. If a value shows `0` or `--`, give it a minute with the key on.
- The charging-related items are most meaningful while the scooter is charging.

---


## Disclaimer

This is an unofficial hobby project and is not affiliated with Ather Energy. Use it at your own risk.
