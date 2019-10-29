---
description: >-
  Erreurs les plus fréquentes, et comment les résoudre, avec Entities Framework
  core
---

# Les erreurs les plus fréquentes avec Entities Framework Core



## System.ArgumentException - AddDbContext was called with configuration, but the context type only declares a parameterless constructor

![](../../.gitbook/assets/image%20%2816%29.png)

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

## System.InvalidOperationException - The instance of the entity type cannot be tracked because an other instance withe same key valud is already tracked

Ici, Entities nous indique qu'on a deux instances avec la même clef en base.  
Testons ces hypothèses : 

* Avez-vous ajouté l'attribut de clef sur l'id ? \[Key\]
* Votre système de génération ramène-t-il une valeur unique à chaque fois ?

Dans notre exemple avec les Wookie, l'attribut static ACCOUNT\_ID ne renvoyait pas la valeur au bon moment.  
Nous avons modifié notre code ainsi : 

```text
public class Wookie
{
    public static int ACCOUNT_ID = 0;

    public Wookie(string name, WarriorType warriorType)
    {
        this.Id = ++ ACCOUNT_ID;
        this.Name = name;
        this.BirthDay = DateTime.Now;
        this.WarriorType = warriorType;
    }

    [Key]
    public int Id { get; set; }

    public string Name { get; private set; }

    public DateTime BirthDay { get; private set; }

    public WarriorType WarriorType { get; set; }
}
```
