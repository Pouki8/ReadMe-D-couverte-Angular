# Mes impressions

## Partie 1 : Créer l'exemple de projet :

**J'ai téléchargé le projet pour le manipuler dans VSC.**

Après avoir ouvert le projet dans VSC, j'ai découvert une multitude de fichier, html, css et de nombreux fichier **.ts** dans plusieurs dossier distinct.

J'ai ouvert la page google du projet avec : **localhost:4200**, ce qui m'a permet de voir la page internet de ce projet. Il n'est pas possible de l'ouvrir avec **Go Live**, car les contenus des fichiers **.html** sont vides ou pratiquement vides. **_Le contenu est entre double accolade et lisible tel quel_**

Lorsque l'on parcourt les dossiers et les fichiers, on peut remarquer que l'**"index.html"** principale ne va renvoyer que le **head** de la page, le **body** (corp) de la page ne va contenir uniquement une seule information : une balise fermante`<app-root></app-root>`

Lorsque l'on parcours le **style.css**, qu'en à lieu est très complet. Il renvoie de nombreuses balise et `class`.

Le fichier **main.ts** qui est un **_"TypeScript"_** n'a que peut d'information.

**Un gros dossier _app_ avec plusieurs fichiers et sous-dossier et un dossier _asset_ contenant un fichier _.json_.**

## Partie 2 : Créer la liste de produits :

#### Dans le fichier product-list.component.html :

Nous ajoutons dans le fichier **product-list.component.html**, un `ngFor` qui permet de faire une boucle sur tous les produits que nous ajouterons dans la liste des produits.

Nous appelons le nom des produits avec le nom de la classe du fichier **product.ts** et la propriété du nom du produit : `{{product.name}}`. Cela permet d'afficher ce qu'il y a de saisie dans le fichier **product.ts**. Nous continuons, en ajoutant aussi la description de la même manière, ce qui permet d'afficher la description du fichier **Product.ts**.
Ensuite, nous ajoutons une balise `button` pour afficher un bouton qui nous permet de pouvoir partager le produit choisit. Cette création de bouton se trouve dans le fichier **product-list.component.html** déclarer avec `(click)="share()` dans une balise `<button>`. En cliquant sur ce bouton, cela déclanche une alerte que nous retrouvons comme méthode `share(){ window.alert("Vous avez partagé ce produit !")}` qui se trouve dans le fichier **product-list.component.ts**.

## Partie 3 : Transmettre des données à un composant enfant :

Nous créons un nouveau composant avec le terminal : **ng generate component product-alerts** qui intégrera un fichier **.ts**, un fichier **.html**, un fichier **.css** et un fichier pour les tests **.ts**.

On peut remarquer qu'il contient les mêmes `@component` que les autres fichiers **.ts**. Nous ajoutons un `import` en haut du fichier pour permettre de pouvoir travaillé avec le composant **product**. _Nous remarquerons que les imports se font automatiquement dans le fichier **app.mosule.ts**._

Dans la classe `export class ProductAlertsComponent{}`, du fichier **product-alerts.component.ts**, nous définissons une propriété `product` qui sera transmise par le parent du composant grâce à `@Input()`.

Nous allons créer une nouvelle balise `<button>` qui déclenchera une alerte que nous retrouverons dans le fichier **product-list.component.ts**, comme pour le **button `share`**. Mais nous allons dans le fichier **product-list.component.html** pour ajouter l'élément `<app-product-alert>` balise auto-fermante. C'est là que nous découvrons qu'un nouveau bouton est apparût _'Me prévenir'_.

## Partie 4 : Transmettre des données à un composant parent :

Nous devons faire un `import` de _Output_ et _EventEmitter_ de `@angular/core`, sans oublier de les déclarer dans la classe `export class ProductAlertsComponent{}` comme suite :

```
export class ProductAlertsComponent {
  @Input() product: Product | undefined;
  @Output() notify = new EventEmitter();
}
```

Puis nous pouvons modifier le fichier **product-list.component.ts** pour faire une alerte _You will be notified when the product goes on sale_.

Nous devons mettre à jour le fichier **product-list.component.html** qui permettre de déclencher l'alerte _You will be notified when the product goes on sale_.

## Partie 5 : Ajout de navigation :

Nous créons un nouveau composant avec le terminal : **ng generate component product-details** qui intégrera un fichier **.ts**, un fichier **.html**, un fichier **.css** et un fichier pour les tests **.ts**.

**Création de nouveau composant pour le détail des produits**

Dans le terminal, nous devons créer de nouveau composant qui intégrera un fichier **.ts**, un fichier **.html**, un fichier **.css** et un fichier pour les tests **.ts**.

Comme nous avons créer un nouveau composant, il est automatiquement importer dans le fichier **app.module.ts** que nous ouvrons pour ajouter un itinéraire pour les détails du produit avec un `path` dans `import: []` par le biais de RouterModule qui est un module de `@angular/router` **Angular**.

Nous allons, ensuite, dans le **.html** du composant **product-list** pour modifier l'ancre du nom du produit pour inclure un routerLink `[routerLink]="['/products', product.id]"` avec le `product.id`. _Comme expliqué plus tôt_ Cependant, les détails du produit ne s'affiche plus !

C'est en modifiant le fichier **.ts** du composant **product-details**, que nous allons pouvoir afficher de nouveau les détails. Nous allons implémenter un OnInit à la classe `ProductDetailsComponent` et une propriété `product: Product | undefined;` qui sera undefined. Et, ajouter une propriété privé `route` dans le constructor : `constructor(private route: ActivatedRoute) { }`.
Dans la méthode `ngOnInit()`, nous modifions pour accéder aux paramètres de l'itinéraire en utilisant `route.snapshot` qui active avec `ActivatedRouteSnapshot` qui contient les informations sur l'itinéraire actif à ce moment précis.

Dans le **.html** du même composant, nous ajoutons un `*ngIf` que j'ai dû importé dans le fichier **app.module** et préciser les données qui doivent ressortir :

```
<h2>Product Details</h2>

<div *ngIf="product">
  <h3>{{ product.name }}</h3>
  <h4>{{ product.price | currency }}</h4>
  <p>{{ product.description }}</p>
</div>
```

C'est alors que, lorsque l'utilisateur clique sur le nom du produit, le router dirige vers l'URL distincte du produit : **ProductDetailsComponent**. C'est dans ce composant que l'on a appelé les données du _le détail_, nom, prix et description. _(ces détails sont récupérer dans le fichier product.ts)_

## Partie 5 : Créer le service de panier d'achat :

On génère un composant service cart pour pouvoir ajouter la possibilité d'ajouter au panier l'achat. On doit donc importer le composant dans le **Product-details.ts** pour pouvoir créer un bouton dans le **.html** qui permettra d'ajouter au panier le produit sélectionner.

### Configurer le composant panier :

On génère un composant panier qui nous permettre d'avoir une nouvelle page qui nous mène au panier pour voir nos produits ajoutés lorsqu'on a cliqué sur **acheter**. On va importerle composant dans l'app.module et un lien dans le **top-bar.component.html**. Nous allons aussi permettre de faire le lien dans le composant **cart** pour ajouter le **cartService** ce qui permettra de voir dans le panier les ajouts lors du click sur **acheter**. Nous récupérons aussi les prix dans le composant **shipping** en important le composant **cart-service** dans le composant **shipping.composant**.

## Partie 6 : Création du formulaire :

Nous allons ajouter dans le fichier **.html** du composant **cart** la possibilité à l'utilisateur de saisir son nom et son adresse. Cela apparaîtra dans le panier.

# En résumé :

Chaque ajout de composant permet d'ajouter des pages liées à la page principale sans rechargement de la page. A chaque ajout de composant, ils sont directement importé dans le fichier **app.mocule.ts** mais nous devons les importer dans le fichier **.ts** des composants lorsqu'ils seront utilisé (ou appelé par le fichier **.html** mais nous les ajouterons dans les fichiers **.ts** préalablement).

Finallement, cela permettra de pouvoir modifier ou ajouter des données uniquement dans le composant dédié. Par exemple : si les prix des produits changent, nous n'aurons qu'à les modifier dans le **product.ts** qui sera appelé dans le composant **product-list** et affichera le **product-list.html** avec les données saisies dans le **product.ts**.

De même, si l'utilisateur clique sur un des produits, il affichera ce qui est indiqué dans le **product.ts** puisque le composant **product-detail** a un import **product.ts**.

A chaque ajout de composant, il y a l'import dont on a besoin pour renvoyer les données qui s'en réfère.
