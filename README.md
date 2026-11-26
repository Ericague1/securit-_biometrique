# securit-_biometrique
## Analyse et identification des besoins
1.1 Contexte du projet
L'ESTIM (École Supérieure de Technologie et de Management) a enregistré, en janvier 2026, 4 cas de vol de moto sur son campus. Face à cette insécurité, la présidente de l'assemblée des étudiants a lancé une compétition visant à concevoir un projet de sécurité des motos via un démarrage biométrique.

1.2 Identification des acteurs
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
