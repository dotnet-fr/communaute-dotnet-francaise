---
description: >-
  Vous trouverez ici les réponses aux questions les plus communes autour
  d'Entities Framework Core.
---

# Les questions les plus fréquentes avec Entities Framework Core

## Quelle est la grande différence entre Attach et Entry ?

Avec Entry, vous allez mettre **tout votre objet**, une fois attaché au contexte Entities, dans **un état de modification**.

```text
this._context.Entry<Wookie>(wookie).State = EntityState.Modified;


```

Et vu qu'un ORM est très souvent lié à une base de données, la mise à jour du Context avec la base de données va **générer une requête SQL d'UPDATE sur TOUS les champs de l'entité mise à jour** !

Peut-être souhaitez-vous mettre à jour uniquement les propriétés modifiées ?  
Dans ce cas-ci, préférez utiliser Attach : 

```text
this._context.Attach(wookie);
wookie.Name = "Chewie ? ";
this._context.SaveChanges();
```



