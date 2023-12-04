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

Comme nous avons créer un nouveau composant, nous allons l'importer dans le fichier **app.module.ts**
