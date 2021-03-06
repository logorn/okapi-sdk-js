[![NPM version](https://badge.fury.io/js/laposte-okapi-sdk.svg)](http://badge.fury.io/js/laposte-okapi-sdk)
[![Build Status](https://travis-ci.org/DeveloperLaPoste/okapi-sdk-js.png?branch=master)](https://travis-ci.org/DeveloperLaPoste/okapi-sdk-js)
[![Coverage Status](https://coveralls.io/repos/DeveloperLaPoste/okapi-sdk-js/badge.svg)](https://coveralls.io/r/DeveloperLaPoste/okapi-sdk-js)
[![npm](https://img.shields.io/npm/l/express.svg?style=flat-square)]()

<div>
  <a href="https://developer.laposte.fr">
    <img style="display: inline-block" title="Okapi" src="https://github.com/DeveloperLaPoste/okapi-sdk-js/raw/master/assets/img/okapi-logo-200.png">
  </a>
  <a href="https://fr.wikipedia.org/wiki/JavaScript">
    <img style="display: inline-block" title="JavaScript" src="http://i.stack.imgur.com/Mmww2.png"> 
  </a>
  <a href="https://www.laposte.fr/">
    <img style="display: inline-block" title="La Poste" src="https://logorigine.files.wordpress.com/2011/10/logo-la-poste.jpg" height="200"> 
  </a>
</div>

## Le SDK client Okapi pour JavaScript / nodejs / navigateurs

Ce SDK facilite la consommation des [Open APIs de La Poste](https://developer.laposte.fr/), via la plateforme Okapi :

![Developer La Poste](https://github.com/DeveloperLaPoste/okapi-sdk-js/raw/master/assets/img/developer-laposte-fr-screenshot.png)

Pour consommer des APIs de La Poste, vous devez au préalable :
- [Créer votre compte](https://developer.laposte.fr/signup)
- Créer une application et noter la clé d'app générée, à utiliser comme appKey dans le SDK
- Souscrire à une API du [store](https://developer.laposte.fr/products)
 
## Installation

```
$ npm i laposte-okapi-sdk --save
```

## Utilisation

```javascript
  const okapiSdk = require('laposte-okapi-sdk');
  const oka = okapiSdk({appKey: 'mySecretAppKey'});
  oka.api('superapi')
    .version(1)
    .resource('contacts')
    .get()
    .spread((data, res) => {
      console.log('data :', data);
      console.log('status code :', res.statusCode);
    })
    .catch(function(err) {
      console.error(err);
    });
```

La méthode verbe déclenche la requête avec la l'équivalent HTTP de get, post, put, patch ou delete.

Tous les exemples suivants sont équivalents :

- chainage :

    ```javascript  
      oka.api('superapi').version(1).resource('contacts').get()
    ```

- la méthode verbe accepte une chaîne de caractère comme chemin de la ressource :

    ```javascript
      oka.api('superapi').version(1).get('contacts')
    ```

- la méthode verbe considère le paramètre comme l'URL complète s'il est du type String et qu'aucune API n'a été renseignée au préalable :

    ```javascript
      oka.get('superapi/v1/contacts')
    ```

- construction directe via un objet :

    ```javascript
      oka.build({ api: 'superapi', version: 1, resource: 'contacts'}).get()
    ```

- encore plus direct via la méthode verbe :

    ```javascript
      oka.get({ api: 'superapi', version: 1, resource: 'contacts'})
    ```

## Utilisation dans un navigateur

### Après installation via NPM

- Version adaptée à la production :

    ```html
    <script src="node_modules/laposte-okapi-sdk/client/okapi-sdk.min.js"></script>
    ```

- Version non minifiée pour les développements :

    ```html
    <script src="node_modules/laposte-okapi-sdk/client/okapi-sdk.js"></script>
    ```

### Directement

- Version adaptée à la production :

    ```html
    <script src="https://github.com/DeveloperLaPoste/okapi-sdk-js/raw/master/client/okapi-sdk.min.js"></script>
    ```

- Version non minifiée pour les développements :

    ```html
    <script src="https://github.com/DeveloperLaPoste/okapi-sdk-js/raw/master/client/okapi-sdk.js"></script>
    ```

## Référence API

Les méthodes suivantes peuvent être chainées : elles retournent this (Object) pour permettre un chainage des appels.

### .api

Définit le contexte d'URL de l'API à consommer.

Arguments : contexte d'URL de l'API (String)

### .version

Définit la version de l'API à consommer.

Arguments : version (Integer|String)

### .resource

Définit l'URI de ressource de l'API à consommer.

Arguments : URI de la ressource (String)

### .uri

Définit une URI complète à utiliser (alternative à l'utilisation de .api et .version).

Arguments : uri (String) (ex : '/APIname/APIversion/resource')

### .body

Définit le corps de la requête.

Arguments : corps (Object)

### .query

Définit les paramètres de query string.

Arguments: query (Object)

### .params

Défnit les paramètres de l'URI.

Arguments: params (Object)

### .attachment

Définit un fichier à uploader.

Arguments: attachment (Object)

### .build

Méthode utilitaire tout-en-un qui construit l'URI.

Arguments: opt (Object)
 
Exemple :

```{API name, API version, resource, [...]})```

Les méthodes suivantes ne sont pas chainées :

### .toUrl

Retourne l'URL complète de la requête.

Arguments: [opt] (Object)

Exemple : 

```{API name, API version, resource, [...]}```

Retourne une URL complète (String)

### .get | .post | .put | .patch | .post | .delete

Ces méthodes sont identiques à leur équivalent HTTP, l'invocation de l'une de ces méthode déclenche l'appel de la requête au serveur.

Arguments: [opt] (Object)

Exemple : 

```{API name, API version, resource, [...]}```

Retourne une promesse qui se réalise avec les arguments suivants :
- res : réponse (Object)
- body : corps de la réponse body (Object)

