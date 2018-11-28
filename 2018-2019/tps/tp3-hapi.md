# TP3 : Hapi

<center>
![hapi](../../resources/hapi.jpg)
<br><br>
</center>

Hapi est un framework Node.JS développé par la société Wallmart et ayant comme philosophie que tout est plugin à l'intérieur des projets Hapi.

Hapi, tout comme ExpressJS ou Koa rajoute une surcouche au module Http pour permettre un meilleur découpage du code et une facilité de déclaration des différentes routes.

Avant de rentrer plus en détail avec un *boilerplate* tout prêt pour la suite des TP, vous avez, comme d'habitude, un tutoriel nodeschool pour bien comprendre son fonctionnement :

- Si vous n'avez pas eu le temps de le faire lors du TP1, je vous recommande vivement de faire `learnyounode` pour bien comprendre le fonctionnement de base de NodeJS et du module Http.
- `makemehapi`

## Hapipal

 Hapipal est un ecosystème hapi contenant plusieurs plugins qui facilitent certains chose sur Hapi. Nous allons en utiliser tout au long des TP's. Les plus courrants sont:

  - **haute-couture** : Permet de structurer notre projet hapi sous forme de dossiers. (https://github.com/hapipal/haute-couture)
  - **schwifty** : Pour les models de base de données intégrant  [`objection`](https://vincit.github.io/objection.js/). (https://github.com/hapipal/schwifty)
  - **schmervice** : Rajoute une couche permetant d'avoir des services afin de regrouper de la logique. (https://github.com/hapipal/schmervice)
  - **toys** : Un ensemble d'utilitaires pour simplifier pas mal de choses (https://github.com/hapipal/toys)

  Vous retrouverez aussi des tutoriels en anglais sur leur [site](https://hapipal.com/) et les autres libraries sur leur [github](https://github.com/hapipal)

## Boilerplate

Un boilerplate est un projet de base que vous prenez pour commencer un nouveau projet. Afin que tout le monde parte sur une base commune pour la suite des TP, vous devrez vous baser sur le boilerplate trouvable à cette adresse :

```
https://github.com/hapipal/boilerplate
```

Vous trouverez toute la documentation quand à son fonctionnement directement sur son repo git.

### Plugins

Vous trouverez de multiples plugins dans l'ecosystème hapi et hapipal, quelques-uns qui peuvent etre utiles sont:

- **Good** : Permet de logger facilement du contenu au sein du serveur en lieu et place du traditionnel `console.log` : https://github.com/hapijs/good
- **Blipp** : Affiche dans la console, lors du démarrage du serveur, les routes disponibles : https://github.com/danielb2/blipp
- **Boom** : Permet d'uniformiser les retours d'erreur aux requêtes : https://github.com/hapijs/boom
- **Boom decorators** : Permet d'utiliser facilement Hapi Boom dans le projet : https://github.com/brainsiq/hapi-boom-decorators
