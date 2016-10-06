Ce document définit l'ensemble des règles de style et les bonnes pratiques mises en œuvre en CSS chez Adfab.

Le but de ces règles est de créer une base de code uniforme afin de faciliter sa compréhension et son abord par un tiers parce que ce tiers, c'est vous dans trois mois.

# Guide de style

Ce guide de style est très largement inspiré de [celui d'Airbnb](https://github.com/airbnb/css).

## Les noms

* Doivent être écrits en minuscule
* Doivent être séparés par un tiret court (le signe « moins »)
* Doivent être écrits en anglais états-uniens et sans abréviation

## Les déclarations

* Doivent être sur une ligne propre
* Doivent se terminer par une virgule ou une accolade
* Doivent comporter un espace avant une accolade

## Les règles

* Doivent être indentés de 4 espaces par rapport à la déclaration
* Doivent comporter un espace après les deux-points
* Doivent se terminer par un point-virgule

## Les blocs de déclaration

* Doivent être séparés par une ligne vide

## Les propriétés

Elles doivent être organisées par type, dans l'ordre suivant :

 1. Positionnement
 2. Affichage et modèle de boîte
 3. Couleur
 4. Texte
 5. Autre

## Exemple

### Avant

```css
.commentaire, .commentaireEnTete
{
  position: relative;
  line-height: 1.4;
  width: 80%;
  color: #fff
  font-family: sans-serif;
  cursor: pointer;
  margin:10%;
  background: #000;
  display: inline-block
}
.commentaire{
  margin-bottom:20px
}
```

### Après

```css
.comment,
.comment-heading {
    position: relative;

    display: inline-block;
    width: 80%;
    margin: 10%;

    background: #000;
    color: #fff;

    font-family: sans-serif;
    line-height: 1.4;

    cursor: pointer;
}

.comment {
    margin-bottom: 20%;
}
```

# Bonnes pratiques

## Ciblage

* Il doit être explicite : on cible l'élément que l'on souhaite modifier, pas son parent ou ce qui existe déjà
* Il ne doit jamais supposer que le balisage ne changera pas

### Préférer les classes…

#### …aux balises

Le balisage est susceptible d'être modifié en cours ou fin de projet pour des raisons telles que le SEO ou l'optimisation. Appuyer les règles de style sur des classes plutôt que sur les balises permet donc de facilement modifier le balisage sans impacter le style.

#### …et aux identifiants

Ceux-ci ont un poids de 10 fois supérieur à celui d'une classe, ils sont donc difficiles à surcharger et nuisent ainsi à la réutilisation des composants.

L'article de CSS Wizardry sur [les raisons pour lesquelles il est préférable d'utiliser des classes plutôt que des identifiants](http://csswizardry.com/2014/07/hacks-for-dealing-with-specificity/) permet d'aller plus loin sur le sujet.

## Nommage

### <a name="naming-elements"></a> Éléments

Chaque bloc doit être identifié par une classe suffixée de :

* `-block` pour un bloc
* `-page` pour une page

Chaque surcharge d'une classe d'un de ces deux types doit être suffixée par un nom explicite tel que `comment-block-response` ou `text-block-bigger`.

Pour surcharger un bloc sur une page, il faut créer une classe reprenant le nom de la classe de la page, du bloc et éventuellement de sa variation tel que : `product-page-comment-block-title`. Cela permet de garder des règles CSS d'un poids léger (et donc facilement surchargeable), de créer des éléments facilement réutilisables et d'éviter de dépasser la [limite d'imbrication](#nesting-limit).

### <a name="naming-color-var"></a> Variables de couleur

Les noms de variables contenant des couleurs devraient être composés du nom de la couleur et éventuellement d'un des 6 suffixes suivant :

 1. `lightest`
 2. `lighter`
 3. `light`
 4. `dark`
 5. `darker`
 6. `darkest`

On obtient ainsi 7 déclinaisons (car on peut aussi ne pas ajouter de suffixe) pour une seule couleur. Si cela venait à ne pas être suffisant, il s'agirait alors de se rapprocher de la Direction Artistique afin de leur soumettre le problème.

Enfin, il est possible de suffixer une couleur par le nom d'une marque l'utilisant, pour un résultat tel que : `$blue-facebook`, `$blue-twitter`, …

## Structure

### Arborescence

Les projets SASS/LESS doivent suivre l'arborescence ci-dessous.

Aucun fichier spécifique ne doit être créé pour les plateformes mobiles, les règles doivent être intégrées directement sous leur contrepartie *desktop* dans les feuilles de style.

#### `/common/`

Réunit les éléments globaux au projet, ainsi que les blocs uniques qu'on retrouve sur l'ensemble des pages.

#####`common.scss`

Contient le *reset* et le style par défaut des balises.

#####`font.scss`

Contient la définition des familles de polices. L'[article de Jonathan Vallet sur les `font-face`s](http://connect.adfab.fr/design/la-police-comment-bien-l-ecrire) permet d'aller plus loin sur le sujet.
 
#####`var.scss`

Contient les variables globales du projet. La majorité des variables devraient être définies dans ce fichier, le but étant de faciliter la modification du site juste en changeant une variable. On devrait notamment y retrouver :

* **Les couleurs** : Toutes les couleurs utilisées au sein du projet devraient être listée ici, nommée de la façon évoquée dans le [sous-chapitre « Variables de couleur » du chapitre « Nommage »](#naming-color-var)
* **Les couleurs des éléments de base** : Telles que la couleur par défaut du texte (`$text-color`), la couleur des liens (`$link-color`), des titres (`$title-color`), … Bien entendu la valeur de ces variables doit être une couleur définie au dessus tel qu'évoqué ci-dessus
* **La taille des éléments de base** : Pour ceux qui en possèdent une fixe telle que, souvent, la hauteur du header (`$header-height`), du footer (`$footer-height`), … Ce qui permet de les réutiliser au sein d'élément qui se positionnent par rapport à ces derniers (comme un sous-menu, par exemple)

#####`mixin.scss`

#####`sprite.scss`

Contient une classe par élément du *sprite*, au cas où on aurait pas pu utiliser de police d'icônes.

#### `/layout/`

#####`header.scss`

#####`footer.scss`

#####`menu.scss`

#####`sidebar.scss`

#### `/libs/`

Les fichiers CSS renommés pour terminer par `.scss` des librairies qui n’ont pas pu être *mergés* automatiquement via gulp/npm.

Les fichiers des librairies ne doivent pas être surchargés ici mais dans un fichier avec le même nom dans le dossier `/components/`, ce afin de toujours pouvoir mettre la librairie à jour.

#### `/components/`

Le style des composants de base tels que les boutons, les titres ou les formulaires.

#####`button.scss`

#####`title.scss`

Le style des titres et sous-titres.

#####`form.scss`

#####`/libs/`

Un fichier du surcharge par librairie, reprenant le même nom de fichier que dans le dossier `/libs/`.

#### `/blocks/`

Un fichier pour chaque type de bloc, reprenant son nom. Un bloc texte ayant pour classe `text-block` se retrouvera donc le fichier `/blocks/_text.scss`.

#### `/pages/`

Un fichier par page du site reprenant son nom et contenant les surcharges de chaque blocs de la page. Normalement le contenu est assez léger, puisque défini dans chaque bloc. Si cela venait à pas être le cas, il conviendra de s'interroger sur le bon découpage du *design*.

Le fichier le plus gros de ce répertoire devrait être la page d'accueil, généralement la page la plus spécifique d'un site.

Comme pour les blocs, on peut facilement retrouver le chemin du fichier d'une classe de page : `.home-page` sera dans `/pages/_home.scss`.

----------

On hésitera pas à ajouter des variables locales dans les blocs et pages afin de mieux comprendre l'adhérence d'un élément sur un autre.

#### Exemple

```css
input {
    height: 30px;
    width: calc(100% - 60px);
}

button {
    width: 60px;
    height: 30px;
}
```

Dans le code ci-dessus, on pourrait mettre la valeur « `60px` » dans une variable afin de pouvoir facilement la modifier si besoin mais surtout afin d'expliciter la relation entre l'`input` et le `button` : le premier prend toute la largeur disponible soustrait de la largeur du bouton.

## Compréhension

### Utilisation de `z-index`

Une propriété `z-index` doit toujours comporter un commentaire indiquant :

* la raison pour laquelle elle a été ajoutée. Soit généralement l'élément sous ou au dessus duquel l'élément auquel s'applique le `z-index` doit être positionné
* la règle qui le surcharge, si il y en a une

D'autre part, il est préférable de garder des paliers multiples de 5 ou 10 et d'itérer sur cette même base afin d'éviter de finir avec des valeurs fantaisistes de plusieurs milliers, par exemple.

## Optimisation

### <a name="nesting-limit"></a> Limite d'imbrication

Les sélecteurs ne doivent pas dépasser la limite de 3 niveaux de profondeur.

Le respect des [règles de nommage des éléments](#naming-elements) devrait faciliter le respect de celle-ci.

#### Exemple

##### Avant

```css
.home-page {
    .comment-block {
        .comment-block-title {
            span {
                font-style: italic;
            }
        }
    }
}
```

##### Après

```css
.home-page-comment-block-title {
    span {
        font-style: italic;
    }
}
```

### La surqualification

Il convient d'éviter au mieux la sur-qualification des sélecteurs soit de ne cibler que ce qui est strictement nécessaire à l'application des règles. Ainsi on préférera écrire `.nav a` plutôt que `ul.nav li a`.

### L'intention de sélection

L'intention du sélecteur doit correspondre à la raison du votre style. Il convient, par exemple, de se demander si l'on sélectionne un `ul` parce qu'il est à l'intérieur d'un `header` ou bien parce que ce `ul` contient une liste de liens constituant la navigation principale du site. Si cette dernière venait à être la raison d'être du style alors il conviendrait plutôt d'ajouter une classe `header-nav` à l'`ul`. De cette manière, si l'on venait à ajouter un autre `ul` au *header* (pour ajouter un sous-menu, par exemple), il ne prendrait pas le style du menu principal.

## Modernité

À l'heure actuelle on assure plus de compatibilité au delà d'Internet Explorer 9 qui supporte en partie CSS 3, il donc possible d'utiliser certaines de ses fonctionnalités telles que :

* `:not()`, qui permet de sélectionner tous les éléments sauf ceux correspondant au sélecteur qui lui ai passé
* `calc()`, qui permet de calculer des dimensions pour soustraire, par exemple, à un élément prenant l'ensemble de la largeur d'un bloc la taille d'un élément devant venir se positionner à son côté
* `translate(-50%)`, qui permet de centrer des éléments (voir l'[article de CSS Tricks sur le positionnement](https://css-tricks.com/centering-css-complete-guide/) pour aller plus loin)
* `::before` et `::after` qui permettent notamment d'ajouter des éléments graphiques avant ou après un élément sans avoir à ajouter de balisage (typiquement un `span`) pour ce faire

L'utilisation du `display: flex` est recommandée, même si cela nécessite d'utiliser un *polyfill*.

# Pour aller plus loin

* [Sondage de CSS Tricks sur l'ordre des propriétés CSS](https://css-tricks.com/poll-results-how-do-you-order-your-css-properties/)
* [Article de CSS Wizardry sur les raisons pour lesquelles il est préférable d'utiliser des classes plutôt que des identifiants](http://csswizardry.com/2014/07/hacks-for-dealing-with-specificity/)
* [Guide de style CSS/SASS de Airbnb](https://github.com/airbnb/css)
* [Article de Jonathan Vallet sur les `font-face`s](http://connect.adfab.fr/design/la-police-comment-bien-l-ecrire)
* [Article de CSS Tricks sur le positionnement](https://css-tricks.com/centering-css-complete-guide/)
