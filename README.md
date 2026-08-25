# COnfiguration Serveur Connectiq
ce document récapitule le mise enplace et la sécurisation du serveur Ubuntu24.04 réalisée lors des Projets 2 et 
3
#projet 2: Gestion des Accès et Pincipe de Moindre privilège
##1 Matrice des Accès et Utilisateurs
**fifa**: Compte Administrateur( accès `sudo` complet).
* **stagiaire1** : Compte restreint avec privilèges `sudo` limitée uniquement à la gestion de service web(`/usr/bin/systemctl *nginx`).
* **stagiaire2 & stagiaire3** : Comptes utilisateurs standard sans privilèges d'administrations .

##2 Sécurisation des Permissions Fichier & Répertoires
* **`/etc/shadow/`**: Restreint en `600`( `rw-------`) - réservé exclusivement à `root`.
* **`/ets/passwd/`**: Défini en `644`( `rw-r--r--`) - lecture seule pour les utilisateurs non-root.
* **Dossiers personnels (`/home/stagiaireX`)** : Restreint en `700` (`rwx------`)pour empêcher le furetage inter-utilisateurs.

##3 Neutralisations des Comptes Systemes & Audit
* Désactivation des comptes systèmes inutiles (`games`, `news`).
* Vérification de l'absence du compte `gnats`.
* Audit initial des ports d'écoute via `sudo ss -tulpn`.



#projet 3: Pare-feu UFW et Sécurisation du serveur
##1 Configuration du pare-feu UFW
* Activation du pare-feu `UFW` avec politiquede filtrage restrictif (blocage de tout le trafic entrant par défaut ).
* Modification du port d'écoute SSH standard ( ** 22 **) vers le port sécurisé ** 2222/tcp ** .
* Authorisation des règles de flux entrants :
 * **SSH** : port `2222/tcp`
 * **HTTP**: port `80/tcp`
 * **HTTPS**: port `443/tcp`
* Installation et activation de `Fail2ban`.
* Activation et validation de la prison **`shhd`** pour surveiller et banir les tentatives répétées d'authentification frauduleuse.

## Vérification et Validation
* **Statut UFW**: `sudo ufw status verbose` (Règles 2222,80, 443, actives).
* **Statut Fail2ban**: `sudo fail2ban-client status sshd` (Jail `sshd`opérationnel).
* **Audit des sockets**: `sudo ss -tulpn` (Seuls les services légitimes sont en écoutes).

EOF

