---
description: 'Tout pour bien commencer autour d''entities framework core, avec dotnet core'
---

# Entities framework core

Première étape : ajout du Package **Microsoft. EntityFrameworkCore. SqlServer ou à minimum :Microsoft. EntityFrameworkCore**

![](../../.gitbook/assets/image%20%284%29.png)

Acceptons les licences

![](../../.gitbook/assets/image%20%283%29.png)

### Puis créeons notre context ORM Entities Framework Core

```text
using Microsoft.EntityFrameworkCore;

public class DefaultContext : DbContext
{
}
```

En pensant à ajouter la bonne référence

![](../../.gitbook/assets/image%20%2819%29.png)



### Ajoutons une classe et son DbSet

```text
public class DefaultContext : DbContext
{
    public DefaultContext() { }

    public DefaultContext(DbContextOptions options) : base(options)
    {
        
    }

    protected override void OnModelCreating(ModelBuilder modelBuilder)
    {
        base.OnModelCreating(modelBuilder);
    }

    public DbSet<Wookie> Wookies { get; set; }
}
```

### Travail en mémoire, sans réelle base de données

Si vous n'avez pas encore de base de données, vous pouvez indiquer à **Entities de travailler en mémoire**.

Attention, ici, les contraintes d'intégrité ne sont pas vérifier. C'est très pratique dans certains cas, cependant :

* Quand la base de données n'est pas prête et que l'on doit tout de même **livrer un montrable**
* Lorsque l'on souhaite **lancer des tests unitaires, sans utiliser une vraie base de données**

**Vous devez alors paramétrer Entities pour forcer le travail en mémoire, grâce à l'extension :** 

![](../../.gitbook/assets/image%20%2817%29.png)



En la **configurant côté Startup.cs** : 

```text
 public void ConfigureServices(IServiceCollection services)
{
    services.AddDbContext<Models.Contexts.DefaultContext>((builder) => builder.UseInMemoryDatabase("DefaultContext"));
    
    services.AddControllers();
}
```

Vous allez pouvoir l'appeler dans votre Controller, **sans créer de base de données**, sous SQL SERVER par exemple;

