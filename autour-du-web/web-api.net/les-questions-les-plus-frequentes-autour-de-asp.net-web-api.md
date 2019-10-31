---
description: >-
  Découvrez ici l'ensemble des questions les plus fréquentes autour du
  développement d'API web avec asp.net core web API.
---

# Les questions les plus fréquentes autour de asp.net web API

## Comment accéder à notre context Entities depuis une contrainte personnalisée ?

Vous l'avez sans doute remarqué : **impossible de récupérer le context Entities depuis le constructor**, comme on le fait depuis nos controllers.

Comment alors, y accéder, et **éviter de casser l'injection de dépendances** que l'on souhaite mettre en place dans notre application ? 

Dans votre fonction Match, vous avez le context Http qui est passé, avec httpContext. Vous pouvez y accéder depuis cette variable !

```text
 public bool Match(HttpContext httpContext, IRouter route, string routeKey, RouteValueDictionary values, RouteDirection routeDirection)
{
    var context = httpContext.RequestServices.GetService(typeof(Models.Contexts.DefaultContext));
    return true;
}
```

