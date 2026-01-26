# Streamlit Never Sleep

Empêche tes applications **Streamlit** de s’endormir en les réveillant automatiquement **tous les jours à 10h (heure française)** grâce à **GitHub Actions + Playwright**.

Ce projet est conçu pour les apps Streamlit hébergées sur **Streamlit Cloud** qui passent en *cold start* après une période d’inactivité — **même quand un bouton doit être cliqué pour lancer l’app**.

---

## Fonctionnalités

* Réveil automatique des apps Streamlit
* Gestion des *cold starts*
* Planification quotidienne à **10h heure FR (été + hiver)**
* Ouverture réelle de la page via navigateur headless
* Clic automatique sur le bouton de démarrage
* Logs clairs dans GitHub Actions
* Gratuit (aucun serveur requis)

---

## Comment ça marche ?

* GitHub Actions lance un script Python une fois par jour
* Le script utilise **Playwright** pour :

  * ouvrir chaque app Streamlit dans un navigateur headless
  * attendre que l’UI soit prête
  * cliquer automatiquement sur le bouton ("yes", "get it", "start", etc.)
* Cela force un **vrai rerun Streamlit**
* L’app est ainsi pleinement réveillée

---

## Fork & installation (pas à pas)

### Fork du projet

* Clique sur **Fork** en haut à droite de ce dépôt
* Le repo sera copié sur ton GitHub

---

### Modifier les URLs Streamlit

Dans le fichier `wake.py`, remplace la liste :

```python
SITES = [
    "https://ton-app.streamlit.app/",
]
```

---

### Adapter les mots-clés du bouton

Dans `wake.py`, ajuste la liste `KEYWORDS` pour correspondre au texte réel du bouton à cliquer :

```python
KEYWORDS = [
    "yes",
    "get it",
    "back up",
    "start",
    "run",
    "launch",
]
```

> Le script cherche un bouton contenant l’un de ces mots (insensible à la casse).
> S’il n’en trouve aucun, il clique le premier bouton visible.

---

### Vérifier / adapter l’heure de réveil

Le workflow est configuré pour **10h heure française** (été & hiver inclus).

Fichier : `.github/workflows/wake.yml`

```yaml
on:
  schedule:
    # Heure d'été (CEST = UTC+2) → 10h Paris = 08h UTC
    - cron: "0 8 * 3-10 *"
    # Heure d'hiver (CET = UTC+1) → 10h Paris = 09h UTC
    - cron: "0 9 * 11,12,1,2 *"
  workflow_dispatch:
```

> GitHub Actions fonctionne en **UTC**.
> Le changement d’heure est géré via deux crons.

---

### Activer GitHub Actions

* Va dans ton repo forké
* Onglet **Actions**
* Active les Actions si GitHub te le demande
* Clique sur **Wake Streamlit Apps**
* Lance **Run workflow** une première fois pour tester

---

## Tester localement

```bash
pip install playwright
python -m playwright install chromium
python wake.py
```

---

## Planification automatique

Le script est exécuté automatiquement :

* Tous les jours à **10h heure française**
* Sans aucune action de ta part
* Même si l’app Streamlit attend un clic utilisateur

---

## Bonnes pratiques

* 1 réveil par jour est largement suffisant
* Évite les refresh agressifs
* Ajoute des mots-clés spécifiques à ton bouton
* N’utilise ce projet que pour tes propres apps

---

## Dépannage

### Le bouton n’est pas cliqué

* Vérifie le texte réel du bouton
* Ajoute un mot-clé plus précis dans `KEYWORDS`
* Regarde les logs GitHub Actions

---

##
