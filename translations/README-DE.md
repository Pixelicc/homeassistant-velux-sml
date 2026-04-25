# Velux SML Rollläden/Markisen Integrationsanleitung

> [!WARNING]
> Diese Integration erfordert die manuelle Verkabelung der Velux SML Rollläden und eines 24V-Netzteils. Eine unsachgemäße Verkabelung kann zu Geräteschäden, Sachschäden oder Personenschäden führen. Ich übernehme keine Verantwortung für Schäden oder Verletzungen, die durch das Befolgen dieser Anleitung entstehen. Die Durchführung erfolgt auf eigene Gefahr.

## Hardware-Anforderungen

- **24V Netzteil**
- **Sonoff 4CH Pro (R3)**

## Erste Einrichtung

1. **Manuelle Verbindung & Zurücksetzen**  
   Verbinden Sie den Rollladen manuell mit 24V und schließen Sie ihn vollständig.

   > **Hinweis:** Dies funktioniert nur, wenn der Rollladen noch nicht mit einer Velux-Steuereinheit verbunden war. Falls doch, setzen Sie ihn mit der Steuereinheit auf die Werkseinstellungen zurück.

2. **Verkabelung**
   - Schließen Sie die 24V-Kabel an den Sonoff 4CH Pro an:
     - Erster Rollladen: Relais 1 und Relais 2
     - Zweiter Rollladen (falls verwendet): Relais 3 und Relais 4
   - Überbrücken Sie die Relais und schließen Sie sie gemäß dem untenstehenden Schaltplan an.
   - Der Sonoff 4CH Pro und die Rollläden werden beide über das 24V-Netzteil mit Strom versorgt.

   ```
   [Wiring Diagram Placeholder]
   ```

## Sonoff 4CH Pro Erste Einrichtung

1. Versorgen Sie den Sonoff 4CH Pro über das 24V-Netzteil mit Strom.
2. Richten Sie das Gerät über die **eWeLink App** auf Ihrem Smartphone ein und erstellen Sie ein Cloud-Konto.
3. Verbinden Sie den Sonoff mit Ihrem WLAN-Netzwerk (nur 2,4 GHz).

## Home Assistant Integration

1. Integrieren Sie den Sonoff 4CH Pro über die [SonoffLAN Integration](https://github.com/AlexxIT/SonoffLAN).
2. Melden Sie sich bei der Ersteinrichtung mit Ihrem eWeLink-Cloud-Konto an.
3. Konfigurieren Sie die Integration nach der Ersteinrichtung für die rein lokale Steuerung (standardmäßig auf Auto, fällt auf lokal zurück).
4. Sie können nun den Internetzugang für den Sonoff deaktivieren; die Cloud-Verbindung wird nicht mehr benötigt.
5. Erstellen Sie im Home Assistant Helfer-Tab einen `input_number` Helfer im Bereich von 0-100 mit einer Schrittweite von 1.
6. Importieren Sie `blueprint-DE.yaml` in Home Assistant oder klicken Sie auf die untenstehende Schaltfläche und folgen Sie der Anleitung.
   </br>
   [![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https://raw.githubusercontent.com/pixelicc/homeassistant-velux-sml/refs/heads/main/translations/blueprint-DE.yaml)
7. Erstellen Sie einen `template` Cover-Helfer über den Home Assistant Helfer-Tab und konfigurieren Sie ihn wie unten gezeigt.
   </br>
   _Wenn die Kabel verkehrt herum angeschlossen sind, tauschen Sie `open` und `closed` im untenstehenden Zustandstemplate. Tun Sie dies nur, wenn Sie auch die Option `reverse` in der Blueprint aktiviert haben._
   <img width="552" height="534" alt="Template-Cover-Helper-Screenshot-1" src="https://github.com/user-attachments/assets/802b872c-56f1-409d-8bd4-656d6f10c2b1" />
   <img width="552" height="434" alt="Template-Cover-Helper-Screenshot-2" src="https://github.com/user-attachments/assets/38540422-3ff3-46ba-b3ad-c3f3a990622a" />
   <img width="552" height="434" alt="Template-Cover-Helper-Screenshot-3" src="https://github.com/user-attachments/assets/5e62899a-25cf-49f0-af2e-daad0ec3ff33" />
   <img width="552" height="445" alt="Template-Cover-Helper-Screenshot-4" src="https://github.com/user-attachments/assets/39189d5e-0381-43b7-8f0e-d7a54c0ded39" />
   <img width="552" height="168" alt="Template-Cover-Helper-Screenshot-5" src="https://github.com/user-attachments/assets/00fcdbd7-c418-4f2c-9e63-1a45fb0bfcc0" />
   <img width="552" height="264" alt="Template-Cover-Helper-Screenshot-6" src="https://github.com/user-attachments/assets/005f1dc9-8c7e-45e7-bd6e-d7fbc597f1e7" />
   <img width="552" height="497" alt="Template-Cover-Helper-Screenshot-7" src="https://github.com/user-attachments/assets/e8d9c518-f9b6-4b27-9754-c951505afca6" />
