# Bonus
## expliquez ce qui se passe plus bas :  

```js
db.achats.aggregate([
    { $addFields: {
            "total_achats": { $sum: "$achats"
            },
            "total_reduc": { $sum: "$reductions"
            }
        }
    },
    { $addFields: {
            "total_final": { $subtract: [
                    "$total_achats",
                    "$total_reduc"
                ]
            }
        }
    },
    { $project: {
            "_id": 0,
            "nom": 1,
            "prenom": 1,
            "Total payé": { $divide: [
                    { $subtract: [
                            { $multiply: ['$total_final',
                                    100
                                ]
                            },
                            { $mod: [
                                    { $multiply: ['$total_final',
                                            100
                                        ]
                                    },
                                    1
                                ]
                            }
                        ]
                    },
                    100
                ]
            }
        }
    }
]) 
```

## Explication :