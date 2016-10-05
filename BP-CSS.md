Ce document d�finit l'ensemble des r�gles de style et les bonnes pratiques mises en �uvre en CSS chez Adfab.

Le but de ces r�gles est de cr�er une base de code uniforme afin de faciliter sa compr�hension et son abord par un tiers parce que ce tiers, c'est vous dans trois mois.

# Guide de style

Ce guide de style est tr�s largement inspir� de [celui d'Airbnb](https://github.com/airbnb/css).

##Les noms

* Doivent �tre �crits en minuscule
* Doivent �tre s�par�s par un tiret court (le signe � moins �)
* Doivent �tre �crits en anglais �tats-uniens et sans abr�viation

##Les d�clarations

* Doivent �tre sur une ligne propre
* Doivent se terminer par une virgule ou une accolade
* Doivent comporter un espace avant une accolade

##Les r�gles

* Doivent �tre indent�s de 4 espaces par rapport � la d�claration
* Doivent comporter un espace apr�s les deux-points
* Doivent se terminer par un point-virgule

##Les blocs de d�claration

* Doivent �tre s�par�s par une ligne vide

## Les propri�t�s

Elles doivent �tre organis�es par type, dans l'ordre suivant :

 1. Positionnement
 2. Affichage et mod�le de bo�te
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
###Apr�s
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

###Pr�f�rer les classes�

####�aux balises

Le balisage est susceptible d'�tre modifi� en cours ou fin de projet pour des raisons telles que le SEO ou l'optimisation. Appuyer les r�gles de style sur des classes plut�t que sur les balises permet donc de facilement modifier le balisage sans impacter le style.

#### �et aux identifiants

Ceux-ci ont un poids de 10 fois sup�rieur � celui d'une classe, ils sont donc difficiles � surcharger et nuisent ainsi � la r�utilisation des composants.

L'article de CSS Wizardry sur [les raisons pour lesquelles il est pr�f�rable d'utiliser des classes plut�t que des identifiants](http://csswizardry.com/2014/07/hacks-for-dealing-with-specificity/) permet d'aller plus loin sur le sujet.

##Nommage

###Variables de couleur

Les noms de variables contenant des couleurs peuvent �tre suffix�s de 6 variantes :

 1. `lightest`
 2. `lighter`
 3. `light`
 4. `dark`
 5. `darker`
 6. `darkest`

On obtient ainsi 7 d�clinaisons (car on peut aussi ne pas ajouter de suffixe) pour une seule couleur. Si cela venait � ne pas �tre suffisant, il s'agirait alors de se rapprocher de la Direction Artistique afin de leur soumettre le probl�me.

Enfin, il est possible de suffixer une couleur par le nom d'une marque l'utilisant, pour un r�sultat tel que : `$blue-facebook`, `$blue-twitter`, �

## Structure

### Arborescence

Les projets SASS/LESS doivent suivre l'arborescence ci-dessous.

Aucun fichier sp�cifique ne doit �tre cr�� pour les plateformes mobiles, les r�gles doivent �tre int�gr�es directement sous leur contrepartie *desktop* dans les feuilles de style.

#### `/common/`

R�unit les �l�ments globaux au projet, ainsi que les blocs uniques qu'on retrouve sur l'ensemble des pages.

#####`common.scss`

Contient le *reset* et le style par d�faut des balises.

#####`font.scss`

Contient la d�finition des familles de polices. L'[article de Jonathan Vallet sur les `font-face`s](http://connect.adfab.fr/design/la-police-comment-bien-l-ecrire) permet d'aller plus loin sur le sujet.
 
#####`var.scss`

Contient les variables globales du projet. La majorit� des variables devraient �tre d�finies dans ce fichier, le but �tant de faciliter la modification du site juste en changeant une variable. Les couleurs, les tailles, les espacements, � devraient �tre ici.

* Les couleurs de base: On liste toutes les couleurs utilis�es avec un nom simple. Si plusieurs variations d'une couleur se retrouvent sur le site on peut utiliser diff�rents suffixes: dark, darker, light, lighter... Si le site contient trop de variation d'une couleur dans les maquettes, s'assurer avec le graphiste qu'elles sont justifi�es. Toutes les couleurs sont d�finies en tant que variables.
* Les couleurs des �l�ment. On utilise $text-color pour la couleur g�n�rale du texte du site. On peut retrouver �galement $title-color, $subtitle-color, $link-color... Ces variables ont pour valeur une autre variable de couleur de base, ce qui permet de faire �voluer le site plus facilement et �tre bien plus clair.
* La hauteur des �l�ments. Plusieurs �l�ments ont souvent une hauteur fixe: $header-height, $footer-height... Ce qui permet souvent de les r�utiliser vu que d'autres �l�ments se calent par rapport � ceux l� (un sous-menu par exemple). Ainsi en changeant la variable on �vite de tout racalculer.

Ne pas h�siter � ajouter des variables dans les blocs et page pour mieux comprendre l'adh�rence d'un �l�ment sur un autre.
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
Dans ce cas on met "15px" dans une variable, ce qui permettra de le modifier plus facilement si besoin, et de mieux comprendre que l'input et le button ont la m�me taille.

#####`mixin.scss`

Contient les *mixins*.

#####`sprite.scss`

Pour le cas o� on ne peut pas utiliser de font-icon

#### `/layout/`

#####`header.scss`

#####`footer.scss`

#####`menu.scss`

#####`sidebar.scss`

#### `/libs/`

les fichiers css (renomm�s en scss) des diff�rentes librairies, qui n�ont pas pu �tre merg�s via gulp/npm automatiquement. Si on doit les surcharger on ne le fait pas ici mais dans un fichier avec le m�me nom dans le dossier components, pour toujours pouvoir mettre � jour la librairie.

#### `/components/`

Le style des plus petites �l�ments qu'on retrouve sous de nombreuses d�clinaisons sur l'ensemble des pages au niveau "inline": les titres, les boutons, les liens... Ces fichiers servent � d�finir la taille et les effets sur les boutons, les liens, les titres et sous-titres, g�n�ralement communs � l'ensemble des blocs, ne serait-ce que pour la police utilis�e.
* button
* title
* form: le skin g�n�ral des formulaires
* libs: un fichier par librairie qui reprend le m�me nom que dans le dossier libs. Chaque fichier contient les surcharges des librairies

#### `/blocks/`

Un fichier pour chaque type de block, reprenant le nom du bloc. On retrouve donc le chemin facilement par rapport � la classe : .text-block sera dans scss/blocks/_text.scss.

Un bloc est une section, une division d'une page. Il peut se retrouver plusieurs fois sur une page et/ou sur plusieurs pages. Chaque section d'une page doit �tre mise dans un bloc.

#### `/pages/`

Un fichier pour chaque page, reprenant l'id de la page, et contenant les surcharges de chaque blocs de la page. Normalement le contenu est assez l�ger, puisque d�fini dans chaque bloc. En th�orie on devrait retrouver les backgound-image qui changent, certaines d�clinaisons de couleurs s�pcifique, surtout sur la home page, g�n�ralement la page la plus sp�cifique d'un site.

Comme pour les blocs on retrouve donc le chemin facilement par rapport � la classe : .home-page sera dans scss/pages/_home.scss.

##Optimisation

### Complexit� des r�gles
Pas plus de 3 niveaux de profondeur pour d�finir les r�gles:
```
.page-container {
  .content {
    .profile {
      // STOP!
    }
  }
}
```
En respectant le nommage des �l�ments comme d�crit ci-dessous, �a devrait �tre tr�s simple � respecter


Quand on d�clare un z-index, toujours mettre un commentaire � c�t� pour indiquer au-dessus/dessous de quel �l�ment il se trouve, et la r�gle qu'il surcharge. Pas besoin de mettre des z-index de plusieurs milliers, de 5 en 5 ou 10 en 10 est suffisant, au cas o� on doivent intercaler un �l�ment entre 2. G�n�ralement on n�a qu�� mettre un z-index : 1 et 2 pour l��l�ment � faire passer au dessus.

### CSS et s�lecteurs JS
N'utilisez jamais une classe de style CSS pour vos ancres JavaScript

Associer un comportement javascript � une classe de style signifie que nous ne pourrons jamais avoir l'un sans l'autre.
Si vous avez besoin de lier un �v�nement � une balise, cr�ez une classe JS dans votre CSS. Il s'agit simplement d'une classe avec un nommage .js-, par exemple .js-toggle, .js-drag-and-drop. Cela signifie que nous pouvons joindre les deux classes JS et CSS pour notre balisage, sans avoir de chevauchements g�nants.
```
<th class="is-sortable js-is-sortable"></th>
```
Le balisage ci-dessus contient deux classes ; la premi�re est associ�e au style du tableau, la deuxi�me � une fonction de tri.

## Nommage des �l�ments
Le d�coupage a permis de d�terminer les blocs qui sont communs ou sp�cifiques � chaque page.
Chaque bloc est identifi� par une classe:
* .my-custom-block pour chaque bloc d'un type. Toujours terminer le nommage par "-block" pour bien identifier les �l�ments. ex: .text-block
* .my-custom-block-variation pour les d�clinaisons possibles d'un bloc qu'on retrouve sur plusieurs pages. Cette classe surcharger une ou plusieurs r�gles, mais il faut appliquer la classe de base aux bloc ex: .text-block-bigger, .text-block-left
* .my-custom-page pour les pages. On les nomme avec une classe qui se termine syst�matiquement par -page. ex: .home-page
* .my-custom-page-my-custom-block pour cibler un bloc sp�cifiquement sur une page pour le surcharger. On doit retrouver le nom de la page et la classe du bloc surcharg�, et �ventuellement le nom du bloc sp�cifique pour le retrouver facilement. ex: .home-page-intro-text-block

Pour les �l�ments � l�int�rieur des blocs, on reprend le nom du bloc, suffix� de notre �l�ment. Par exemple : .header-block-title, .header-block-description�

De cette fa�on dans le scss on n�a pas besoin d�imbriquer les �l�ments dans le bloc, ce qui permet d�avoir un poids tr�s l�ger sur les r�gles css (et ne pas d�passer les 3 niveaux de complexit�, et tr�s facilement les �tendre dans les pages.
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

## Produire du code optimis�
### L'intention de s�lection
Une sur-qualification des s�lecteurs ressemble � div.promo. Vous obtiendrez s�rement le m�me r�sultat en utilisant simplement .promo

Un autre exemple d'un s�lecteur sur-qualifi� pourrait �tre ul.nav li a {}. Comme ci-dessus, nous pouvons supprimer ul puisque nous savons que .nav est une liste, il est aussi logique que a doit �tre dans un li, donc nous mettre � la di�te ul.nav li a {} pour obtenir simplement .nav a {}.

Au lieu d'utiliser les s�lecteurs pour cibler un �l�ment du DOM, il est souvent pr�f�rable de mettre une classe sur l'�l�ment que vous voulez explicitement styler. Prenons l'exemple pr�cis d'un s�lecteur comme .header ul {} �

Imaginons que ul est en effet le menu principal de notre site Web. il vit dans l'en-t�te et vous pensez que se sera le seul ul en ces lieux ; .header ul {} fonctionnera, mais ce n'est pas id�al ou souhaitable. Ce n'est pas � l'�preuve du temps et certainement pas assez explicite. D�s que nous ajouterons un autre ul pour cet en-t�te il va adopter le style de notre navigation principale. Il y a de grandes chances que ce ne soit pas voulu. Cela signifie que nous devons soit remanier une grande quantit� de codeou annuler beaucoup de styles sur les uls dans ce .header pour supprimer les effets de la s�lection globale.

L'intention de votre s�lecteur doit correspondre � la raison de votre style. Demandez-vous 'Est-ce-que je s�lectionne cela car c'est un ul � l'int�rieur de .header ou parce que c'est la navigation principale de mon site ?'. La r�ponse � cette question permettra de d�terminer votre s�lecteur.

Soyez explicites ; ciblez l'�l�ment que vous voulez modifier, pas son parent. Ne supposez jamais que le balisage ne changera pas. Codez des s�lecteurs qui ciblent ce que vous voulez, pas ce qui se trouve �tre d�j� l�.

### Penser CSS 3
En 2016, on ne fait plus que du IE 9+, qui supporte bien le CSS 3 globalement. Par exemple:
* :not, pour cibler tous les �l�ments sauf le premier ou le dernier, bien pratique pour mettre un s�parateur entre tous les �l�ments sauf le dernier ou le premier.
* calc() pour �viter les margin n�gatifs ou certains calages hasardeux dans la dimension des �l�ments
* le centrage d'�l�ments avec les translate(-50%)
* mettre les �l�ments graphiques (icones...) dans les ::before ou ::after, pas dans des spans vides.
* Pour les navigateurs r�cents on peut faire du flex pour bien aligner des �l�ments ou avoir des tailles harmonieuses, en laissant quand m�me le fallback pour IE 9 si besoin avec les inline-block
* Ne jamais mettre de display: table, table-cell ou autre. Ces display sont r�serv�s aux tableaux uniquement. Il existe suffisamment de mani�res de centrer des �l�ments verticalement pour s'en passer. https://css-tricks.com/centering-css-complete-guide/

# Pour aller plus loin

* [Sondage de CSS Tricks sur l'ordre des propri�t�s CSS](https://css-tricks.com/poll-results-how-do-you-order-your-css-properties/)
* [Article de CSS Wizardry sur les raisons pour lesquelles il est pr�f�rable d'utiliser des classes plut�t que des identifiants](http://csswizardry.com/2014/07/hacks-for-dealing-with-specificity/)
* [Guide de style CSS/SASS de Airbnb](https://github.com/airbnb/css)
* [Article de Jonathan Vallet sur les `font-face`s](http://connect.adfab.fr/design/la-police-comment-bien-l-ecrire)
