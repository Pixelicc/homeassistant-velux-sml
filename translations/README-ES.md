# Guía de Integración de Persianas/Cubiertas Velux SML

🌍 Viendo actualmente: **Español** ∙ [English](../README.md) ∙ [Deutsch](README-DE.md) ∙ [Français](README-FR.md)

> [!WARNING]
> Esta integración requiere el cableado manual de las persianas Velux SML y una fuente de alimentación de 24V. Un cableado incorrecto podría resultar en daños al equipo, daños a la propiedad o lesiones personales. No asumo ninguna responsabilidad por cualquier daño o lesión causada al seguir esta guía. Proceda bajo su propio riesgo.

## Requisitos de Hardware

- **Fuente de alimentación de 24V + Conector de barril**
- **Sonoff 4CH Pro (R3)**

## Configuración Inicial

1. **Conexión Manual y Restablecimiento**  
   Conecte la persiana a 24V manualmente y deje que se cierre y se abra por completo para establecer los puntos finales.

   > **Nota:** Esto solo funciona si la persiana no se ha conectado a una unidad de control Velux anteriormente. Si es así, restablézcala a los valores predeterminados utilizando la unidad de control.

2. **Cableado**
   - Conecte la fuente de alimentación de 24V al Sonoff 4CH Pro a través de un conector de barril:
     - Primera persiana: Relé 1 y Relé 2
     - Segunda persiana (si se usa): Relé 3 y Relé 4
   - Conecte los relés según el diagrama de cableado a continuación.
   - El Sonoff 4CH Pro y las persianas reciben 24V de la fuente de alimentación. La fuente de alimentación de 24V debe dividirse en 2-3 cables para alimentar tanto el Sonoff a través de un conector de barril como las persianas directamente.

   <img width="306" height="286" alt="image" src="https://github.com/user-attachments/assets/45f6cba8-faf6-445d-9808-4aa0122c0be7" />

## Configuración Inicial del Sonoff 4CH Pro

1. Encienda el Sonoff 4CH Pro con la fuente de alimentación de 24V.
2. Configure el dispositivo usando la aplicación **eWeLink** en su teléfono y cree una cuenta en la nube.
3. Conecte el Sonoff a su red Wi-Fi (solo 2.4GHz).

## Integración en Home Assistant

1. Integre el Sonoff 4CH Pro usando la [integración SonoffLAN](https://github.com/AlexxIT/SonoffLAN).
2. Inicie sesión con su cuenta en la nube de eWeLink para la primera configuración.
3. Después de la configuración inicial, configure la integración para control solo local (por defecto es auto, pero cambia a local).
4. Ahora puede desactivar el acceso a internet para el Sonoff; la conexión a la nube ya no es necesaria.
5. Cree un ayudante (helper) `input_number` que vaya de 0 a 100 con un paso de 1 en la pestaña de ayudantes de Home Assistant.
6. Importe `blueprint-ES.yaml` en Home Assistant o haga clic en el botón incrustado a continuación y siga su guía.
   </br>
   [![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https://raw.githubusercontent.com/pixelicc/homeassistant-velux-sml/refs/heads/main/translations/blueprint-ES.yaml)

   > [!NOTE]
   > Intente no abrir, cerrar o establecer la posición de la persiana desde Home Assistant con demasiada rapidez, ya que esto puede hacer que la persiana pierda su punto final aprendido y requiera un reinicio completo.

7. Cree un ayudante de persiana (cover) `template` a través de la pestaña de ayudantes de Home Assistant y configúrelo como se muestra a continuación.
   </br>
   _Si los cables están conectados al revés, cambie `open` y `closed` en la plantilla de estado a continuación. Solo haga esto si también activó la opción `reverse` en el blueprint._
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
