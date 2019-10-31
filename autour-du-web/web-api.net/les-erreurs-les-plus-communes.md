---
description: 'Wiki des erreurs les plus connues, durant vos développements d''application'
---

# Les erreurs les plus communes

## Que faire quand j'ai System.NotSupportedException: Deserialization of reference types without parameterless constructor is not supported ?

Vous avez sans doute tenté de profiter du Binder automatique d'asp.net core. Et c'est une très bonne chose !

Cependant, le Binder par défaut cherche à instancier, en automatique, votre classe. Ne sachant pas quel\(s\) paramètre\(s\) mettre dans votre constructeur, **il attend un constructeur vide**.

## Que faire quand j'ai InvalidOperationException ?

![](../../.gitbook/assets/image%20%281%29.png)

Voici les questions à vous poser :

* Avez-vous créé un Controller héritant de [ControllerBase](https://docs.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.mvc.controllerbase?view=aspnetcore-3.0) ?
* Avez-vous ajouté [l'attribut de routage](https://docs.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.mvc.routeattribute?view=aspnetcore-3.0) sur au moins votre Controller ? 

Au minimum, vous devez avoir ces attributs :

![](../../.gitbook/assets/image%20%2810%29.png)



