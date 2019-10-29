---
description: 'Wiki des erreurs les plus connues, durant vos développements d''application'
---

# Les erreurs les plus communes

## Que faire quand j'ai InvalidOperationException ?

![](../../.gitbook/assets/image%20%281%29.png)

Voici les questions à vous poser :

* Avez-vous créé un Controller héritant de [ControllerBase](https://docs.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.mvc.controllerbase?view=aspnetcore-3.0) ?
* Avez-vous ajouté [l'attribut de routage](https://docs.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.mvc.routeattribute?view=aspnetcore-3.0) sur au moins votre Controller ? 

Au minimum, vous devez avoir ces attributs :

![](../../.gitbook/assets/image%20%289%29.png)



