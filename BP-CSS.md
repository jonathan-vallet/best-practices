Ce document d�finit l'ensemble des r�gles de style et les bonnes pratiques mises en �uvre en CSS chez Adfab.

Le but de ces r�gles est de cr�er une base de code uniforme afin de faciliter sa compr�hension et son abord par un tiers parce que ce tiers, c'est vous dans trois mois.

# Guide de style

Ce guide de style est tr�s largement inspir� de [celui d'Airbnb](https://github.com/airbnb/css).

## Les noms

* Doivent �tre �crits en minuscule
* Doivent �tre s�par�s par un tiret court (le signe � moins �)
* Doivent �tre �crits en anglais �tats-uniens et sans abr�viation

## Les d�clarations

* Doivent �tre sur une ligne propre
* Doivent se terminer par une virgule ou une accolade
* Doivent comporter un espace avant une accolade

## Les r�gles

* Doivent �tre indent�s de 4 espaces par rapport � la d�claration
* Doivent comporter un espace apr�s les deux-points
* Doivent se terminer par un point-virgule

## Les blocs de d�claration

* Doivent �tre s�par�s par une ligne vide

## Les propri�t�s

Elles doivent �tre organis�es par type, dans l'ordre suivant :

 1. Positionnement
 2. Affichage et mod�le de bo�te
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

### Apr�s

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

* Il doit �tre explicite : on cible l'�l�ment que l'on souhaite modifier, pas son parent ou ce qui existe d�j�
* Il ne doit jamais supposer que le balisage ne changera pas

### Pr�f�rer les classes�

#### �aux balises

Le balisage est susceptible d'�tre modifi� en cours ou fin de projet pour des raisons telles que le SEO ou l'optimisation. Appuyer les r�gles de style sur des classes plut�t que sur les balises permet donc de facilement modifier le balisage sans impacter le style.

#### �et aux identifiants

Ceux-ci ont un poids de 10 fois sup�rieur � celui d'une classe, ils sont donc difficiles � surcharger et nuisent ainsi � la r�utilisation des composants.

L'article de CSS Wizardry sur [les raisons pour lesquelles il est pr�f�rable d'utiliser des classes plut�t que des identifiants](http://csswizardry.com/2014/07/hacks-for-dealing-with-specificity/) permet d'aller plus loin sur le sujet.

## Nommage

### <a name="naming-elements"></a> �l�ments

Chaque bloc doit �tre identifi� par une classe suffix�e de :

* `-block` pour un bloc
* `-page` pour une page

Chaque surcharge d'une classe d'un de ces deux types doit �tre suffix�e par un nom explicite tel que `comment-block-response` ou `text-block-bigger`.

Pour surcharger un bloc sur une page, il faut cr�er une classe reprenant le nom de la classe de la page, du bloc et �ventuellement de sa variation tel que : `product-page-comment-block-title`. Cela permet de garder des r�gles CSS d'un poids l�ger (et donc facilement surchargeable), de cr�er des �l�ments facilement r�utilisables et d'�viter de d�passer la [limite d'imbrication](#nesting-limit).

### <a name="naming-color-var"></a> Variables de couleur

Les noms de variables contenant des couleurs devraient �tre compos�s du nom de la couleur et �ventuellement d'un des 6 suffixes suivant :

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

Contient les variables globales du projet. La majorit� des variables devraient �tre d�finies dans ce fichier, le but �tant de faciliter la modification du site juste en changeant une variable. On devrait notamment y retrouver :

* **Les couleurs** : Toutes les couleurs utilis�es au sein du projet devraient �tre list�e ici, nomm�e de la fa�on �voqu�e dans le [sous-chapitre � Variables de couleur � du chapitre � Nommage �](#naming-color-var)
* **Les couleurs des �l�ments de base** : Telles que la couleur par d�faut du texte (`$text-color`), la couleur des liens (`$link-color`), des titres (`$title-color`), � Bien entendu la valeur de ces variables doit �tre une couleur d�finie au dessus tel qu'�voqu� ci-dessus
* **La taille des �l�ments de base** : Pour ceux qui en poss�dent une fixe telle que, souvent, la hauteur du header (`$header-height`), du footer (`$footer-height`), � Ce qui permet de les r�utiliser au sein d'�l�ment qui se positionnent par rapport � ces derniers (comme un sous-menu, par exemple)

#####`mixin.scss`

#####`sprite.scss`

Contient une classe par �l�ment du *sprite*, au cas o� on aurait pas pu utiliser de police d'ic�nes.

#### `/layout/`

#####`header.scss`

#####`footer.scss`

#####`menu.scss`

#####`sidebar.scss`

#### `/libs/`

Les fichiers CSS renomm�s pour terminer par `.scss` des librairies qui n�ont pas pu �tre *merg�s* automatiquement via gulp/npm.

Les fichiers des librairies ne doivent pas �tre surcharg�s ici mais dans un fichier avec le m�me nom dans le dossier `/components/`, ce afin de toujours pouvoir mettre la librairie � jour.

#### `/components/`

Le style des composants de base tels que les boutons, les titres ou les formulaires.

#####`button.scss`

#####`title.scss`

Le style des titres et sous-titres.

#####`form.scss`

#####`/libs/`

Un fichier du surcharge par librairie, reprenant le m�me nom de fichier que dans le dossier `/libs/`.

#### `/blocks/`

Un fichier pour chaque type de bloc, reprenant son nom. Un bloc texte ayant pour classe `text-block` se retrouvera donc le fichier `/blocks/_text.scss`.

#### `/pages/`

Un fichier par page du site reprenant son nom et contenant les surcharges de chaque blocs de la page. Normalement le contenu est assez l�ger, puisque d�fini dans chaque bloc. Si cela venait � pas �tre le cas, il conviendra de s'interroger sur le bon d�coupage du *design*.

Le fichier le plus gros de ce r�pertoire devrait �tre la page d'accueil, g�n�ralement la page la plus sp�cifique d'un site.

Comme pour les blocs, on peut facilement retrouver le chemin du fichier d'une classe de page : `.home-page` sera dans `/pages/_home.scss`.

----------

On h�sitera pas � ajouter des variables locales dans les blocs et pages afin de mieux comprendre l'adh�rence d'un �l�ment sur un autre.

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

Dans le code ci-dessus, on pourrait mettre la valeur � `60px` � dans une variable afin de pouvoir facilement la modifier si besoin mais surtout afin d'expliciter la relation entre l'`input` et le `button` : le premier prend toute la largeur disponible soustrait de la largeur du bouton.

## Compr�hension

### Utilisation de `z-index`

Une propri�t� `z-index` doit toujours comporter un commentaire indiquant :

* la raison pour laquelle elle a �t� ajout�e. Soit g�n�ralement l'�l�ment sous ou au dessus duquel l'�l�ment auquel s'applique le `z-index` doit �tre positionn�
* la r�gle qui le surcharge, si il y en a une

D'autre part, il est pr�f�rable de garder des paliers multiples de 5 ou 10 et d'it�rer sur cette m�me base afin d'�viter de finir avec des valeurs fantaisistes de plusieurs milliers, par exemple.

## Optimisation

### <a name="nesting-limit"></a> Limite d'imbrication

Les s�lecteurs ne doivent pas d�passer la limite de 3 niveaux de profondeur.

Le respect des [r�gles de nommage des �l�ments](#naming-elements) devrait faciliter le respect de celle-ci.

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

##### Apr�s

```css
.home-page-comment-block-title {
    span {
        font-style: italic;
    }
}
```

### La surqualification

Il convient d'�viter au mieux la sur-qualification des s�lecteurs soit de ne cibler que ce qui est strictement n�cessaire � l'application des r�gles. Ainsi on pr�f�rera �crire `.nav a` plut�t que `ul.nav li a`.

### L'intention de s�lection

L'intention du s�lecteur doit correspondre � la raison du votre style. Il convient, par exemple, de se demander si l'on s�lectionne un `ul` parce qu'il est � l'int�rieur d'un `header` ou bien parce que ce `ul` contient une liste de liens constituant la navigation principale du site. Si cette derni�re venait � �tre la raison d'�tre du style alors il conviendrait plut�t d'ajouter une classe `header-nav` � l'`ul`. De cette mani�re, si l'on venait � ajouter un autre `ul` au *header* (pour ajouter un sous-menu, par exemple), il ne prendrait pas le style du menu principal.

## Modernit�

� l'heure actuelle on assure plus de compatibilit� au del� d'Internet Explorer 9 qui supporte en partie CSS 3, il donc possible d'utiliser certaines de ses fonctionnalit�s telles que :

* `:not()`, qui permet de s�lectionner tous les �l�ments sauf ceux correspondant au s�lecteur qui lui ai pass�
* `calc()`, qui permet de calculer des dimensions pour soustraire, par exemple, � un �l�ment prenant l'ensemble de la largeur d'un bloc la taille d'un �l�ment devant venir se positionner � son c�t�
* `translate(-50%)`, qui permet de centrer des �l�ments (voir l'[article de CSS Tricks sur le positionnement](https://css-tricks.com/centering-css-complete-guide/) pour aller plus loin)
* `::before` et `::after` qui permettent notamment d'ajouter des �l�ments graphiques avant ou apr�s un �l�ment sans avoir � ajouter de balisage (typiquement un `span`) pour ce faire

L'utilisation du `display: flex` est recommand�e, m�me si cela n�cessite d'utiliser un *polyfill*.

# Pour aller plus loin

* [Sondage de CSS Tricks sur l'ordre des propri�t�s CSS](https://css-tricks.com/poll-results-how-do-you-order-your-css-properties/)
* [Article de CSS Wizardry sur les raisons pour lesquelles il est pr�f�rable d'utiliser des classes plut�t que des identifiants](http://csswizardry.com/2014/07/hacks-for-dealing-with-specificity/)
* [Guide de style CSS/SASS de Airbnb](https://github.com/airbnb/css)
* [Article de Jonathan Vallet sur les `font-face`s](http://connect.adfab.fr/design/la-police-comment-bien-l-ecrire)
* [Article de CSS Tricks sur le positionnement](https://css-tricks.com/centering-css-complete-guide/)
