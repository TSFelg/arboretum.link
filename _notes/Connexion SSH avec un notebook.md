---
title : Connexion SSH avec un notebook
tags : Réseau
etat : hiver
---

Utiliser un notebook jupyter déporté sur un serveur a pour avantage d'externaliser les calculs et d'éviter de trop surcharger sa machine, qui n'est pas forcément optimisée pour des charges lourdes en RAM ou en CPU.

Louer un serveur n'est pas gratuit et une concurrence féroce a lieu sur ce marché sur le marché des "petits" VPS. il semble que deux stratégies émergent :

- Proposer des prix les plus faibles possibles à l'entrée comme produit d'appel en espérant que le consommateur ne voudra pas faire l'effort de changer ensuite, et augmentera sa demande au fur et à mesure qu'il utilise le service. Les sites comme [lowendbox.com](https://lowendbox.com/) sont représentatifs de cette stratégie "discount". Je suppose que les consommateurs visés sont dans ce cas les utilisateurs avertis, hobbyistes ou web-devs voulant économiser au maximum.

- Proposer un accompagnement, une interface peaufinée et des tutoriels avancés, avec un prix plus élevé. [Digital Ocean](https://www.digitalocean.com/) est un bon exemple : on a accès à une interface ne rebuttant pas les débutants et propose de nombreux guides sur la mise en place d'un serveur. On a même à présent des installations en un clic qui évitent (plus ou moins...) à l'utilisateur de devoir se connecter en SSH. Ils ont dû, à mon avis, identifier cela comme un goulot d'étranglement significatif de la demande peu qualifiée, qui a une meilleure propension à payer. On peut qualifier cette offre de "premium", les tarifs étant au minimum deux fois plus élevés. Entre [Contabo](https://contabo.com/?show=vps) et [Linode](https://www.linode.com/products/shared/), le ratio de prix est de 10 (8\$ Contabo / 80\$ Linode) pour une instance ayant 16gb de RAM. 

Contabo race maîtresse ? Ils bradent la RAM et les perfomances CPU sont acceptables. Par contre, l'interface de gestion date des années 2000 et les options sont considérablement limitées.

On pourrait citer les nouveaux entrants comme [Deepnote](https://deepnote.com), [Google Colab](https://colab.research.google.com/) ou [Datalore](https://datalore.jetbrains.com/), récents sur le marché et vendant une machine associée à un notebook jupyter. Ces solutions ne sont, à mon sens, pas encore matures pour des usages avancés nécéssitant une grande flexibilité et restent assez coûteuses pour l'utilisateur. Par ailleurs, je suppose que ces acteurs tenteront de développer des API spécifiques à leur service[^1] qui restreindront les possibilités de changement et augmentera leur pouvoir de marché.

[^1]: Tout comme Obsidian a développé un dialecte Markown qui lui est propre

Pour mettre en place un serveur, voir mon repo sur [Github](https://github.com/Maxence-L/debian-datascience-setup). Bref, voici comment se connecter en SSH, en cas d'oubli :

On commence par se connecter à la machine distance en CLI :

```bash
ssh username@ip
````

Une fois connecté ont démarre le notebook (ici jupyterLab) et on lui donne le port sur lequel envoyer les données :

```bash
jupyter lab --no-browser --port=8080
````

On peut à présent ouvrir un nouveau tunnel SSH sur notre machine locale et lui dire de passer les informations du port 8080 de la machine distante sur le port équivalent de notre machine locale :

```bash
ssh -N -L 8080:localhost:8080 <remote_user>@<remote_host>
````

On peut à présent visiter [localhost:8080](http://localhost:8080/) et admirer le notebook ouvert.