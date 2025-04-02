# Wireshark Docker 🕵️‍♂️

![Version](https://img.shields.io/github/v/release/tulia311/wireshark-docker)
![License](https://img.shields.io/github/license/tulia311/wireshark-docker)
![Docker Pulls](https://img.shields.io/docker/pulls/tulia311/wireshark)

![Interface Wireshark](https://miro.medium.com/v2/resize:fit:512/0*mMMUXeLUT7RWL8GB.png)

Un environnement Docker léger pour exécuter Wireshark avec prise en charge de SSH et du transfert X11.
Basé sur la dernière version stable de Debian slim, il permet une analyse efficace et sécurisée du trafic réseau avec une configuration minimale.

## ⚡ Démarrage rapide

```sh
# Cloner le dépôt
git clone https://github.com/tulia311/wireshark.git
cd wireshark-docker

# Construire l'image Docker
docker build -t tulia311/wireshark .

# Lancer le conteneur avec Docker Compose
docker-compose up -d
```

## ✨ Fonctionnalités
- Wireshark préconfiguré pour un usage sans privilèges root
- Serveur SSH sécurisé avec transfert X11 activé
- Création d'un utilisateur non-root pour plus de sécurité
- Prise en charge des applications GUI via SSH et X11
- Optimisé pour une faible consommation de ressources

## 📌 Prérequis

- Docker Engine 20.10+
- Serveur X11 installé sur la machine hôte
- Client SSH avec prise en charge du transfert X11
- Minimum 2 Go de RAM
- 1 Go d’espace disque

## ⚙️ Configuration

### Variables d'environnement

| Variable | Description | Valeur par défaut | Requis |
|----------|-------------|---------|---------|
| DISPLAY | Variable d'affichage X11 | Dépend de l'hôte | Oui |
| XDG_RUNTIME_DIR | Répertoire runtime X11 | /tmp/runtime-root | Non |
| QT_X11_NO_MITSHM | Empêche les problèmes de mémoire partagée X11 | 1 | Non |

### Exemple de configuration

```sh
docker run -d --name wireshark \
  -e DISPLAY=${DISPLAY} \
  -v /tmp/.X11-unix:/tmp/.X11-unix \
  -v ${HOME}/.Xauthority:/root/.Xauthority \
  --cap-add=NET_RAW \
  --cap-add=NET_ADMIN \
  tulia311/wireshark
```

## 📖 Utilisation

### Accès SSH
```sh
ssh -X wireshark@localhost -p 2222
```

### Lancement de Wireshark
```sh
wireshark
```
Si le transfert X11 est correctement configuré, l’interface graphique de Wireshark apparaîtra sur votre machine locale.

## 🔒 Bonnes pratiques de sécurité
- Restreindre l’accès SSH aux utilisateurs de confiance
- Limiter l’exposition réseau du conteneur
- Éviter d’exécuter des processus en tant que root

## 🔧 Maintenance

```sh
# Voir les logs
docker logs -f wireshark

# Redémarrer le conteneur
docker restart wireshark

# Mettre à jour l'image
docker pull tulia311/wireshark
docker stop wireshark
docker rm wireshark
# Relancer avec les mêmes paramètres
```

## 📚 Documentation

- [Documentation officielle de Wireshark](https://www.wireshark.org/docs/)
- [Documentation Docker](https://docs.docker.com)

## 📄 Licence

Ce projet est sous licence MIT - voir [LICENSE](https://raw.githubusercontent.com/tulia311/wireshark/refs/heads/main/LICENSE) pour plus de détails.

---
Développé avec ❤️ par [Tulia311](https://github.com/tulia311)

