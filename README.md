# DFPlayer

# ESP32 + DFPlayer Mini

Ce projet utilise un **ESP32** et un **DFPlayer Mini** pour lire des fichiers audio depuis une carte micro-SD, avec possibilité de contrôler la lecture via ESPHome et Home Assistant.

---

## ⚡ Connexions principales

- **Alimentation**
  - `VCC` → 5V (ou 3,3V selon version)
  - `GND` → masse commune

- **UART (contrôle série avec ESP32)**
  - `RX` (DFPlayer) ← `TX` de l’ESP32 (via résistance 1 kΩ conseillée)
  - `TX` (DFPlayer) → `RX` de l’ESP32

- **Sorties audio**
  - `SPK_1` et `SPK_2` → haut-parleur 3W (⚠️ pas de masse commune, sortie amplifiée)
  - `DAC_R` et `DAC_L` → sortie audio niveau ligne (vers ampli externe, entrée AUX, etc.)

- **Autres**
  - `BUSY` (ou IO1) → signal bas quand une piste est en lecture
  - `IO2` (ou ADKEY1) → entrée pour boutons/potentiomètre (mode autonome)

---

## 📐 Schéma de câblage simplifié

```text

                +-------------------+
                |    DFPlayer Mini  |
                |                   |
        VCC ----| VCC           SPK1|----> Haut-parleur +
        GND ----| GND           SPK2|----> Haut-parleur -
 ESP32 TX ----->| RX            DACR|----> Ampli externe (droite)
 ESP32 RX <-----| TX            DACL|----> Ampli externe (gauche)
                | BUSY/IO1      IO2 |
                +-------------------+

```

---

## 🚀 Utilisation avec ESPHome

Exemple de configuration YAML :

```yaml
uart:
  tx_pin: GPIO17
  rx_pin: GPIO16
  baud_rate: 9600

dfplayer:
  uart_id: uart_bus
```

---

## 🔊 Notes importantes

- Les sorties **SPK1/SPK2** sont amplifiées → à utiliser uniquement avec un petit haut-parleur (4Ω / 3W).  
- Les sorties **DAC_L/DAC_R** sont en niveau ligne → pour un ampli externe ou une entrée AUX.  
- Les deux types de sorties fonctionnent **en même temps**, mais le signal est identique.  
- Ne jamais relier **SPK1/SPK2** au GND !

---

## 📂 Licence

Projet open-source (MIT). Libre d’utilisation et de modification.


# Problèmes de fiabilité

| Critère                   | **YX5200**                          | **MH2024K**                        | **GD3200B**                    |
| ------------------------- | ----------------------------------- | ---------------------------------- | ------------------------------ |
| **Origine**               | Officielle (DFRobot, YX brand)      | Clone chinois                      | Clone moderne                  |
| **Compatibilité Arduino** | ✅ Très bonne (librairie DFRobot)    | ⚠️ Partielle                       | ⚠️ Incomplète (bugs constatés) |
| **Qualité audio**         | 👍 Bonne (stable, peu de parasites) | Moyenne                            | Variable selon lot             |
| **Fonction ADKEY**        | ✅ Stable                            | ✅ Fonctionne                       | ❌ Souvent défaillante          |
| **Commandes série UART**  | ✅ Fiables                           | ⚠️ Comportement instable           | ❌ Incohérentes parfois         |
| **Disponibilité**         | Rare (plus cher)                    | Fréquente (souvent sur AliExpress) | Très fréquente depuis 2023     |
| **Documentation**         | 📘 Complète                         | 📙 Limite                          | ❌ Très peu de documentation    |

- 🥇 YX5200 : Meilleur choix. C’est la puce d’origine utilisée par DFRobot. Elle est parfaitement compatible avec les bibliothèques Arduino, fiable, bien documentée, et largement testée.
- 🥈 MH2024K : Clone fonctionnel, utilisable pour des projets simples, mais peut causer des problèmes avec les commandes série ou les fonctions avancées.
- 🥉 GD3200B : À éviter si possible, sauf si vous êtes prêt à contourner des bugs (ex. volume figé, mauvaise gestion des dossiers).
