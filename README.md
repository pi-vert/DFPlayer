# DFPlayer

## Problèmes de fiabilité

| Critère                   | **YX5200**                          | **MH2024K**                        | **GD3200B**                    |
| ------------------------- | ----------------------------------- | ---------------------------------- | ------------------------------ |
| **Origine**               | Officielle (DFRobot, YX brand)      | Clone chinois                      | Clone moderne                  |
| **Compatibilité Arduino** | ✅ Très bonne (librairie DFRobot)    | ⚠️ Partielle                       | ⚠️ Incomplète (bugs constatés) |
| **Qualité audio**         | 👍 Bonne (stable, peu de parasites) | Moyenne                            | Variable selon lot             |
| **Fonction ADKEY**        | ✅ Stable                            | ✅ Fonctionne                       | ❌ Souvent défaillante          |
| **Commandes série UART**  | ✅ Fiables                           | ⚠️ Comportement instable           | ❌ Incohérentes parfois         |
| **Disponibilité**         | Rare (plus cher)                    | Fréquente (souvent sur AliExpress) | Très fréquente depuis 2023     |
| **Documentation**         | 📘 Complète                         | 📙 Limite                          | ❌ Très peu de documentation    |

🥇 YX5200 : Meilleur choix. C’est la puce d’origine utilisée par DFRobot. Elle est parfaitement compatible avec les bibliothèques Arduino, fiable, bien documentée, et largement testée.
🥈 MH2024K : Clone fonctionnel, utilisable pour des projets simples, mais peut causer des problèmes avec les commandes série ou les fonctions avancées.
🥉 GD3200B : À éviter si possible, sauf si vous êtes prêt à contourner des bugs (ex. volume figé, mauvaise gestion des dossiers).
