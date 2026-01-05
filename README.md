# Streamlit Never Sleep

Empêche tes applications **Streamlit** de s’endormir en les réveillant automatiquement **tous les jours à 10h (heure française)** grâce à **GitHub Actions**.

Ce projet est conçu pour les apps Streamlit hébergées sur Streamlit Cloud qui passent en *cold start* après une période d’inactivité.

---

## Fonctionnalités

- 🔔 Réveil automatique des apps Streamlit
- 🧊 Détection des *cold starts*
- 🕙 Planification quotidienne à **10h heure FR (été + hiver)**
- 🧠 Mesure du temps de réponse
- 🧾 Logs clairs dans GitHub Actions
- 💯 Gratuit (aucun serveur requis)

---

## 🧠 Comment ça marche ?

- GitHub Actions lance un script Python une fois par jour
- Le script envoie une requête HTTP vers chaque app Streamlit
- Dès la première requête, l’app commence à se réveiller
- Le script détecte si l’app était :
  - déjà réveillée
  - en cold start
  - ou en erreur

---

## Fork & installation (pas à pas)

### Fork du projet
- Clique sur **Fork** en haut à droite de ce dépôt
- Le repo sera copié sur ton GitHub

---

### Modifier les URLs Streamlit

Dans le fichier `wake.py`, remplace la liste :

```python
SITES = [
    "https://ton-app.streamlit.app/",
]
```

### Vérifier / adapter l’heure de réveil

Le workflow est configuré pour 10h heure française, été & hiver inclus.
    Fichier :
    .github/workflows/wake.yml

Si tu veux une autre heure, modifie les lignes cron.

### Activer GitHub Actions

- Va dans ton repo forké
- Onglet Actions
- Active les Actions si GitHub te le demande
- Clique sur Wake Streamlit Apps
- Lance Run workflow une première fois pour tester

### Tester manuellement

Tu peux lancer le script localement :
- pip install requests
- python wake.py

## Planification automatique

Le script est exécuté automatiquement :

Tous les jours à 10h heure française
Sans aucune action de ta part
GitHub Actions utilise l’UTC, le changement d’heure est géré via deux crons.

## Bonnes pratiques

- 1 réveil par jour est largement suffisant
- Évite les refresh agressifs
- N’utilise ce projet que pour tes propres apps

## Auteur

Tom LEPERT
