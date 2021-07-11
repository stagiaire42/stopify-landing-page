# landing-page
## Présentation
Le mini site de l'entreprise contient 2 pages :
- la page d'acceuil
- la page de contact

Le site est généré par le framework [hugo](https://gohugo.io/) et le thème utilisé est [bigspring](https://themes.gohugo.io/bigspring-hugo-startup-theme/).
Les sources du site sont présentes dans le dossier nommé `website`.

## Procédures
### Faire tourner le site en local (préproduction)
La génération du site peut être simulée en local grâce à une image docker et à docker-compose.

Un service nommé `dev_server` est défini dans le fichier docker-compose.yml.
- Le stage de build du service crée une image docker dont le `Dockerfile` et les scripts associés se trouvent dans le dossier `docker-image`.
- Lorsque le service est lancé la commande exécutée par le container est `hugo server --bind-"0.0.0.0"` avec un mapping du dossier `website` sur le volume `/src` du container et avec un mapping du port 1313 du container sur le port 1313 de la machine qui fait tourner docker. Cette commande permet de lancer hugo en mode serveur afin de voir en live toutes les modifications apportées au site en ouvrant l'URL http://localhost:1313.

### Comment (re)build l'image de l'environnement de dev
`docker-compose build`

### Comment lancer l'environnement de dev
`docker-compose up` ou `docker-compose up -d` pour passer en mode daemon

### Comment stopper l'environnement de dev
CTRL+C ou `docker-compose down`

### Changer la version d'hugo installée dans l'image Docker
Changer la version dans le script `docker-image/_script/hugo.sh` via la variable `HUGO_VERSION`.  
Il faut ensuite reconstruire l'image.