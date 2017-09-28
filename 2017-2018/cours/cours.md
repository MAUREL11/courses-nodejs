<!-- $theme: gaia -->

# Node.JS

---
# Sommaire

1. Qu'est-ce que Node.JS
2. Utilisations
3. Gestionnaire de paquet et package.json
4. EventLoop
5. Versions de Node.JS
6. Plan de travail

---
# Qu'est-ce que Node.JS

- Javascript côté server
- Moteur V8 de Webkit
- Open Source
- Multiplateforme (ou presque)
- Mono thread
- Asynchrone
- I/O non bloqués

---
# Qu'est-ce que Node.js

- Versions standards et LTS
	![version](https://github.com/nodejs/LTS/raw/master/schedule.png)
    
---
# Qu'est-ce que Node.JS

- serveur http

```javascript
var http = require('http');

http.createServer(function (req, res) {
    res.writeHead(200, {'Content-Type': 'text/html'});
    res.end('Hello World!');
}).listen(8080);
```

---
Utilisation

- scripts bash
- compilations diverses (babel, ...)
- applications multiplateformes desktop (electron, NW)
- applications mobiles (react-native, ionic, native-script)
- serveurs web (express, hapi, koa)
- serverless (chromeless, ...)
- ...

---
# Gestionnaire de paquets

- NPM
	- officiel
	- npmjs.org

```
npm install -S hapi
```

- Yarn
	- facebook
	- plus rapide

```
yarn add hapi
```
---
# Gestionnaire de paquets

- NPX
	- Permet de lancer des binaires installés via npm
	- Peu importe s'ils sont au sein du projet ou global

```
./node_modules/.bin/eslint
/usr/bin/eslint

npx eslint
```

---
# Package.json

- coeur de l'application
- paquets utilisés
- commandes de lancement
- version Node.JS requise

---

```
{
  "private": true,
  "name": "Test APP",
  "description": "This is an example package.json",
  "version": "0.0.0-this-does-not-matter",
  "license": "MIT",
  "scripts": {
    "dev": "npx poi",
  },
  "devDependencies": {
    "less": "2.7.2",
    "less-loader": "4.0.5",
  },
  "dependencies": {
    "lodash": "4.17.4",
    "moment": "2.18.1",
  }
}
```
---
# Package.json

- **scripts** : scripts à lancer via `npm run`
- **devDependencies** : Dépendances servant uniquement pour la phase de développement
- **dependencies** : dépendances du projet
- **private** : Si à `true`, le projet ne sera jamais publié sur npm si vous lancez `npm publish` par mégarde

---
#### EventLoop 

```
   ┌───────────────────────┐
┌─>│        timers         │
│  └──────────┬────────────┘
│  ┌──────────┴────────────┐
│  │     I/O callbacks     │
│  └──────────┬────────────┘
│  ┌──────────┴────────────┐
│  │     idle, prepare     │
│  └──────────┬────────────┘      ┌───────────────┐
│  ┌──────────┴────────────┐      │   incoming:   │
│  │         poll          │<─────┤  connections, │
│  └──────────┬────────────┘      │   data, etc.  │
│  ┌──────────┴────────────┐      └───────────────┘
│  │        check          │
│  └──────────┬────────────┘
│  ┌──────────┴────────────┐
└──┤    close callbacks    │
   └───────────────────────┘
```
---
# EventLoop (détails)
   
   - **timers** : lance les callbacks programmés par `setTimeout` et `setIntervale`
   - **I/O callbacks** : lance tous les autres callbacks
   - **idle, prepare** : utilisé par le coeur de Node.JS
   - **poll** : Créer de nouveauc événements d'entrée/sortie. Le cas échéant, peut bloquer l'exécution du script.
   - **check** : invoque les callbacks de `setImmediate`
   - **close callbacks** : `socket.on('close')`, ...

---
# EventLoop (détails)

- Permet l'asynchrone
- Possibilité de forcer l'exécution au prochain passage avec `process.nextTick()` 
- Fonctions avec callback pas toujours asynchrones selon ce qu'elles font
- Promesses toujours Asynchrones

---
# EventLoop (exemples)

```javascript
const funcSync = callback => {
    let fields = {
        foo : 'foo'
    };
    callback(fields);
};

console.log('a');
funcSync(field => { console.log(field); });
console.log('fin');
```

```
a
{foo: "foo"}
fin
```

---
# EventLoop (exemples)

```javascript
const funcSync = callback => {
    let fields = { foo : 'foo'};
    process.nextTick(() => {
    	callback(fields);
    });
};

console.log('a');
funcSync(field => { console.log(field); });
console.log('fin');
```

```
a
fin
{foo: "foo"}
```

---
# EventLoop (exceptions)

- **Attention** : tous les callbacks ne sont pas asynchrones de base :

```javascript
const a = [1, 2, 3, 4];

a.forEach((value) => {
    console.log(value);
});

console.log('after forEach');
```
- Les fonctions des types de base (String, Object, Array, ...) sont toujours synchrones.

---
# Versions de Node.JS

![version](https://github.com/nodejs/Release/raw/master/schedule.png)

---
### Versions de Node.JS

| Release   |  LTS Status     | Active LTS Start  | Maintenance End   |
|   :--:    |    :---:        |   :---:           |       :---:       |
|  v0.12.x  |**End-of-Life**  |        -          |    2016-04-01     |  
| 4.x       |**Maintenance**  |    2015-10-01     |    April 2018     |
|  5.x      |No LTS           |                   |                   |
| 6.x       |**Active**       |    2016-10-18     |   April 2019      |
|  7.x      |No LTS           |                   |                   |
|  8.x      |**Pending**      |    2017-10-31     |   December 2019   |

---
### Versions de Node.JS

- Deux types de version :
	- LTS : Support éttendu : Ce sont les versions les plus stables
	- Les autres : versions dites "beta" (test de nouvelles fonctionnalités, ...)

---
# Plan de travail