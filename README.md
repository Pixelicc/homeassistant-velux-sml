# Velux SML Shutters/Covers Integration Guide

🌍 Currently viewing **English** ∙ [Deutsch](translations/README-DE.md) ∙ [Español](translations/README-ES.md) ∙ [Français](translations/README-FR.md)

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
   </br>
   _If wires are connected in reverse, switch `open` and `closed` in the state template below. Only do this if you also toggled the `reverse` option in the blueprint._
   <img width="552" height="534" alt="Template-Cover-Helper-Screenshot-1" src="https://github.com/user-attachments/assets/802b872c-56f1-409d-8bd4-656d6f10c2b1" />
   ```jinja2
   {% set switch1 = states('switch.SONOFF_SWITCH_ENTITY_1') %}
   {% set switch2 = states('switch.SONOFF_SWITCH_ENTITY_2') %}
   {% if switch1 == 'on' and switch2 == 'on' %}
      open
   {% else %}
      closed
   {% endif %}
   ```
   <img width="552" height="434" alt="Template-Cover-Helper-Screenshot-2" src="https://github.com/user-attachments/assets/38540422-3ff3-46ba-b3ad-c3f3a990622a" />
   <img width="552" height="434" alt="Template-Cover-Helper-Screenshot-3" src="https://github.com/user-attachments/assets/5e62899a-25cf-49f0-af2e-daad0ec3ff33" />
   <img width="552" height="445" alt="Template-Cover-Helper-Screenshot-4" src="https://github.com/user-attachments/assets/39189d5e-0381-43b7-8f0e-d7a54c0ded39" />
   <img width="552" height="168" alt="Template-Cover-Helper-Screenshot-5" src="https://github.com/user-attachments/assets/00fcdbd7-c418-4f2c-9e63-1a45fb0bfcc0" />
   ```jinja2
   {{ states('input_number.YOUR_INPUT_NUMBER_HELPER') }}
   ```
   <img width="552" height="264" alt="Template-Cover-Helper-Screenshot-6" src="https://github.com/user-attachments/assets/005f1dc9-8c7e-45e7-bd6e-d7fbc597f1e7" />
   ```yaml
   action: script.velux_sml_control_script
   data:
      action: Position
      requested_position: "{{ position }}"
   ```
   <img width="552" height="497" alt="Template-Cover-Helper-Screenshot-7" src="https://github.com/user-attachments/assets/e8d9c518-f9b6-4b27-9754-c951505afca6" />
   ```jinja2
   {{ has_value('switch.SONOFF_SWITCH_ENTITY_1') and has_value('switch.SONOFF_SWITCH_ENTITY_2') }}
   ```
