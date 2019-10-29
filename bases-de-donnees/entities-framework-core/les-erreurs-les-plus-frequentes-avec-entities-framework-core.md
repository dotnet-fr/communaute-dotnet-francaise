---
description: >-
  Erreurs les plus fréquentes, et comment les résoudre, avec Entities Framework
  core
---

# Les erreurs les plus fréquentes avec Entities Framework Core

## System.ArgumentException - AddDbContext was called with configuration, but the context type only declares a parameterless constructor

![](../../.gitbook/assets/image%20%2815%29.png)

Ici, nous avons créé un Context ORM Entities Framework Core, qui n'a **qu'un constructeur vide**.  
Nous devons ajouter un cnostructor dédié pour prendre en compte la configuration souhaité depuis Startup.cs.  


{% code-tabs %}
{% code-tabs-item title="DefaultContext.cs" %}
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
{% endcode-tabs-item %}
{% endcode-tabs %}

