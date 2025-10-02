# Nextcloud

Mon cloud qui contiendra mes fichiers.

## Installation

```shell
cp .env-example .env
```

```shell
cp Caddyfile.example Caddyfile
```

Dans le fichier alimenter les infos afin de faire fonctionner NextCloud.

```shell
docker compose up -d
```

## Configurations complémentaires

### Trusted Domain
```shell
sudo docker exec -u www-data -it nextcloud php occ config:system:set trusted_domains 1 --value=nextcloudsama.devpapangue.com
```

### Trusted Proxies
```shell
docker network ls
# Et trouver le nom du réseau de nextcloud
sudo docker network inspect [nom_du_reseau] | grep Subnet
# Et ajouter le résultat dans le fichier .env "TRUSTED_PROXIES"
```

### Index manquants
```shell
# A copier/coller sans réfléchir
docker exec -u www-data nextcloud php occ db:add-missing-indices
```

### Activer la maintenance
```shell
sudo docker exec -u www-data -it nextcloud php occ config:system:set maintenance_window_start --type=integer --value=1
```

### Envoie d'email (à debugger)
