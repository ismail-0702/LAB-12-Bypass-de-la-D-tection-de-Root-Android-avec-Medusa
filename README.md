# LAB-12-Bypass-de-la-D-tection-de-Root-Android-avec-Medusa
1. Présentation
Ce laboratoire a pour but d'analyser les mécanismes de détection de root intégrés dans une application Android, puis de les contourner dans un environnement contrôlé grâce aux outils d'instrumentation dynamique.
L'application cible est OWASP UnCrackable Level 2, une application Android intentionnellement vulnérable, conçue à des fins pédagogiques dans le domaine de la sécurité mobile et du reverse engineering.
Deux approches ont été mises en œuvre :

Bypass manuel via Frida.
Bypass automatisé / semi-automatisé via Medusa.

L'objectif est de démontrer qu'une protection purement côté client — telle que la détection de root — peut être contournée à l'exécution si elle n'est pas appuyée par des mécanismes de sécurité plus robustes côté serveur ou au niveau applicatif.

2. Objectifs du laboratoire

Installer et configurer Frida sur le PC et sur l'émulateur Android.
Vérifier la communication entre le PC et l'émulateur via ADB.
Lancer une application Android protégée contre les environnements rootés.
Observer le comportement de l'application avant toute intervention.
Utiliser Frida pour intercepter des appels Java sensibles.
Bloquer les fonctions responsables de la fermeture de l'application.
Masquer les fichiers et indicateurs associés au root.
Contourner la vérification du code secret.
Exploiter Medusa comme couche d'automatisation basée sur Frida.
Documenter l'ensemble du processus avec des captures d'écran.


3. Environnement de travail
ÉlémentDétailsSystème hôteWindowsTerminalPowerShellAppareil AndroidÉmulateur AndroidIdentifiant de l'émulateuremulator-5554Application cibleOWASP UnCrackable Level 2Package Androidowasp.mstg.uncrackable2Outil principalFridaOutil complémentaireMedusaType d'analyseAnalyse dynamiqueNiveauSécurité mobile / Reverse engineering Android

4. Application cible
OWASP UnCrackable Level 2
Application volontairement vulnérable issue du projet OWASP Mobile Security Testing Guide (MSTG), utilisée ici comme terrain d'entraînement pour le contournement des protections root.

5. Réalisation
Étape 1 — Connexion de l'émulateur Android via ADB
<img width="775" height="85" alt="Connexion ADB" src="https://github.com/user-attachments/assets/ccc88142-b46f-4ff7-93c2-da2ab6e58a88" />

Confirmation que l'émulateur Android est correctement connecté au PC d'Ismail via ADB.


Étape 2 — Détection de l'application par Frida
<img width="1208" height="736" alt="Détection Frida" src="https://github.com/user-attachments/assets/8366a68d-c02c-40dd-bdbc-1ed86d8d3210" />

Frida identifie l'émulateur ainsi que l'application UnCrackable Level 2 depuis le poste d'Ismail.


Étape 3 — Exécution du script Frida avec chargement des hooks
<img width="1410" height="649" alt="Exécution script Frida" src="https://github.com/user-attachments/assets/07f90dc1-f647-4da0-8707-19ab34f67524" />

Le script Frida est lancé et les hooks sont chargés avec succès dans l'environnement d'Ismail.


Étape 4 — Résultat du bypass (Frida)
<img width="384" height="835" alt="Bypass réussi" src="https://github.com/user-attachments/assets/a849dded-8742-4aff-97c2-c2f52b00d206" />

L'application ne se ferme plus après détection de root : le bypass est opérationnel.


Étape 5 — Lancement de Medusa et sélection de l'émulateur
<img width="1432" height="612" alt="Lancement Medusa" src="https://github.com/user-attachments/assets/4236371c-4a78-462c-8513-d2b0123bc5dd" />

Ismail lance Medusa et sélectionne l'émulateur Android comme cible.


Étape 6 — Intégration du script Frida dans Medusa (agent.js)
<img width="1035" height="850" alt="Agent.js dans Medusa" src="https://github.com/user-attachments/assets/2413dab6-cbbe-4e45-8508-65a606c047ac" />

Le script Frida personnalisé est utilisé comme fichier agent.js directement dans Medusa.


Étape 7 — Exploration des modules disponibles dans Medusa
<img width="802" height="265" alt="Modules Medusa" src="https://github.com/user-attachments/assets/3745ba8e-89fc-4fe5-b94a-4402a00a78b0" />

Vue des modules disponibles dans Medusa lors de la session d'Ismail.


Étape 8 — Bypass final via Medusa
<img width="384" height="835" alt="Bypass final Medusa" src="https://github.com/user-attachments/assets/a849dded-8742-4aff-97c2-c2f52b00d206" />

L'application est lancée avec succès via Medusa, bypass appliqué : le root n'est plus détecté.

