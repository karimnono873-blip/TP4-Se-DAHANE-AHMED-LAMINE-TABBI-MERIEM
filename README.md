# 🌌 TP 4 : Timers & Génération de signaux PWM - Systèmes Embarqués

Bienvenue dans le dépôt du **Travail Pratique N°4**. L'objectif de cette session est de dépasser les limitations des temporisations logicielles (`HAL_Delay`) en exploitant les périphériques matériels **Timers** du microcontrôleur **STM32 Nucleo-C031C6** pour générer un signal **PWM (Pulse Width Modulation)**.

Ce projet se démarque par la création d'un **Rapport de Laboratoire Interactif Web (HTML/CSS/JS)** qui intègre un véritable **Oscilloscope Virtuel** pour visualiser la modulation du signal en temps réel.

## 🚀 Fonctionnalités du Jumeau Numérique (Web)

Le fichier `compte_rendu_tp4.html` est une application web autonome au design "Deep Space" qui comprend :
* **Un Oscilloscope Virtuel Dynamique :** Un composant `<canvas>` trace instantanément le signal carré généré. La largeur des impulsions (Ton) s'adapte en temps réel aux manipulations du curseur.
* **Simulation d'une LED Dimmable :** L'intensité lumineuse (calculée via l'opacité et un effet de lueur CSS) varie proportionnellement au rapport cyclique (Duty Cycle).
* **Code Source Intégré :** Visualisation de la boucle C gérant la modification dynamique du registre de comparaison via la macro `__HAL_TIM_SET_COMPARE()`.
* **Analyse d'Ingénierie (Post-Lab) :** Explications détaillées sur les principes de la PWM et les calculs critiques de fréquence (détermination du `Prescaler` et de l'`Auto-Reload Register` pour cibler 1kHz sur un processeur à 48MHz).

## 📋 Concept Réalisé (Code C & Simulation)

**Génération PWM sur Timer 3 (Canal 2) :**
* **Hardware :** Configuration du `TIM3` pour générer un signal PWM directement routé vers la broche `PA5` (LED) via sa fonction alternative (Alternate Function).
* **Calculs (Fréquence 1 kHz) :** Avec une horloge système à 48 MHz, le `Prescaler` est fixé à 47 et l'`ARR` à 999. Cela permet d'obtenir une résolution de 1000 pas pour un contrôle ultra-précis de la luminosité (0.0% à 100.0%).
* **Performance :** Une fois la génération démarrée par la commande matérielle `HAL_TIM_PWM_Start()`, la PWM est maintenue par le hardware. Le processeur est libéré à 100% de la gestion de la LED.

## 🛠️ Matériel & Outils Requis

* **Carte :** STM32 Nucleo-C031C6 (Matériel physique ou simulation via [Wokwi](https://wokwi.com/stm32)).
* **Composants :** LED intégrée ou externe sur PA5, Oscilloscope (optionnel pour vérifier le signal physique).
* **Environnement C :** STM32CubeIDE (Génération de code via CubeMX).
* **Environnement Web :** Navigateur web moderne pour lancer le rapport interactif et l'oscilloscope.

## ⚙️ Instructions d'Exécution

### 1. Visualiser le Jumeau Numérique (Web)
Double-cliquez sur le fichier `compte_rendu_tp4.html`. Ajustez le curseur du "Rapport Cyclique" pour observer la variation de l'intensité de la LED et la forme du signal correspondant sur l'oscilloscope.

### 2. Exécuter le Code C (STM32 / Wokwi)
1. Importez la configuration dans STM32CubeIDE ou créez un projet Wokwi.
2. Assurez-vous que le composant **TIM3** est activé avec le Canal 2 en mode **PWM Generation CH2**.
3. Définissez le Prescaler à `47` et la Counter Period (ARR) à `999`.
4. Compilez, flashez le code et observez l'effet visuel de "respiration" (Fading) automatique sur la LED branchée en `PA5`.

## 👥 Équipe du Projet

**Année Universitaire :** 2025/2026
* **Binôme :** Dahane Ahmed Lamine & Tabbi Meriem
* **Enseignante Responsable :** Mme. Afaf Saoud
