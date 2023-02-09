## Exercice 1 
Modifiez la collection salle afin que soient dorénavant validés les documents destinés à y être insérés ; cette validation aura lieu en mode « strict » et portera sur les champs suivants :

nom sera obligatoire et devra être de type chaîne de caractères.

capacite sera obligatoire et devra être de type entier (int).

Dans le champ adresse, les champs codePostal et ville, tous deux de type chaîne de caractères, seront obligatoires.
```js
db.runCommand({
  collMod: "salles",
  validator: {
    $jsonSchema: {
      bsonType: "object",
      title: "objet de validation des salles",
      required: ["nom","capacite","adresse.codePostal","adresse.ville"],
      properties: {
        nom: {
          bsonType: "string"
        },
        capacite: {
          bsonType: "int"
        },
        "adresse.codePostal": {
          bsonType: "string"
        },
        "adresse.ville": {
          bsonType: "string"
        }
      }
    }
  }
})
```
Que constatez-vous lors de la tentative d’insertion suivante, et quelle en est la cause ?
```js
db.salles.insertOne( 
{"nom": "Super salle", "capacite": 1500, "adresse": {"ville": "Musiqueville"}} 
) 
```

**Il manque le champ codePostal dans le champ adresse**

Que proposez-vous pour régulariser la situation ?
```js
db.salles2.insertOne( 
{"nom": "Super salle", "capacite": 1500, "adresse": {"ville": "Musiqueville","codePostal":"69100"}} 
) 
```

## Exercice 2

Rajoutez à vos critères de validation existants un critère supplémentaire : le champ _id devra dorénavant être de type entier (int) ou ObjectId.
```js
db.runCommand({
  collMod: "salles",
  validator: {
    $jsonSchema: {
      bsonType: "object",
      title: "objet de validation des salles",
      required: ["nom","capacite","adresse.codePostal","adresse.ville"],
      properties: {
        id: {
          bsonType: ["int","objectId"]
        },
        nom: {
          bsonType: "string"
        },
        capacite: {
          bsonType: "int"
        },
        "adresse.codePostal": {
          bsonType: "string"
        },
        "adresse.ville": {
          bsonType: "string"
        }
      }
    }
  }
})
```
Que se passe-t-il si vous tentez de mettre à jour l’ensemble des documents existants dans la collection à l’aide de la requête suivante :
```js
db.salles.updateMany({}, {$set: {"verifie": true}}) 

```
**ça ne modifie rien**

Supprimez les critères rajoutés à l’aide de la méthode delete en JavaScript

## Exercice 3

Rajoutez aux critères de validation existants le critère suivant :

Le champ smac doit être présent OU les styles musicaux doivent figurer parmi les suivants : "jazz", "soul", "funk" et "blues".

Que se passe-t-il lorsque nous exécutons la mise à jour suivante ?
```js
db.salles.update({"_id": 3}, {$set: {"verifie": false}})
```