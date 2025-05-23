# 🩺 Prédiction des Frais d'Assurance Santé avec Interprétation des Modèles

Dans ce projet, nous construisons un **modèle de machine learning prédictif** afin d’estimer les *frais d’assurance santé* à partir de données clients (âge, sexe, IMC, nombre d’enfants, statut fumeur, région). L’objectif est de simuler le travail d’un data scientist dans une compagnie d’assurance : prédire les coûts médicaux futurs pour mieux tarifer, gérer les risques et personnaliser les offres.

## 🛠 Étapes du projet

Ce notebook suit une approche complète et structurée :

1. **Exploration des données (EDA)** : comprendre les distributions, corrélations, et particularités des variables.
2. **Prétraitement** : encodage binaire (`sex`, `smoker`), One-Hot Encoding (`region`), ajout de variables d’interaction (`age_smoker`, `bmi_sex`).
3. **Modélisation** :
   - Modèle de base : `RandomForestRegressor` (bon benchmark)
   - Modèle avancé : `XGBoostRegressor` avec `GridSearchCV`, régularisation (`reg_alpha`, `reg_lambda`) et validation croisée
4. **Évaluation** :
   - Indicateurs utilisés : R², MSE, MAE
   - Analyse des performances par segments (fumeur vs non-fumeur, sexe, régions)
5. **Interprétabilité des modèles** :
   - ✅ **Importance globale** des variables (XGBoost `plot_importance`)
   - ✅ **SHAP** pour une interprétation *globale* (impact de chaque variable sur toutes les prédictions)
   - ✅ **SHAP** pour une interprétation *locale* (explication précise d’un individu)
   - ✅ **LIME** pour visualiser les règles locales qui influencent chaque prédiction

---

## 🎯 Résultats principaux

- Le modèle XGBoost atteint un **R² de 0.88** et une **MAE de ~2459**, ce qui est performant pour un problème de régression sur données réelles.
- Les variables les plus importantes sont : `smoker`, `bmi`, `age`, et les interactions (`age_smoker`, `bmi_sex`).
- Des biais d’erreur ont été identifiés : les prédictions sont légèrement moins précises pour les hommes et les fumeurs.

---

## 🔎 Interprétabilité : SHAP & LIME

Nous avons mis l'accent sur l’explicabilité du modèle :

- **SHAP (SHapley Additive exPlanations)** fournit une interprétation fine et mathématiquement solide du modèle. Il permet de :
  - Visualiser l’influence moyenne de chaque variable (`summary_plot`)
  - Comprendre pourquoi un individu reçoit une certaine prédiction (`waterfall_plot`)

- **LIME (Local Interpretable Model-Agnostic Explanations)** explique les prédictions ponctuelles en simulant un modèle local simple autour d’une observation. Cela donne des règles lisibles comme :

  > "Le client n'est pas fumeur, a un IMC normal, et a entre 39 et 51 ans → donc ses frais estimés sont faibles."

Ces outils permettent à un acteur métier (ex. un assureur) de **comprendre, faire confiance et justifier** le modèle.

---

## 🧠 Conclusion

Ce projet montre non seulement comment construire un modèle prédictif performant pour estimer des coûts d’assurance santé, mais aussi comment l’**expliquer en toute transparence** grâce à SHAP et LIME.

L’interprétabilité est essentielle dans les secteurs réglementés comme l’assurance, où les décisions algorithmiques doivent être compréhensibles par les clients, les actuaires et les régulateurs.

📌 N'hésitez pas à explorer les visualisations SHAP et LIME ci-dessous pour comprendre *comment et pourquoi* chaque prédiction est faite.
