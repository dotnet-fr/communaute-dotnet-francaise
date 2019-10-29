---
description: 'Tout pour bien commencer autour d''entities framework core, avec dotnet core'
---

# Entities framework core

Première étape : ajout du Package **Microsoft. EntityFrameworkCore. SqlServer ou à minimum :Microsoft. EntityFrameworkCore**

![](../.gitbook/assets/image%20%284%29.png)

Acceptons les licences

![](../.gitbook/assets/image%20%283%29.png)

### Puis créeons notre context ORM Entities Framework Core

```text
using Microsoft.EntityFrameworkCore;

public class DefaultContext : DbContext
{
}
```

En pensant à ajouter la bonne référence

![](../.gitbook/assets/image%20%2817%29.png)

