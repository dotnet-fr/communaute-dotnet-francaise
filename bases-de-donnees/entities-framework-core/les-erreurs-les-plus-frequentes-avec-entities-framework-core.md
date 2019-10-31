---
description: >-
  Erreurs les plus fréquentes, et comment les résoudre, avec Entities Framework
  core
---

# Les erreurs les plus fréquentes avec Entities Framework Core

## Microsoft.EntityFrameworkCore.DbUpdateConcurrencyException  : Attempted to update or delete an entity that does not exist in the store

Vous avez lancé la sauvegarde de votre context Entities, et vous obtenez cette erreur ?

Il semblerait que vous ayiez attaché une instance de votre objet, qui **n'appartient pas à votre context**.  
Entities va vérifier avec l'identifiant \(**l'attribut \[Key\]** \) si l'instance existe déjà dans le context.

Cherchez à attacher des objets déjà existants, ou en tout connus de votre context.

De plus, vérifiez si vous avez bien **la clef de votre instance qui est renseignée**.

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

## Impossible de scaffolder la base de données existantes

![](../../.gitbook/assets/image%20%2818%29.png)

Vous avez sans doute essayer de lancer la **commande de scaffolding depuis une base de données** existante :   
**dotnet ef dbcontext scaffold "Data Source=\(local\): Initial Catalog=StarWars.Database" Microsoft.EntityFrameworkCore.SqlServer**

Il vous faut ajouter la référence au Package :  **Microsoft.EntityFrameworkCore.Design, depuis nuget.**

