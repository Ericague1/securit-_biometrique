 # 🔐 Système de sécurisation des motos par démarrage biométrique

## Contexte du projet
L'*UNSTIM* a enregistré, en janvier 2026, 4 cas de vol de moto sur son campus. Face à cette insécurité, la présidente de l'assemblée des étudiants a lancé une compétition visant à concevoir un projet de sécurité des motos via un démarrage biométrique.

## Analyse et identification des besoins
###   Identification des acteurs
#### 1. Identification des acteurs du système

Les acteurs représentent les différentes entités qui interagissent directement ou indirectement avec le système de sécurisation des motos par démarrage biométrique.

| **Acteur** | **Rôle** |
|---|---|
| **Étudiant / Propriétaire de moto** | Utilisateur principal du système. Il enregistre son empreinte digitale et utilise celle-ci pour démarrer sa moto. |
| **Présidente de l'assemblée des étudiants** | Initiatrice du projet et de la compétition. Elle valide les projets proposés. |
| **Administrateur du système** | Assure la gestion des comptes utilisateurs, des empreintes digitales et des paramètres du système. |
| **Système biométrique (capteur)** | Capture et vérifie les empreintes digitales présentées lors d'une tentative de démarrage. |
| **Agent de sécurité** | Consulte les journaux de démarrage afin de vérifier les activités et d'intervenir en cas d'incident. |



#### 1.2 Identification des besoins fonctionnels (BF)

Les besoins fonctionnels décrivent les différentes opérations que le système doit être capable d'effectuer pour répondre aux attentes des utilisateurs et assurer la sécurité des motos.

| **Code** | **Besoin fonctionnel** |
|---|---|
| **BF1** | Le système doit permettre à un étudiant de s'enregistrer en renseignant son profil et les informations relatives à sa moto. |
| **BF2** | Le système doit permettre l'enregistrement de l'empreinte digitale du propriétaire de la moto. |
| **BF3** | Le système doit capturer l'empreinte digitale au moment où l'utilisateur tente de démarrer la moto. |
| **BF4** | Le système doit comparer l'empreinte capturée à l'empreinte de référence enregistrée dans sa base de données. |
| **BF5** | Le système doit autoriser ou refuser le démarrage du moteur en fonction du résultat de l'authentification biométrique. |
| **BF6** | Le système doit enregistrer chaque tentative de démarrage en précisant la date, l'heure et le résultat de l'opération. |
| **BF7** | Le système doit permettre à un administrateur de gérer les utilisateurs et leurs empreintes digitales. |
| **BF8** | Le système doit déclencher une alerte en cas de tentatives répétées de démarrage échouées, pouvant indiquer une tentative de vol. |

---

### 📌 Synthèse

L'identification des acteurs permet de déterminer les personnes et les entités qui interagissent avec le système. Quant aux besoins fonctionnels, ils définissent les services que le dispositif doit fournir.

Ces deux éléments constituent une base essentielle pour la réalisation des diagrammes UML, notamment :

- Le diagramme de cas d'utilisation ;
- Le diagramme de séquence ;
- Le diagramme de classes ;
- Le diagramme d'activités ;
- Le diagramme de composants.

## 1.3 Identification des besoins non fonctionnels (BNF)
### Code	Besoin non fonctionnel


Les besoins non fonctionnels définissent les critères de qualité, de performance et de sécurité que le système doit respecter pour garantir son bon fonctionnement et offrir une expérience satisfaisante aux utilisateurs.

| **Code** | **Besoin non fonctionnel** | **Description** |
|---|---|---|
| **BNF1** | **Sécurité** | Les empreintes digitales doivent être chiffrées et stockées de manière sécurisée afin de protéger les données biométriques des utilisateurs. |
| **BNF2** | **Performance** | La vérification biométrique doit être effectuée en moins de 2 secondes. |
| **BNF3** | **Fiabilité** | Le système doit atteindre un taux de reconnaissance supérieur à 99 %. |
| **BNF4** | **Disponibilité** | Le système doit être opérationnel 24 heures sur 24 afin de permettre aux étudiants de démarrer leur moto à tout moment. |
| **BNF5** | **Ergonomie** | Le système doit être simple, intuitif et rapide à utiliser pour l'étudiant. |
| **BNF6** | **Traçabilité** | Le système doit conserver l'historique des démarrages pendant une durée minimale de 12 mois. |
| **BNF7** | **Portabilité** | Le système doit pouvoir être adapté à différents modèles de motos. |



### 📌 Synthèse

Les besoins non fonctionnels définissent les exigences de qualité auxquelles le système doit répondre. Ils permettent de garantir :

- **La sécurité** des données biométriques ;
- **La rapidité** de l'authentification ;
- **La fiabilité** de la reconnaissance des empreintes ;
- **La disponibilité** permanente du dispositif ;
- **La simplicité** d'utilisation ;
- **La traçabilité** des tentatives de démarrage ;
- **L'adaptabilité** à différents modèles de motos.

Ces exigences serviront de critères de référence lors de la conception, du développement et des tests du système de sécurisation des motos par démarrage biométrique.









##  🔧 Le cœur du dispositif embarqué sur la moto

Cette partie regroupe les composants électroniques essentiels au fonctionnement du système. Ils permettent d'identifier l'utilisateur, de vérifier son identité et d'autoriser ou de bloquer le démarrage de la moto.

| **Composant** | **Rôle concret dans le projet** | **Pourquoi est-il indispensable ?** |
|---|---|---|
| **Capteur d'empreinte digitale** (ex. R305/R307) | Capture l'empreinte du doigt de l'étudiant et la convertit en données numériques. | C'est le point d'entrée de l'authentification. Sans lui, le système ne peut pas savoir qui tente de démarrer la moto. |
| **Microcontrôleur** (ex. Arduino Uno/Nano) | Constitue le cerveau du système : il reçoit les données du capteur, les compare aux empreintes enregistrées, puis décide d'autoriser ou non le démarrage. | Il assure la logique de décision et fait le lien entre la biométrie et l'action mécanique. |
| **Module relais** | Agit comme un interrupteur électronique commandé par le microcontrôleur. Il commande le circuit d'autorisation du démarrage. | C'est l'actionneur physique qui permet d'exécuter la décision du système. |
| **Régulateur de tension** (ou convertisseur DC-DC) | Abaisse la tension de la batterie 12 V de la moto vers une tension stable de 5 V pour alimenter l'Arduino et le capteur. | Il protège les composants électroniques contre les variations de tension du système électrique de la moto. |
| **Buzzer / LED d'état** | Émet un signal sonore ou lumineux pour indiquer si l'accès est autorisé (vert) ou refusé (rouge). | Offre un retour immédiat à l'utilisateur. Le buzzer peut également signaler une tentative suspecte. |



##  📡 Composants optionnels mais très pertinents pour le contexte UNSTIM

Ces composants ne sont pas obligatoires pour réaliser une première version fonctionnelle du dispositif. Cependant, ils apportent des fonctionnalités supplémentaires particulièrement intéressantes dans le cadre de la lutte contre le vol de motos.

| **Composant** | **Rôle concret** | **Pourquoi est-ce utile ici ?** |
|---|---|---|
| **Module GSM** (ex. SIM800L) | Envoie un SMS au propriétaire ou à l'administrateur en cas de tentative de démarrage non autorisée. | Le projet vise à lutter contre le vol. Le propriétaire peut ainsi être alerté à distance, même lorsqu'il n'est pas à proximité de sa moto. |
| **Écran LCD** (16x2 ou OLED) | Affiche des messages simples : « Accès autorisé », « Empreinte refusée », « Système prêt ». | Facilite l'utilisation du dispositif sur le terrain et le débogage pendant la phase de test. Il améliore également l'ergonomie du système. |



## . 💻 Côté gestion : administration et supervision

Au-delà du dispositif électronique installé sur la moto, le projet nécessite une solution de gestion permettant de centraliser les informations et de contrôler les accès.

| **Composant** | **Rôle concret** | **Pourquoi est-il nécessaire ?** |
|---|---|---|
| **Ordinateur / Serveur local** | Stocke la base de données des étudiants, des motos et des empreintes de référence. Permet d'enregistrer les nouveaux utilisateurs et de consulter l'historique des démarrages. | Le projet inclut une dimension administrative. Il faut donc un espace centralisé pour gérer les inscriptions et vérifier les autorisations. |
| **Logiciel / Application de gestion** | Propose une interface permettant à l'administrateur d'ajouter ou de supprimer un étudiant, d'enregistrer une empreinte et de consulter les journaux d'activité (*logs*). | Sans interface, la gestion des utilisateurs serait manuelle et peu fiable. Cette application rend le système plus pratique et exploitable à l'échelle de l'UNSTIM. |



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

**Remarque :** Les composants optionnels peuvent être intégrés progressivement selon le budget et les objectifs de la compétition. Le montage électrique réel devra être conçu et testé avec des protections adaptées, notamment pour isoler les circuits électroniques de la moto et éviter toute intervention dangereuse sur son système d'allumage.


# 🔐 Scénario complet du projet de démarrage biométrique

Ce document présente le fonctionnement global du système de sécurisation des motos par démarrage biométrique, depuis son installation jusqu'à sa maintenance.

Le scénario est organisé en six phases. Chaque phase décrit deux aspects complémentaires :

- **En avant :** les actions visibles réalisées par les utilisateurs.
- **En arrière :** les opérations techniques exécutées automatiquement par le système.



## ⚙️ PHASE 0 — Installation et préparation du système

### 👤 En avant : actions de l'administrateur

1. L'administrateur installe sur la moto les composants électroniques suivants :
   - Capteur d'empreinte digitale ;
   - Microcontrôleur ;
   - Module relais ;
   - Régulateur de tension ;
   - Buzzer et LED ;
   - Module GSM (optionnel).
2. Il procède au raccordement du dispositif au circuit d'autorisation du démarrage, conformément aux spécifications électriques de la moto.
3. Il alimente le système à partir de la batterie de 12 V de la moto, avec un régulateur permettant d'obtenir une alimentation stable de 5 V pour les composants électroniques.

### 💻 En arrière : fonctionnement interne

- Le régulateur **stabilise la tension** afin de protéger l'Arduino et le capteur biométrique.
- Le microcontrôleur **initialise ses périphériques** et vérifie leur disponibilité.
- Le relais est **maintenu ouvert par défaut** : aucun démarrage n'est autorisé sans authentification.
- Le système passe en **état d'attente** et affiche le message : « Système prêt ».



## 📝 PHASE 1 — Enrôlement de l'étudiant et de son empreinte

### 👤 En avant : actions de l'étudiant et de l'administrateur

1. L'étudiant se présente auprès de l'administrateur avec sa moto et sa carte d'étudiant.
2. L'administrateur crée le **profil de l'étudiant** en renseignant les informations suivantes :
   - Nom ;
   - Prénom ;
   - Filière ;
   - Numéro d'immatriculation de la moto.
3. L'étudiant pose son doigt sur le capteur biométrique deux à trois fois afin de permettre l'enregistrement de son empreinte de référence.
4. Le système affiche un message de confirmation : **« Empreinte enregistrée avec succès »**.

### 💻 En arrière : fonctionnement interne

- Le capteur **capture l'image de l'empreinte** et la convertit en un modèle numérique appelé *template*.
- Le template est **protégé par un mécanisme de chiffrement** avant son stockage.
- L'empreinte enregistrée est **associée à l'identifiant de la moto** autorisée.
- Un **journal d'enrôlement** est créé avec les informations suivantes :
  - Date ;
  - Heure ;
  - Identité de l'opérateur responsable de l'enregistrement.

> ⚠️ **Exigence de sécurité :** l'image brute de l'empreinte ne doit pas être conservée. Seul le modèle biométrique de référence, protégé de manière appropriée, doit être stocké.



## 🟢 PHASE 2 — Démarrage normal (scénario nominal)

Cette phase décrit le fonctionnement du système lorsqu'un étudiant autorisé tente de démarrer sa moto.

### 👤 En avant : actions de l'étudiant

1. L'étudiant pose son doigt sur le capteur biométrique.
2. La LED **orange** s'allume pour indiquer : « Vérification en cours… ».
3. En moins de deux secondes, si l'empreinte est reconnue, la LED **verte** s'allume et affiche : « Accès autorisé ».
4. L'étudiant utilise la commande


