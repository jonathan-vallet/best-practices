Le but de ce document est de définir l'ensemble des règles pour structurer et nommer tous les fichiers CSS correctement, et ce de façon exhaustive. De cette façon, chaque développeur devra respecter l'ensemble des règles définies, afin que chacun code de manière uniforme, permettant une lecture et une reprise du code très simple de la part des collègues, ainsi que travailler ensemble sur les projets le plus efficacement possible.
Conventions de nommage
Inspirations
Au niveau du nommage des variables et des règles css/sass: 
Au niveau de l'ordre des règles: https://css-tricks.com/poll-results-how-do-you-order-your-css-properties/
Pour comprendre l'interdiction des id dans la css: http://csswizardry.com/2014/07/hacks-for-dealing-with-specificity/
Écriture des règles
 Afin que n’importe quel développeur puisse s’intégrer facilement au projet, il est important que l’ensemble des développeur code de la même manière. Certains framework imposent leurs conventions de nommage puisqu’il y a déjà du code pré-écrit, mais pour le reste il faut qu’on utilise tous les mêmes conventions. On fonctionne comme l'a défini Airbnb, ce modèle fonctionnant bien: https://github.com/airbnb/css
Les classes en css sont notés en minuscule, séparé par des tirets.
L’accolade se met en fin de ligne pour les déclarations
Un espace entre
2 espaces d’indentation
Une règle css par ligne
Les déclarations des propriétés se font par ordre de pertinence (et non alphabétique, voir plus bas)
Toujours inclure le point-virgule final
Quand on déclare un z-index, toujours mettre un commentaire à côté pour indiquer au-dessus/dessous de quel élément il se trouve, et la règle qu'il surcharge. Pas besoin de mettre des z-index de plusieurs milliers, de 5 en 5 ou 10 en 10 est suffisant, au cas où on doivent intercaler un élément entre 2. Généralement on n’a qu’à mettre un z-index : 1 et 2 pour l’élément à faire passer au dessus.
Pas d'id dans les règles, voir plus bas pour les raisons.
Exemple :
Mauvais:
.avatar{
    border-radius:50%;
    border:2px solid white }
.no, .nope, .not_good {
    // ...
}
#lol-no {
  // ...
}
Bon
.widget {
  z-index: 1 // Under .widget-heading
}
.widget-heading {
  z-index: 2; // Over .widget
}
 
.avatar {
  border-radius: 50%;
  border: 2px solid white;
}

.one,
.selector,
.per-line {
  // ...
}
Cibler les éléments
Dans la mesure du possible, on cible les éléments par une classe et non par l'élément html.
Pour les titres et sous-titres, ne jamais cibler par h1, h2… ces éléments sont susceptibles d’être modifiés en fin de projet lors de la mise en place de SEO, il faut donc limiter l’adhérence entre le structure du html et la mise en page.
De même pour les divs, cibler sur une class -block,ce qui permet de transformer le div en lien facilement.
Complexité des règles
Pas plus de 3 niveaux de profondeur pour définir les règles:
.page-container {
  .content {
    .profile {
      // STOP!
    }
  }
}
En respectant le nommage des éléments comme décrit ci-dessous, ça devrait être très simple à respecter
Ordre des propriétés
Afin de facilement s'y retrouver, on organise les propriétés par type et par importance. L'exemple ci-dessous détaille un ordre plutôt optimal des propriétés. Dans la pratique on ne met pas les commentaires ni les sauts de lignes entre chaque type de propriété, c'est juste à titre d'exemple.
Source: https://css-tricks.com/poll-results-how-do-you-order-your-css-properties/
.selector {
  /* Positioning */
  position: absolute;
  z-index: 10;
  top: 0;
  right: 0;

  /* Display & Box Model */
  display: inline-block;
  overflow: hidden;
  box-sizing: border-box;
  width: 100px;
  height: 100px;
  padding: 10px;
  border: 10px solid #333;
  margin: 10px;

  /* Color */
  background: #000;
  color: #fff
  
  /* Text */
  font-family: sans-serif;
  font-size: 16px;
  line-height: 1.4;
  text-align: right;

  /* Other */
  cursor: pointer;
}
Pas de sélecteurs par id
Il faut bannir l'usage des id dans les règles css. Ils pourront ainsi être utilisés exclusivement pour le JS.
Un id a un poids 10 fois supérieur à une classe, c'est donc très compliqué de le surcharger. En utilisant que des classes, on peut facilement ajouter un niveau de précision pour surcharger un style.
Un id est unique, il empêche la réutilisation d'un composant, d'un bloc, ou du style d'une page.
Pour plus d'informations sur ce sujet: http://csswizardry.com/2014/07/hacks-for-dealing-with-specificity/
Écriture des variables
dans les fichiers sass/less, on écrit les variables en lowercase séparé par des tirets: $my-var. Ce choix a été fait pour correspondre au nommage utilisé sur la doc officielle et d'autres librairies comme Bootstrap.
Pour les couleurs on utilise différents suffixes pour les variantes: dark, darker, dakest, light, lighter, ligthest. par exemple: $grey, $grey-dark, $grey-light... Ce qui permet pour chaque teinte de définir 7 variantes, ce qui devrait être largement suffisant, auquel cas il faut voir avec la DA pour uniformiser davantage les couleurs.
On peut ajouter des couleurs spécifiques pour tout ce qui est marques: $blue-facebook, $blue-twitter...
Langue de nommage
La plupart (sinon tous) des langages sont écrits en anglais-US. Dans un souci de cohérence, il est préférable d'utiliser toujours un anglais américain quand on développe. Pas de français, de franglais ni d’anglais gb dans les noms de classe ou de variable :
On ne veut pas de .footer-block-plan-du-site
On écrit color et pas colour
Pas d’abréviation, on écrit .block-image, pas .block-img
Quand on ne connait pas un mot en anglais, on prend 2 minutes pour le chercher, par exemple sur http://www.wordreference.com/ qui permet de trouver la bonne traduction d’un mot.
CSS et sélecteurs JS
N'utilisez jamais une classe de style CSS pour vos ancres JavaScript
Associer un comportement javascript à une classe de style signifie que nous ne pourrons jamais avoir l'un sans l'autre.
Si vous avez besoin de lier un évènement à une balise, créez une classe JS dans votre CSS. Il s'agit simplement d'une classe avec un nommage .js-, par exemple .js-toggle, .js-drag-and-drop. Cela signifie que nous pouvons joindre les deux classes JS et CSS pour notre balisage, sans avoir de chevauchements gênants.
<th class="is-sortable js-is-sortable"></th>
Le balisage ci-dessus contient deux classes ; la première est associée au style du tableau, la deuxième à une fonction de tri.
Structure générale
Structure des fichiers less/sass
Le dossier sass/less est structuré comme suit:
common
layout
libs
components
blocks
pages
Cette structure correspond au développement atomique qui doit être réalisé sur les pages, comme décrit ci-après. Chaque point correspondant à un fichier sass/less
Pour le responsive, pas de fichier mobile ni tablette, on met les règles directement dans les fichiers correspondants à chaque bloc/page; les blocs étant indépendant et ayant normalement le même comportement à chaque fois qu'ils sont appelés.
common
Les éléments les plus globaux du site, ainsi que les blocs uniques qu'on retrouve sur l'ensemble des pages
common: le reset, les règles communes au site (body/html, paragraphes, titres...
font: la définition des font-family. Pour bien décrire les font-face, suivre les indications données sur l’article du blog : http://connect.adfab.fr/design/la-police-comment-bien-l-ecrire
var: les variables du site
mixin: les mixins utilisées.
sprite: pour le cas où on ne peut pas utiliser de font-icon
layout
header
footer
menu
sidebar
libs
les fichiers css (renommés en scss) des différentes librairies, qui n’ont pas pu être mergés via gulp/npm automatiquement. Si on doit les surcharger on ne le fait pas ici mais dans un fichier avec le même nom dans le dossier components, pour toujours pouvoir mettre à jour la librairie.
components
Le style des plus petites éléments qu'on retrouve sous de nombreuses déclinaisons sur l'ensemble des pages au niveau "inline": les titres, les boutons, les liens... Ces fichiers servent à définir la taille et les effets sur les boutons, les liens, les titres et sous-titres, généralement communs à l'ensemble des blocs, ne serait-ce que pour la police utilisée.
button
title
form: le skin général des formulaires
libs: un fichier par librairie qui reprend le même nom que dans le dossier libs. Chaque fichier contient les surcharges des librairies
blocks
Un fichier pour chaque type de block, reprenant le nom du bloc. On retrouve donc le chemin facilement par rapport à la classe : .text-block sera dans scss/blocks/_text.scss.
Un bloc est une section, une division d'une page. Il peut se retrouver plusieurs fois sur une page et/ou sur plusieurs pages. Chaque section d'une page doit être mise dans un bloc.
pages
Un fichier pour chaque page, reprenant l'id de la page, et contenant les surcharges de chaque blocs de la page. Normalement le contenu est assez léger, puisque défini dans chaque bloc. En théorie on devrait retrouver les backgound-image qui changent, certaines déclinaisons de couleurs sépcifique, surtout sur la home page, généralement la page la plus spécifique d'u site.
Comme pour les blocs on retrouve donc le chemin facilement par rapport à la classe : .home-page sera dans scss/pages/_home.scss.
Variables less/sass
Dans l'idéal, le fichier de var doit être le plus détaillé possible, ce qui permet de changer un paramètre du site juste en changeant une variable. Les couleurs, les hauteurs/largeurs d'éléments, les espacements... doivent être ici
Les couleurs de base: On liste toutes les couleurs utilisées avec un nom simple. Si plusieurs variations d'une couleur se retrouvent sur le site on peut utiliser différents suffixes: dark, darker, light, lighter... Si le site contient trop de variation d'une couleur dans les maquettes, s'assurer avec le graphiste qu'elles sont justifiées. Toutes les couleurs sont définies en tant que variables.
Les couleurs des élément. On utilise $text-color pour la couleur générale du texte du site. On peut retrouver également $title-color, $subtitle-color, $link-color... Ces variables ont pour valeur une autre variable de couleur de base, ce qui permet de faire évoluer le site plus facilement et être bien plus clair.
La hauteur des éléments. Plusieurs éléments ont souvent une hauteur fixe: $header-height, $footer-height... Ce qui permet souvent de les réutiliser vu que d'autres éléments se calent par rapport à ceux là (un sous-menu par exemple). Ainsi en changeant la variable on évite de tout racalculer.
Ne pas hésiter à ajouter des variables dans les blocs et page pour mieux comprendre l'adhérence d'un élément sur un autre. Par exemple:
input {
	height: 15px;
	width: calc(100% - 15px);
}
button {
	width: 15px;
	height: 15px;
	line-height: 15px;
}
Dans ce cas on met "15px" dans une variable, ce qui permettra de le modifier plus facilement si besoin, et de mieux comprendre que l'input et le button ont la même taille.
Nommage des éléments
Le découpage a permis de déterminer les blocs qui sont communs ou spécifiques à chaque page.
Chaque bloc est identifié par une classe:
.my-custom-block pour chaque bloc d'un type. Toujours terminer le nommage par "-block" pour bien identifier les éléments. ex: .text-block
.my-custom-block-variation pour les déclinaisons possibles d'un bloc qu'on retrouve sur plusieurs pages. Cette classe surcharger une ou plusieurs règles, mais il faut appliquer la classe de base aux bloc ex: .text-block-bigger, .text-block-left
.my-custom-page pour les pages. On les nomme avec une classe qui se termine systématiquement par -page. ex: .home-page
.my-custom-page-my-custom-block pour cibler un bloc spécifiquement sur une page pour le surcharger. On doit retrouver le nom de la page et la classe du bloc surchargé, et éventuellement le nom du bloc spécifique pour le retrouver facilement. ex: .home-page-intro-text-block
Pour les éléments à l’intérieur des blocs, on reprend le nom du bloc, suffixé de notre élément. Par exemple : .header-block-title, .header-block-description…
De cette façon dans le scss on n’a pas besoin d’imbriquer les éléments dans le bloc, ce qui permet d’avoir un poids très léger sur les règles css (et ne pas dépasser les 3 niveaux de complexité, et très facilement les étendre dans les pages.
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

Produire du code optimisé
L'intention de sélection
Une sur-qualification des sélecteurs ressemble à div.promo. Vous obtiendrez sûrement le même résultat en utilisant simplement .promo
Un autre exemple d'un sélecteur sur-qualifié pourrait être ul.nav li a {}. Comme ci-dessus, nous pouvons supprimer ul puisque nous savons que .nav est une liste, il est aussi logique que a doit être dans un li, donc nous mettre à la diète ul.nav li a {} pour obtenir simplement .nav a {}.
Au lieu d'utiliser les sélecteurs pour cibler un élément du DOM, il est souvent préférable de mettre une classe sur l'élément que vous voulez explicitement styler. Prenons l'exemple précis d'un sélecteur comme .header ul {} …
Imaginons que ul est en effet le menu principal de notre site Web. il vit dans l'en-tête et vous pensez que se sera le seul ul en ces lieux ; .header ul {} fonctionnera, mais ce n'est pas idéal ou souhaitable. Ce n'est pas à l'épreuve du temps et certainement pas assez explicite. Dès que nous ajouterons un autre ul pour cet en-tête il va adopter le style de notre navigation principale. Il y a de grandes chances que ce ne soit pas voulu. Cela signifie que nous devons soit remanier une grande quantité de codeou annuler beaucoup de styles sur les uls dans ce .header pour supprimer les effets de la sélection globale.
L'intention de votre sélecteur doit correspondre à la raison de votre style. Demandez-vous 'Est-ce-que je sélectionne cela car c'est un ul à l'intérieur de .header ou parce que c'est la navigation principale de mon site ?'. La réponse à cette question permettra de déterminer votre sélecteur.
Soyez explicites ; ciblez l'élément que vous voulez modifier, pas son parent. Ne supposez jamais que le balisage ne changera pas. Codez des sélecteurs qui ciblent ce que vous voulez, pas ce qui se trouve être déjà là.
Penser CSS 3
En 2016, on ne fait plus que du IE 9+, qui supporte bien le CSS 3 globalement. Par exemple:
:not, pour cibler tous les éléments sauf le premier ou le dernier, bien pratique pour mettre un séparateur entre tous les éléments sauf le dernier ou le premier.
calc() pour éviter les margin négatifs ou certains calages hasardeux dans la dimension des éléments
le centrage d'éléments avec les translate(-50%)
mettre les éléments graphiques (icones...) dans les ::before ou ::after, pas dans des spans vides.
Pour les navigateurs récents on peut faire du flex pour bien aligner des éléments ou avoir des tailles harmonieuses, en laissant quand même le fallback pour IE 9 si besoin avec les inline-block
Ne jamais mettre de display: table, table-cell ou autre. Ces display sont réservés aux tableaux uniquement. Il existe suffisamment de manières de centrer des éléments verticalement pour s'en passer. https://css-tricks.com/centering-css-complete-guide/