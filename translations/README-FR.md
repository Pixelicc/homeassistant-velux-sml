# Guide d'Intégration des Volets/Stores Velux SML

🌍 Actuellement affiché : **Français** ∙ [English](../README.md) ∙ [Deutsch](README-DE.md) ∙ [Español](README-ES.md)

> [!WARNING]
> Cette intégration nécessite le câblage manuel des volets Velux SML et d'une alimentation 24V. Un câblage incorrect pourrait entraîner des dommages matériels ou des blessures. Je n'assume aucune responsabilité pour tout dommage ou blessure causé en suivant ce guide. Procédez à vos propres risques.

## Matériel Requis

- **Alimentation 24V**
- **Sonoff 4CH Pro (R3)**

## Configuration Initiale

1. **Connexion Manuelle & Réinitialisation**  
   Connectez le volet au 24V manuellement et fermez-le complètement.

   > **Remarque :** Cela ne fonctionne que si le volet n'a jamais été connecté à une unité de contrôle Velux auparavant. Si c'est le cas, réinitialisez-le aux paramètres par défaut à l'aide de l'unité de contrôle.

2. **Câblage**
   - Connectez les fils 24V au Sonoff 4CH Pro :
     - Premier volet : Relais 1 et Relais 2
     - Deuxième volet (si utilisé) : Relais 3 et Relais 4
   - Pondez les relais et connectez-les selon le schéma de câblage ci-dessous.
   - Le Sonoff 4CH Pro et les volets reçoivent tous deux du 24V de l'alimentation.

   ```
   [Wiring Diagram Placeholder]
   ```

## Configuration Initiale du Sonoff 4CH Pro

1. Alimentez le Sonoff 4CH Pro avec l'alimentation 24V.
2. Configurez l'appareil à l'aide de l'application **eWeLink** sur votre téléphone et créez un compte cloud.
3. Connectez le Sonoff à votre réseau Wi-Fi (2.4GHz uniquement).

## Intégration Home Assistant

1. Intégrez le Sonoff 4CH Pro en utilisant [l'intégration SonoffLAN](https://github.com/AlexxIT/SonoffLAN).
2. Connectez-vous avec votre compte cloud eWeLink pour la première configuration.
3. Après la configuration initiale, configurez l'intégration pour un contrôle en local uniquement (le mode par défaut est auto, se replie sur local).
4. Vous pouvez maintenant désactiver l'accès Internet du Sonoff ; la connexion cloud n'est plus nécessaire.
5. Créez une entrée `input_number` allant de 0 à 100 avec un pas de 1 dans l'onglet des entrées (helpers) de Home Assistant.
6. Importez `blueprint-FR.yaml` dans Home Assistant ou cliquez sur le bouton intégré ci-dessous et suivez son guide.
   </br>
   [![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https://raw.githubusercontent.com/pixelicc/homeassistant-velux-sml/refs/heads/main/translations/blueprint-FR.yaml)
7. Créez une entrée `template` de volet (cover) via l'onglet des entrées de Home Assistant et configurez-la comme indiqué ci-dessous.
   </br>
   _Si les fils sont connectés à l'envers, inversez `open` et `closed` dans le modèle d'état ci-dessous. Ne le faites que si vous avez également basculé l'option `reverse` dans le blueprint._
   <img width="552" height="534" alt="Template-Cover-Helper-Screenshot-1" src="https://github.com/user-attachments/assets/802b872c-56f1-409d-8bd4-656d6f10c2b1" />
   <img width="552" height="434" alt="Template-Cover-Helper-Screenshot-2" src="https://github.com/user-attachments/assets/38540422-3ff3-46ba-b3ad-c3f3a990622a" />
   <img width="552" height="434" alt="Template-Cover-Helper-Screenshot-3" src="https://github.com/user-attachments/assets/5e62899a-25cf-49f0-af2e-daad0ec3ff33" />
   <img width="552" height="445" alt="Template-Cover-Helper-Screenshot-4" src="https://github.com/user-attachments/assets/39189d5e-0381-43b7-8f0e-d7a54c0ded39" />
   <img width="552" height="168" alt="Template-Cover-Helper-Screenshot-5" src="https://github.com/user-attachments/assets/00fcdbd7-c418-4f2c-9e63-1a45fb0bfcc0" />
   <img width="552" height="264" alt="Template-Cover-Helper-Screenshot-6" src="https://github.com/user-attachments/assets/005f1dc9-8c7e-45e7-bd6e-d7fbc597f1e7" />
   <img width="552" height="497" alt="Template-Cover-Helper-Screenshot-7" src="https://github.com/user-attachments/assets/e8d9c518-f9b6-4b27-9754-c951505afca6" />
