# Prévision du rendement mensuel du S&P 500 avec un réseau LSTM

Application interactive **Streamlit** permettant d'estimer le rendement logarithmique du mois suivant de l'indice S&P 500 à partir de données financières mensuelles et d'un réseau de neurones récurrents **LSTM**.

> **Projet académique à visée pédagogique.** Les rendements boursiers sont difficiles à prévoir. Cette application ne constitue pas un conseil en investissement et ne doit pas être utilisée seule pour prendre des décisions financières.

## Objectif

Étudier l'apport du Deep Learning à la prévision des séries financières en construisant un modèle multivarié qui exploite les 12 derniers mois d'observations pour prévoir le rendement logarithmique du S&P 500 au mois suivant.

## Données

Le projet utilise des données mensuelles historiques de Robert Shiller (1881–2023), distribuées via [DataHub – S&P 500](https://datahub.io/core/s-and-p-500).

Les variables utilisées sont :

- **SP500** : niveau de l'indice S&P 500 ;
- **Earnings** : bénéfices ;
- **Consumer Price Index** : indice des prix à la consommation ;
- **Long Interest Rate** : taux d'intérêt à long terme ;
- **PE10** : ratio cours/bénéfices ajusté sur 10 ans.

Le fichier de données fourni dans le dépôt est `sp500_multivarie_propre_1881_2023.csv`.

## Méthodologie

1. **Préparation des données :** tri chronologique et construction de variables financières à partir des séries mensuelles.
2. **Transformation des variables :** rendement logarithmique du S&P 500, croissance logarithmique des bénéfices, variation logarithmique du CPI, variation du taux d'intérêt à long terme et logarithme du ratio PE10.
3. **Normalisation :** standardisation à l'aide des moyennes et écarts-types enregistrés dans `scaler.json`.
4. **Modélisation :** réseau LSTM multivarié avec une fenêtre temporelle de 12 mois, 32 unités et un dropout de 0,4.
5. **Prévision :** estimation du rendement logarithmique du mois suivant, puis conversion en rendement en pourcentage et en niveau indicatif de l'indice.
6. **Application :** interface Streamlit permettant de sélectionner le dernier mois connu, de modifier les 13 dernières observations et de consulter la prévision.

La configuration du modèle est enregistrée dans `config_finale.json` et le modèle entraîné dans `modele_lstm_final.keras`.

## Application

L'application permet de :

- sélectionner le dernier mois historique à utiliser ;
- consulter et modifier les valeurs des cinq variables sur les 13 derniers mois ;
- obtenir le rendement mensuel prévu et un niveau indicatif du S&P 500 ;
- visualiser l'évolution récente de l'indice ;
- comparer la prévision au rendement réellement observé lorsque le mois suivant est disponible et que les données n'ont pas été modifiées.

## Structure du dépôt

```
SP500/
├── app.py                                  # Application interactive Streamlit
├── requirements.txt                        # Dépendances Python
├── modele_lstm_final.keras                 # Modèle LSTM entraîné
├── config_finale.json                      # Configuration du modèle
├── scaler.json                             # Paramètres de normalisation
├── sp500_multivarie_propre_1881_2023.csv   # Données mensuelles
└── README.md                               # Documentation du projet
```

## Installation et lancement

Cloner le dépôt :

```bash
git clone https://github.com/rahhalfatimazahrae/SP500.git
cd SP500
```

Installer les dépendances :

```bash
pip install -r requirements.txt
```

Lancer l'application :

```bash
streamlit run app.py
```

L'application s'ouvrira dans le navigateur à l'adresse locale indiquée par Streamlit.

## Limites et précautions

- Les rendements financiers mensuels présentent du bruit et sont particulièrement difficiles à prévoir.
- Une prévision ponctuelle ne garantit pas une performance supérieure à une prévision de référence simple.
- Les résultats dépendent de la période d'entraînement, des transformations et du choix des variables.
- La comparaison avec une valeur réelle n'est affichée que lorsque le mois suivant est présent dans le jeu de données et que les observations n'ont pas été modifiées.
- Le dépôt contient le modèle entraîné et l'application de prédiction ; le notebook ou script complet ayant servi à l'entraînement n'est pas inclus dans la structure actuelle du dépôt.
- Cette application est un outil pédagogique, pas un système de trading ni un conseil financier.

## Auteur

**RAHHAL Fatima Zahrae**  
[GitHub](https://github.com/rahhalfatimazahrae) · [LinkedIn](https://www.linkedin.com/in/fatima-zahrae-rahhal/)
