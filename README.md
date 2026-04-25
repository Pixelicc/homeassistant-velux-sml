# Velux SML Shutters/Covers Integration Guide

> [!WARNING]
> This integration requires manual wiring of the Velux SML covers and a 24V power supply. Incorrect wiring could result in equipment damage, property damage, or personal injury. I do not take any responsibility for any damage or injury caused by following this guide. Proceed at your own risk.

## Hardware Requirements

- **24V Power Supply**
- **Sonoff 4CH Pro (R3)**

## Initial Setup

1. **Manual Connection & Reset**  
   Connect the cover to 24V manually and fully close it.

   > **Note:** This only works if the cover has not been connected to a Velux control unit before. If it has, reset it to default using the control unit.

2. **Wiring**
   - Connect the 24V wires to the Sonoff 4CH Pro:
     - First cover: Relay 1 and Relay 2
     - Second cover (if used): Relay 3 and Relay 4
   - Bridge the relays and connect according to the wiring diagram below.
   - The Sonoff 4CH Pro and the covers both receive 24V from the power supply.

   ```
   [Wiring Diagram Placeholder]
   ```

## Sonoff 4CH Pro Inital Setup

1. Power the Sonoff 4CH Pro with the 24V power supply.
2. Set up the device using the **eWeLink app** on your phone and create a cloud account.
3. Connect the Sonoff to your Wi-Fi network (2.4GHz only).

## Home Assistant Integration

1. Integrate the Sonoff 4CH Pro using the [SonoffLAN integration](https://github.com/AlexxIT/SonoffLAN).
2. Log in with your eWeLink cloud account for the first setup.
3. After initial setup, configure the integration for local-only control (defaults to auto, falls back to local).
4. You can now disable internet access for the Sonoff; the cloud connection is no longer needed.
5. Create an `input_number` helper that ranges from 0-100 with a step of 1 in the Homeassistant helpers tab.
6. Import `blueprint.yaml` into Home Assistant or click on the embedded button below and follow its guide.
   </br>
   [![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https://raw.githubusercontent.com/pixelicc/homeassistant-velux-sml/refs/heads/main/blueprint.yaml)
7. Create a `template` cover helper via the Homeassistant helpers tab and configure it as shown below.
