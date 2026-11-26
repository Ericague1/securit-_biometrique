 # 🔐 Système de sécurisation des motos par démarrage biométrique

## 1.1 Contexte du projet
L'*UNSTIM* a enregistré, en janvier 2026, 4 cas de vol de moto sur son campus. Face à cette insécurité, la présidente de l'assemblée des étudiants a lancé une compétition visant à concevoir un projet de sécurité des motos via un démarrage biométrique.

## Analyse et identification des besoins
##   Identification des acteurs
Acteur	Rôle
Étudiant / Propriétaire de moto	Utilisateur principal ; enregistre son empreinte, démarre sa moto
Présidente de l'assemblée des étudiants	Initiatrice du projet et de la compétition ; valide les projets
Administrateur du système	Gère les comptes, les empreintes et les paramètres
Système biométrique (capteur)	Acteur système ; capture et vérifie l'empreinte
Agent de sécurité	Consulte les journaux de démarrage en cas d'incident
1.3 Identification des besoins fonctionnels (BF)
Code	Besoin fonctionnel
BF1	Le système doit permettre à un étudiant de s'enregistrer (profil + moto)
BF2	Le système doit permettre l'enregistrement de l'empreinte digitale du propriétaire
BF3	Le système doit capturer l'empreinte au moment du démarrage
BF4	Le système doit comparer l'empreinte capturée à l'empreinte de référence
BF5	Le système doit autoriser ou refuser le démarrage du moteur
BF6	Le système doit journaliser chaque tentative de démarrage (date, heure, résultat)
BF7	Le système doit permettre à un administrateur de gérer les utilisateurs et les empreintes
BF8	Le système doit gérer la compétition (inscription des projets, évaluation, classement)
BF9	Le système doit alerter en cas de tentatives répétées échouées (tentative de vol)

## 1.4 Identification des besoins non fonctionnels (BNF)
### Code	Besoin non fonctionnel

BNF1	Sécurité : les empreintes doivent être chiffrées et stockées de façon sécurisée
BNF2	Performance : la vérification biométrique doit prendre moins de 2 secondes
BNF3	Fiabilité : taux de reconnaissance supérieur à 99 %
BNF4	Disponibilité : le système doit fonctionner 24h/24
BNF5	Ergonomie : utilisation simple et rapide pour l'étudiant
BNF6	Traçabilité : conserver l'historique des démarrages pendant au moins 12 mois
BNF7	Portabilité : le système doit s'adapter à différents modèles de motos









##  🔧 Le cœur du dispositif embarqué sur la moto

Cette partie regroupe les composants électroniques essentiels au fonctionnement du système. Ils permettent d'identifier l'utilisateur, de vérifier son identité et d'autoriser ou de bloquer le démarrage de la moto.

| **Composant** | **Rôle concret dans le projet** | **Pourquoi est-il indispensable ?** |
|---|---|---|
| **Capteur d'empreinte digitale** (ex. R305/R307) | Capture l'empreinte du doigt de l'étudiant et la convertit en données numériques. | C'est le point d'entrée de l'authentification. Sans lui, le système ne peut pas savoir qui tente de démarrer la moto. |
| **Microcontrôleur** (ex. Arduino Uno/Nano) | Constitue le cerveau du système : il reçoit les données du capteur, les compare aux empreintes enregistrées, puis décide d'autoriser ou non le démarrage. | Il assure la logique de décision et fait le lien entre la biométrie et l'action mécanique. |
| **Module relais** | Agit comme un interrupteur électronique commandé par le microcontrôleur. Il commande le circuit d'autorisation du démarrage. | C'est l'actionneur physique qui permet d'exécuter la décision du système. |
| **Régulateur de tension** (ou convertisseur DC-DC) | Abaisse la tension de la batterie 12 V de la moto vers une tension stable de 5 V pour alimenter l'Arduino et le capteur. | Il protège les composants électroniques contre les variations de tension du système électrique de la moto. |
| **Buzzer / LED d'état** | Émet un signal sonore ou lumineux pour indiquer si l'accès est autorisé (vert) ou refusé (rouge). | Offre un retour immédiat à l'utilisateur. Le buzzer peut également signaler une tentative suspecte. |



## 2. 📡 Composants optionnels mais très pertinents pour le contexte UNSTIM

Ces composants ne sont pas obligatoires pour réaliser une première version fonctionnelle du dispositif. Cependant, ils apportent des fonctionnalités supplémentaires particulièrement intéressantes dans le cadre de la lutte contre le vol de motos.

| **Composant** | **Rôle concret** | **Pourquoi est-ce utile ici ?** |
|---|---|---|
| **Module GSM** (ex. SIM800L) | Envoie un SMS au propriétaire ou à l'administrateur en cas de tentative de démarrage non autorisée. | Le projet vise à lutter contre le vol. Le propriétaire peut ainsi être alerté à distance, même lorsqu'il n'est pas à proximité de sa moto. |
| **Écran LCD** (16x2 ou OLED) | Affiche des messages simples : « Accès autorisé », « Empreinte refusée », « Système prêt ». | Facilite l'utilisation du dispositif sur le terrain et le débogage pendant la phase de test. Il améliore également l'ergonomie du système. |



## 3. 💻 Côté gestion : administration et supervision

Au-delà du dispositif électronique installé sur la moto, le projet nécessite une solution de gestion permettant de centraliser les informations et de contrôler les accès.

| **Composant** | **Rôle concret** | **Pourquoi est-il nécessaire ?** |
|---|---|---|
| **Ordinateur / Serveur local** | Stocke la base de données des étudiants, des motos et des empreintes de référence. Permet d'enregistrer les nouveaux utilisateurs et de consulter l'historique des démarrages. | Le projet inclut une dimension administrative. Il faut donc un espace centralisé pour gérer les inscriptions et vérifier les autorisations. |
| **Logiciel / Application de gestion** | Propose une interface permettant à l'administrateur d'ajouter ou de supprimer un étudiant, d'enregistrer une empreinte et de consulter les journaux d'activité (*logs*). | Sans interface, la gestion des utilisateurs serait manuelle et peu fiable. Cette application rend le système plus pratique et exploitable à l'échelle de l'ESTIM. |



## 4. ⚙️ Principe général de fonctionnement

Le système fonctionne suivant une succession d'étapes :

1. **Identification :** l'étudiant pose son doigt sur le capteur biométrique.
2. **Capture :** le capteur relève l'empreinte digitale et transmet les données au microcontrôleur.
3. **Vérification :** le microcontrôleur compare l'empreinte capturée aux empreintes enregistrées.
4. **Prise de décision :**
   - Si l'empreinte est reconnue, le système autorise le démarrage.
   - Si l'empreinte n'est pas reconnue, le démarrage reste bloqué.
5. **Signalisation :** la LED, le buzzer ou l'écran informe l'utilisateur du résultat.
6. **Alerte éventuelle :** en cas de tentative suspecte, le module GSM peut envoyer une notification au propriétaire ou à l'administrateur.
7. **Enregistrement :** la tentative est enregistrée dans l'historique pour permettre un suivi administratif.



## 5. 📋 Synthèse des composants

| **Catégorie** | **Composants** |
|---|---|
| Dispositif embarqué indispensable | Capteur d'empreinte, microcontrôleur, module relais, régulateur de tension, buzzer et LED |
| Composants optionnels | Module GSM, écran LCD ou OLED |
| Gestion et administration | Ordinateur ou serveur local, logiciel ou application de gestion |

> **Remarque :** Les composants optionnels peuvent être intégrés progressivement selon le budget et les objectifs de la compétition. Le montage électrique réel devra être conçu et testé avec des protections adaptées, notamment pour isoler les circuits électroniques de la moto et éviter toute intervention dangereuse sur son système d'allumage.
