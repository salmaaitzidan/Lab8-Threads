# LabThreadsAsyncTask – Application Android
Salma AIT ZIDAN

## Description

Application Android développée dans le cadre d'un TP sur la programmation asynchrone. Elle montre comment exécuter des traitements longs (chargement d'image, calcul) sans bloquer l'interface utilisateur, en utilisant les **Threads** et **AsyncTask**.

---

## Fonctionnalités

- **Charger image (Thread)** : lance un thread de fond pour simuler le chargement d'une image. L'interface reste réactive pendant ce temps.
- **Calcul lourd (AsyncTask)** : exécute un calcul intensif avec affichage de la progression via une `ProgressBar`.
- **Afficher Toast** : confirme que l'UI n'est pas bloquée, même pendant un traitement en cours.

---

## Technologies utilisées

| Technologie | Utilisation |
|-------------|-------------|
| Java | Langage principal |
| Android SDK | Framework mobile |
| Thread / Runnable | Traitement en arrière-plan |
| Handler + Looper | Retour vers le UI Thread |
| AsyncTask | Calcul long avec progression |
| ProgressBar | Indicateur visuel |
| Toast | Notification rapide |

---

## Structure du projet

```
LabThreadsAsyncTask/
├── app/
│   ├── src/
│   │   └── main/
│   │       ├── java/com/example/labthreadsasynctask/
│   │       │   └── MainActivity.java
│   │       └── res/
│   │           └── layout/
│   │               └── activity_main.xml
│   └── build.gradle
└── README.md
```

---

## Concepts appris

### UI Thread
Le thread principal qui gère l'affichage et les interactions. Un traitement long ici bloque tout → risque d'ANR (Application Not Responding).

### Worker Thread
Thread de fond pour les opérations lourdes. **Interdit** de toucher directement une View depuis ce thread.

### Retour vers l'UI Thread
Trois méthodes possibles :
```java
// Option 1
view.post(runnable);

// Option 2
new Handler(Looper.getMainLooper()).post(runnable);

// Option 3
runOnUiThread(runnable);
```

### AsyncTask
Classe qui gère automatiquement les threads :
- `onPreExecute()` → UI thread, avant
- `doInBackground()` → thread de fond
- `onProgressUpdate()` → UI thread, pendant
- `onPostExecute()` → UI thread, après

---

## Lancer l'application

1. Cloner ce dépôt
2. Ouvrir avec **Android Studio**
3. Connecter un émulateur ou appareil Android
4. Cliquer sur **Run ▶**

---

## Tests réalisés

| Action | Résultat attendu |
|--------|-----------------|
| Clic "Charger image" puis "Toast" | Toast s'affiche immédiatement → UI fluide |
| Clic "Calcul lourd" | ProgressBar avance de 0 à 100 |
| Attente fin du calcul | Statut affiche le résultat numérique |

---

## Notes

- `AsyncTask` est dépréciée depuis Android 11, mais reste utilisée ici à des fins **pédagogiques**.
- Pour un projet en production, préférer `ExecutorService` ou les coroutines Kotlin.

---
