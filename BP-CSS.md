Ce document définit l'ensemble des règles de style et les bonnes pratiques mises en œuvre en CSS chez Adfab.

Le but de ces règles est de créer une base de code uniforme afin de faciliter sa compréhension et son abord par un tiers parce que ce tiers, c'est vous dans trois mois.

# Guide de style

Ce guide de style est très largement inspiré de [celui d'Airbnb](https://github.com/airbnb/css).

##Les noms

* Doivent être écrits en minuscule
* Doivent être séparés par un tiret court (le signe « moins »)
* Doivent être écrits en anglais états-uniens et sans abréviation

##Les déclarations

* Doivent être sur une ligne propre
* Doivent se terminer par une virgule ou une accolade
* Doivent comporter un espace avant une accolade

##Les règles

* Doivent être indentés de 4 espaces par rapport à la déclaration
* Doivent comporter un espace après les deux-points
* Doivent se terminer par un point-virgule

##Les blocs de déclaration

* Doivent être séparés par une ligne vide

## Les propriétés

Elles doivent être organisées par type, dans l'ordre suivant :

 1. Positionnement
 2. Affichage et modèle de boîte
 3. Couleur
 4. Texte
 5. Autre

##Exemple

###Avant
```
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
###Après
```
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

#Bonnes pratiques

##Ciblage

###Préférer les classes…

####…aux balises

Le balisage est susceptible d'être modifié en cours ou fin de projet pour des raisons telles que le SEO ou l'optimisation. Appuyer les règles de style sur des classes plutôt que sur les balises permet donc de facilement modifier le balisage sans impacter le style.

#### …et aux identifiants

Ceux-ci ont un poids de 10 fois supérieur à celui d'une classe, ils sont donc difficiles à surcharger et nuisent ainsi à la réutilisation des composants.

L'article de CSS Wizardry sur [les raisons pour lesquelles il est préférable d'utiliser des classes plutôt que des identifiants](http://csswizardry.com/2014/07/hacks-for-dealing-with-specificity/) permet d'aller plus loin sur le sujet.

##Nommage

###Variables de couleur

Les noms de variables contenant des couleurs peuvent être suffixés de 6 variantes :

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

Contient les variables globales du projet. La majorité des variables devraient être définies dans ce fichier, le but étant de faciliter la modification du site juste en changeant une variable. Les couleurs, les tailles, les espacements, … devraient être ici.

* Les couleurs de base: On liste toutes les couleurs utilisées avec un nom simple. Si plusieurs variations d'une couleur se retrouvent sur le site on peut utiliser différents suffixes: dark, darker, light, lighter... Si le site contient trop de variation d'une couleur dans les maquettes, s'assurer avec le graphiste qu'elles sont justifiées. Toutes les couleurs sont définies en tant que variables.
* Les couleurs des élément. On utilise $text-color pour la couleur générale du texte du site. On peut retrouver également $title-color, $subtitle-color, $link-color... Ces variables ont pour valeur une autre variable de couleur de base, ce qui permet de faire évoluer le site plus facilement et être bien plus clair.
* La hauteur des éléments. Plusieurs éléments ont souvent une hauteur fixe: $header-height, $footer-height... Ce qui permet souvent de les réutiliser vu que d'autres éléments se calent par rapport à ceux là (un sous-menu par exemple). Ainsi en changeant la variable on évite de tout racalculer.

Ne pas hésiter à ajouter des variables dans les blocs et page pour mieux comprendre l'adhérence d'un élément sur un autre.
```
input {
  height: 15px;
  width: calc(100% - 15px);
}
button {
  width: 15px;
  height: 15px;
  line-height: 15px;
}
```
Dans ce cas on met "15px" dans une variable, ce qui permettra de le modifier plus facilement si besoin, et de mieux comprendre que l'input et le button ont la même taille.

#####`mixin.scss`

Contient les *mixins*.

#####`sprite.scss`

Pour le cas où on ne peut pas utiliser de font-icon

#### `/layout/`

#####`header.scss`

#####`footer.scss`

#####`menu.scss`

#####`sidebar.scss`

#### `/libs/`

les fichiers css (renommés en scss) des différentes librairies, qui n’ont pas pu être mergés via gulp/npm automatiquement. Si on doit les surcharger on ne le fait pas ici mais dans un fichier avec le même nom dans le dossier components, pour toujours pouvoir mettre à jour la librairie.

#### `/components/`

Le style des plus petites éléments qu'on retrouve sous de nombreuses déclinaisons sur l'ensemble des pages au niveau "inline": les titres, les boutons, les liens... Ces fichiers servent à définir la taille et les effets sur les boutons, les liens, les titres et sous-titres, généralement communs à l'ensemble des blocs, ne serait-ce que pour la police utilisée.
* button
* title
* form: le skin général des formulaires
* libs: un fichier par librairie qui reprend le même nom que dans le dossier libs. Chaque fichier contient les surcharges des librairies

#### `/blocks/`

Un fichier pour chaque type de block, reprenant le nom du bloc. On retrouve donc le chemin facilement par rapport à la classe : .text-block sera dans scss/blocks/_text.scss.

Un bloc est une section, une division d'une page. Il peut se retrouver plusieurs fois sur une page et/ou sur plusieurs pages. Chaque section d'une page doit être mise dans un bloc.

#### `/pages/`

Un fichier pour chaque page, reprenant l'id de la page, et contenant les surcharges de chaque blocs de la page. Normalement le contenu est assez léger, puisque défini dans chaque bloc. En théorie on devrait retrouver les backgound-image qui changent, certaines déclinaisons de couleurs sépcifique, surtout sur la home page, généralement la page la plus spécifique d'un site.

Comme pour les blocs on retrouve donc le chemin facilement par rapport à la classe : .home-page sera dans scss/pages/_home.scss.

##Optimisation

### Complexité des règles
Pas plus de 3 niveaux de profondeur pour définir les règles:
```
.page-container {
  .content {
    .profile {
      // STOP!
    }
  }
}
```
En respectant le nommage des éléments comme décrit ci-dessous, ça devrait être très simple à respecter


Quand on déclare un z-index, toujours mettre un commentaire à côté pour indiquer au-dessus/dessous de quel élément il se trouve, et la règle qu'il surcharge. Pas besoin de mettre des z-index de plusieurs milliers, de 5 en 5 ou 10 en 10 est suffisant, au cas où on doivent intercaler un élément entre 2. Généralement on n’a qu’à mettre un z-index : 1 et 2 pour l’élément à faire passer au dessus.

### CSS et sélecteurs JS
N'utilisez jamais une classe de style CSS pour vos ancres JavaScript

Associer un comportement javascript à une classe de style signifie que nous ne pourrons jamais avoir l'un sans l'autre.
Si vous avez besoin de lier un évènement à une balise, créez une classe JS dans votre CSS. Il s'agit simplement d'une classe avec un nommage .js-, par exemple .js-toggle, .js-drag-and-drop. Cela signifie que nous pouvons joindre les deux classes JS et CSS pour notre balisage, sans avoir de chevauchements gênants.
```
<th class="is-sortable js-is-sortable"></th>
```
Le balisage ci-dessus contient deux classes ; la première est associée au style du tableau, la deuxième à une fonction de tri.

## Nommage des éléments
Le découpage a permis de déterminer les blocs qui sont communs ou spécifiques à chaque page.
Chaque bloc est identifié par une classe:
* .my-custom-block pour chaque bloc d'un type. Toujours terminer le nommage par "-block" pour bien identifier les éléments. ex: .text-block
* .my-custom-block-variation pour les déclinaisons possibles d'un bloc qu'on retrouve sur plusieurs pages. Cette classe surcharger une ou plusieurs règles, mais il faut appliquer la classe de base aux bloc ex: .text-block-bigger, .text-block-left
* .my-custom-page pour les pages. On les nomme avec une classe qui se termine systématiquement par -page. ex: .home-page
* .my-custom-page-my-custom-block pour cibler un bloc spécifiquement sur une page pour le surcharger. On doit retrouver le nom de la page et la classe du bloc surchargé, et éventuellement le nom du bloc spécifique pour le retrouver facilement. ex: .home-page-intro-text-block

Pour les éléments à l’intérieur des blocs, on reprend le nom du bloc, suffixé de notre élément. Par exemple : .header-block-title, .header-block-description…

De cette façon dans le scss on n’a pas besoin d’imbriquer les éléments dans le bloc, ce qui permet d’avoir un poids très léger sur les règles css (et ne pas dépasser les 3 niveaux de complexité, et très facilement les étendre dans les pages.
```
// blocks/_header.scss
.header-block {
}
.header-block-title {
}
.header-block-list{
  li {
  }  
}
 
// pages/_home.scss
.home-page {
  .header-block {
 
  }
}
// ou pour limiter la profondeur des blocs
.home-page-header-block {
 
}
```

## Produire du code optimisé
### L'intention de sélection
Une sur-qualification des sélecteurs ressemble à div.promo. Vous obtiendrez sûrement le même résultat en utilisant simplement .promo

Un autre exemple d'un sélecteur sur-qualifié pourrait être ul.nav li a {}. Comme ci-dessus, nous pouvons supprimer ul puisque nous savons que .nav est une liste, il est aussi logique que a doit être dans un li, donc nous mettre à la diète ul.nav li a {} pour obtenir simplement .nav a {}.

Au lieu d'utiliser les sélecteurs pour cibler un élément du DOM, il est souvent préférable de mettre une classe sur l'élément que vous voulez explicitement styler. Prenons l'exemple précis d'un sélecteur comme .header ul {} …

Imaginons que ul est en effet le menu principal de notre site Web. il vit dans l'en-tête et vous pensez que se sera le seul ul en ces lieux ; .header ul {} fonctionnera, mais ce n'est pas idéal ou souhaitable. Ce n'est pas à l'épreuve du temps et certainement pas assez explicite. Dès que nous ajouterons un autre ul pour cet en-tête il va adopter le style de notre navigation principale. Il y a de grandes chances que ce ne soit pas voulu. Cela signifie que nous devons soit remanier une grande quantité de codeou annuler beaucoup de styles sur les uls dans ce .header pour supprimer les effets de la sélection globale.

L'intention de votre sélecteur doit correspondre à la raison de votre style. Demandez-vous 'Est-ce-que je sélectionne cela car c'est un ul à l'intérieur de .header ou parce que c'est la navigation principale de mon site ?'. La réponse à cette question permettra de déterminer votre sélecteur.

Soyez explicites ; ciblez l'élément que vous voulez modifier, pas son parent. Ne supposez jamais que le balisage ne changera pas. Codez des sélecteurs qui ciblent ce que vous voulez, pas ce qui se trouve être déjà là.

### Penser CSS 3
En 2016, on ne fait plus que du IE 9+, qui supporte bien le CSS 3 globalement. Par exemple:
* :not, pour cibler tous les éléments sauf le premier ou le dernier, bien pratique pour mettre un séparateur entre tous les éléments sauf le dernier ou le premier.
* calc() pour éviter les margin négatifs ou certains calages hasardeux dans la dimension des éléments
* le centrage d'éléments avec les translate(-50%)
* mettre les éléments graphiques (icones...) dans les ::before ou ::after, pas dans des spans vides.
* Pour les navigateurs récents on peut faire du flex pour bien aligner des éléments ou avoir des tailles harmonieuses, en laissant quand même le fallback pour IE 9 si besoin avec les inline-block
* Ne jamais mettre de display: table, table-cell ou autre. Ces display sont réservés aux tableaux uniquement. Il existe suffisamment de manières de centrer des éléments verticalement pour s'en passer. https://css-tricks.com/centering-css-complete-guide/

# Pour aller plus loin

* [Sondage de CSS Tricks sur l'ordre des propriétés CSS](https://css-tricks.com/poll-results-how-do-you-order-your-css-properties/)
* [Article de CSS Wizardry sur les raisons pour lesquelles il est préférable d'utiliser des classes plutôt que des identifiants](http://csswizardry.com/2014/07/hacks-for-dealing-with-specificity/)
* [Guide de style CSS/SASS de Airbnb](https://github.com/airbnb/css)
* [Article de Jonathan Vallet sur les `font-face`s](http://connect.adfab.fr/design/la-police-comment-bien-l-ecrire)
