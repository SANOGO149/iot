# ⚡️ Supervision IoT - Station Météo Intelligente & Alerte Canicule (UFHB)

Ce dépôt contient l'infrastructure logicielle complète pour la supervision environnementale et la détection d'alertes canicule sur le campus de l'**Université Félix Houphouët-Boigny (UFHB)**.

---

## 🏗️ Architecture du Système

Le système est entièrement virtualisé et s'articule autour de 5 composants majeurs :

1. **Collecte (Edge IoT) :** Microcontrôleur ESP32 simulé intégrant des capteurs environnementaux.
2. **Transport (Broker MQTT) :** Mosquitto assure le routage asynchrone des messages.
3. **Traitement (Middleware) :** Node-RED parse les payloads JSON et applique la logique métier d'alerte.
4. **Stockage (Time-Series) :** InfluxDB v2 conserve l'historique des métriques environnementales.
5. **Visualisation (Dashboard) :** Grafana affiche les indicateurs temps réel et l'état des alertes.

---

## 🎮 Simulation Matérielle (Wokwi)

Le circuit électronique et le code embarqué de la station météo sont accessibles et simulables directement en ligne.

🔗 **[Accéder à la simulation ESP32 sur Wokwi](https://wokwi.com/projects/467393879477623809)**

Le simulateur reproduit le comportement réel de la station en publiant une payload au format JSON :

```json
{
  "temperature": 32.5,
  "humidity": 65.0,
  "pressure": 1013.2
}
```

---

## 🚀 Déploiement Local via Docker

Toute l'infrastructure de supervision (Mosquitto, Node-RED, InfluxDB, Grafana) est orchestrée via Docker Compose.

### Prérequis

* Docker & Docker Compose installés sur votre machine.

### Lancement

Pour démarrer tous les services en arrière-plan, exécutez la commande suivante à la racine du projet :

```bash
docker-compose up -d
```

### Accès aux interfaces

* **Node-RED (Middleware) :** `http://localhost:1880`
* **InfluxDB (Base de données) :** `http://localhost:8086`
* **Grafana (Supervision) :** `http://localhost:3000`

---

## 📊 Configuration de la Logique d'Alerte

La logique métier implémentée dans Node-RED filtre les données selon les seuils critiques définis pour le confort thermique du campus :

* **Température :**
  * `< 20°C` : 🟢 Vert (Frais)
  * `20°C - 35°C` : 🟠 Orange (Normal / Vigilance)
  * `> 35°C` : 🔴 Rouge (Alerte Canicule 🚨)
  
* **Humidité :** 0 à 100 % (Optimal entre 40 et 60%)
* **Pression :** Suivi barométrique standard autour de 1013 hPa.

---

## 👥 Encadrement Académique

* **Institution :** Université Félix Houphouët-Boigny (Abidjan, Côte d'Ivoire)
* **UFR :** Mathématiques et Informatique
* **Niveau :** Licence 3 Informatique
* **Superviseur :** Dr Konate

---

## 📝 License

Ce projet est développé dans un contexte académique à l'UFHB.