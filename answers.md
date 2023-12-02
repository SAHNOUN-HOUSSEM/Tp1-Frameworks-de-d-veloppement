1. Modifiez le route pour inclure l’URL Movie/released/2020/03 pour une Action
   ByRelease ayant comme arguments (month, year) retournant juste un contenu.

l'action ByRelease est ajoutée dans le contrôlleur des Movies

2. Exécutez. Que remarquez vous? Quel changement à faire pour que le système de routage prend en charge cet route? Expliquez les différentes éventualités rencontrées.

En accedant à l'url Movie/released/2020/03 on obtient une erreur 404 , (route non définie).
justification: si le middleware de routage trouve une correspondance entre l'URL de la requête et un modèle de route, il mappe la requête à l'action du contrôleur spécifiée par le modèle de route. chose qui n'est pas vérifiée dans notre cas.
Pour que le système de routage prenne en charge cette route il faut ajouter l'attribut de routage [Route("Movies/released/{year}/{month}")] avant l'action ByRelease

les différentes éventualités rencontrées:

\*Conflits de route: Il faut respecter l'ordre des routes dans le fichier Program.cs

\*Correspondance de route: Il faut mapper le route dans le fichier Program.cs avec le controlleur et l'action correspondante

3. Présentez avec des exemples les différents systèmes de routage si vous travaillez avec le
   framework de développement web ASP.Net.

ASP.NET offre plusieurs systèmes de routage pour mapper les requêtes HTTP aux actions de contrôleur. Voici quelques exemples :

\*Routage conventionnel : C'est le système de routage traditionnel d'ASP.NET MVC. Il utilise des modèles de route définis dans le fichier Program.cs pour mapper les requêtes aux actions de contrôleur.
app.UseEndpoints(endpoints =>
{
endpoints.MapControllerRoute(
name: "default",
pattern: "{controller=Home}/{action=Index}/{id?}");
});

*Routage par attributs : Ce système de routage permet de définir les routes directement sur les actions de contrôleur en utilisant des attributs.
[Route("Movies/released/{year}/{month}")]
public IActionResult ByReleaseDate(int year, int month)
{
// Votre logique ici
}
*Routage basé sur les zones : Dans les grandes applications, on peut diviser notre application en zones pour organiser mieux le code. Chaque zone peut avoir son propre système de routage.
app.UseEndpoints(endpoints =>
{
endpoints.MapControllerRoute(
name: "AreaRoute",
pattern: "{area:exists}/{controller=Home}/{action=Index}/{id?}");
});
\*Routage d'endpoints : Introduit dans ASP.NET Core 2.2, ce système de routage offre plus de contrôle sur le routage et permet de définir des politiques de routage au niveau de l'endpoint.
app.UseEndpoints(endpoints =>
{
endpoints.MapGet("/hello", async context =>
{
await context.Response.WriteAsync("Hello World!");
});
});

4. On veut à présent passer deux modèles à la vue (Movie et Customer)
   # Ajouter une classe Customer (Id, Name)
   ->créer une classe Customer
   # On veut passer à la vue un film et une Liste de Clients (Penser à ajouter ViewModel)
   ->créer un dossier "ViewModel" contenant la classe "FilmClients"
   # Lister (statique) les enregistrements au niveau du contrôleur (retourner le VM)
   -> var customers = new List<Customer>(){...}
   # Changer le modèle assigné à la vue
   ->ajouter: "" @model ASPCoreApplication2023.ViewModel.FilmClients ""
   # Récupérer les détails du client par son Id.
   ->géré par l'action "Client"
