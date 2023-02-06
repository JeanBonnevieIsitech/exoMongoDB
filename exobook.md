```javascript

// Créez une base de données sample nommée "sample_db" et une collection appelée "employees". Insérez les documents suivants dans la collection "employees":

use sample_db

// Optionnel en sois car l'insertMany va créé la collection si elle n'existe pas
db.createCollection("employees")

db.employees.insertMany([
  { name: "John Doe", age: 35, job: "Manager", salary: 80000 },
  { name: "Jane Doe", age: 32, job: "Developer", salary: 75000 },
  { name: "Jim Smith", age: 40, job: "Manager", salary: 85000 }
  ])

  // Écrivez une requête MongoDB pour trouver tous les documents dans la collection "employees".
  db.employees.find()
  
  // Écrivez une requête pour trouver tous les documents où l'âge est supérieur à 33.
  db.employees.find({"age":{$gt:33}})
  
  // Écrivez une requête pour trier les documents dans la collection "employees" par salaire décroissant.
  db.employees.aggregate(
  [
    { $sort : {salary : -1}}
    ]
  )
  
  // Écrivez une requête pour sélectionner uniquement le nom et le job de chaque document.
  db.employees.find({},{"name":true,"job":true})

  // Écrivez une requête pour compter le nombre d'employés par poste.

  
  
  
  
  
  
  
  
  
  ```