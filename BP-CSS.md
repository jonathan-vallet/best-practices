Le but de ce document est de d�finir l'ensemble des r�gles pour structurer et nommer tous les fichiers CSS correctement, et ce de fa�on exhaustive. De cette fa�on, chaque d�veloppeur devra respecter l'ensemble des r�gles d�finies, afin que chacun code de mani�re uniforme, permettant une lecture et une reprise du code tr�s simple de la part des coll�gues, ainsi que travailler ensemble sur les projets le plus efficacement possible.
Conventions de nommage
Inspirations
Au niveau du nommage des variables et des r�gles css/sass: 
Au niveau de l'ordre des r�gles: https://css-tricks.com/poll-results-how-do-you-order-your-css-properties/
Pour comprendre l'interdiction des id dans la css: http://csswizardry.com/2014/07/hacks-for-dealing-with-specificity/
�criture des r�gles
 Afin que n�importe quel d�veloppeur puisse s�int�grer facilement au projet, il est important que l�ensemble des d�veloppeur code de la m�me mani�re. Certains framework imposent leurs conventions de nommage puisqu�il y a d�j� du code pr�-�crit, mais pour le reste il faut qu�on utilise tous les m�mes conventions. On fonctionne comme l'a d�fini Airbnb, ce mod�le fonctionnant bien: https://github.com/airbnb/css
Les classes en css sont not�s en minuscule, s�par� par des tirets.
L�accolade se met en fin de ligne pour les d�clarations
Un espace entre
2 espaces d�indentation
Une r�gle css par ligne
Les d�clarations des propri�t�s se font par ordre de pertinence (et non alphab�tique, voir plus bas)
Toujours inclure le point-virgule final
Quand on d�clare un z-index, toujours mettre un commentaire � c�t� pour indiquer au-dessus/dessous de quel �l�ment il se trouve, et la r�gle qu'il surcharge. Pas besoin de mettre des z-index de plusieurs milliers, de 5 en 5 ou 10 en 10 est suffisant, au cas o� on doivent intercaler un �l�ment entre 2. G�n�ralement on n�a qu�� mettre un z-index : 1 et 2 pour l��l�ment � faire passer au dessus.
Pas d'id dans les r�gles, voir plus bas pour les raisons.
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
Cibler les �l�ments
Dans la mesure du possible, on cible les �l�ments par une classe et non par l'�l�ment html.
Pour les titres et sous-titres, ne jamais cibler par h1, h2� ces �l�ments sont susceptibles d��tre modifi�s en fin de projet lors de la mise en place de SEO, il faut donc limiter l�adh�rence entre le structure du html et la mise en page.
De m�me pour les divs, cibler sur une class -block,ce qui permet de transformer le div en lien facilement.
Complexit� des r�gles
Pas plus de 3 niveaux de profondeur pour d�finir les r�gles:
.page-container {
  .content {
    .profile {
      // STOP!
    }
  }
}
En respectant le nommage des �l�ments comme d�crit ci-dessous, �a devrait �tre tr�s simple � respecter
Ordre des propri�t�s
Afin de facilement s'y retrouver, on organise les propri�t�s par type et par importance. L'exemple ci-dessous d�taille un ordre plut�t optimal des propri�t�s. Dans la pratique on ne met pas les commentaires ni les sauts de lignes entre chaque type de propri�t�, c'est juste � titre d'exemple.
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
Pas de s�lecteurs par id
Il faut bannir l'usage des id dans les r�gles css. Ils pourront ainsi �tre utilis�s exclusivement pour le JS.
Un id a un poids 10 fois sup�rieur � une classe, c'est donc tr�s compliqu� de le surcharger. En utilisant que des classes, on peut facilement ajouter un niveau de pr�cision pour surcharger un style.
Un id est unique, il emp�che la r�utilisation d'un composant, d'un bloc, ou du style d'une page.
Pour plus d'informations sur ce sujet: http://csswizardry.com/2014/07/hacks-for-dealing-with-specificity/
�criture des variables
dans les fichiers sass/less, on �crit les variables en lowercase s�par� par des tirets: $my-var. Ce choix a �t� fait pour correspondre au nommage utilis� sur la doc officielle et d'autres librairies comme Bootstrap.
Pour les couleurs on utilise diff�rents suffixes pour les variantes: dark, darker, dakest, light, lighter, ligthest. par exemple: $grey, $grey-dark, $grey-light... Ce qui permet pour chaque teinte de d�finir 7 variantes, ce qui devrait �tre largement suffisant, auquel cas il faut voir avec la DA pour uniformiser davantage les couleurs.
On peut ajouter des couleurs sp�cifiques pour tout ce qui est marques: $blue-facebook, $blue-twitter...
Langue de nommage
La plupart (sinon tous) des langages sont �crits en anglais-US. Dans un souci de coh�rence, il est pr�f�rable d'utiliser toujours un anglais am�ricain quand on d�veloppe. Pas de fran�ais, de franglais ni d�anglais gb dans les noms de classe ou de variable :
On ne veut pas de .footer-block-plan-du-site
On �crit color et pas colour
Pas d�abr�viation, on �crit .block-image, pas .block-img
Quand on ne connait pas un mot en anglais, on prend 2 minutes pour le chercher, par exemple sur http://www.wordreference.com/ qui permet de trouver la bonne traduction d�un mot.
CSS et s�lecteurs JS
N'utilisez jamais une classe de style CSS pour vos ancres JavaScript
Associer un comportement javascript � une classe de style signifie que nous ne pourrons jamais avoir l'un sans l'autre.
Si vous avez besoin de lier un �v�nement � une balise, cr�ez une classe JS dans votre CSS. Il s'agit simplement d'une classe avec un nommage .js-, par exemple .js-toggle, .js-drag-and-drop. Cela signifie que nous pouvons joindre les deux classes JS et CSS pour notre balisage, sans avoir de chevauchements g�nants.
<th class="is-sortable js-is-sortable"></th>
Le balisage ci-dessus contient deux classes ; la premi�re est associ�e au style du tableau, la deuxi�me � une fonction de tri.
Structure g�n�rale
Structure des fichiers less/sass
Le dossier sass/less est structur� comme suit:
common
layout
libs
components
blocks
pages
Cette structure correspond au d�veloppement atomique qui doit �tre r�alis� sur les pages, comme d�crit ci-apr�s. Chaque point correspondant � un fichier sass/less
Pour le responsive, pas de fichier mobile ni tablette, on met les r�gles directement dans les fichiers correspondants � chaque bloc/page; les blocs �tant ind�pendant et ayant normalement le m�me comportement � chaque fois qu'ils sont appel�s.
common
Les �l�ments les plus globaux du site, ainsi que les blocs uniques qu'on retrouve sur l'ensemble des pages
common: le reset, les r�gles communes au site (body/html, paragraphes, titres...
font: la d�finition des font-family. Pour bien d�crire les font-face, suivre les indications donn�es sur l�article du blog : http://connect.adfab.fr/design/la-police-comment-bien-l-ecrire
var: les variables du site
mixin: les mixins utilis�es.
sprite: pour le cas o� on ne peut pas utiliser de font-icon
layout
header
footer
menu
sidebar
libs
les fichiers css (renomm�s en scss) des diff�rentes librairies, qui n�ont pas pu �tre merg�s via gulp/npm automatiquement. Si on doit les surcharger on ne le fait pas ici mais dans un fichier avec le m�me nom dans le dossier components, pour toujours pouvoir mettre � jour la librairie.
components
Le style des plus petites �l�ments qu'on retrouve sous de nombreuses d�clinaisons sur l'ensemble des pages au niveau "inline": les titres, les boutons, les liens... Ces fichiers servent � d�finir la taille et les effets sur les boutons, les liens, les titres et sous-titres, g�n�ralement communs � l'ensemble des blocs, ne serait-ce que pour la police utilis�e.
button
title
form: le skin g�n�ral des formulaires
libs: un fichier par librairie qui reprend le m�me nom que dans le dossier libs. Chaque fichier contient les surcharges des librairies
blocks
Un fichier pour chaque type de block, reprenant le nom du bloc. On retrouve donc le chemin facilement par rapport � la classe : .text-block sera dans scss/blocks/_text.scss.
Un bloc est une section, une division d'une page. Il peut se retrouver plusieurs fois sur une page et/ou sur plusieurs pages. Chaque section d'une page doit �tre mise dans un bloc.
pages
Un fichier pour chaque page, reprenant l'id de la page, et contenant les surcharges de chaque blocs de la page. Normalement le contenu est assez l�ger, puisque d�fini dans chaque bloc. En th�orie on devrait retrouver les backgound-image qui changent, certaines d�clinaisons de couleurs s�pcifique, surtout sur la home page, g�n�ralement la page la plus sp�cifique d'u site.
Comme pour les blocs on retrouve donc le chemin facilement par rapport � la classe : .home-page sera dans scss/pages/_home.scss.
Variables less/sass
Dans l'id�al, le fichier de var doit �tre le plus d�taill� possible, ce qui permet de changer un param�tre du site juste en changeant une variable. Les couleurs, les hauteurs/largeurs d'�l�ments, les espacements... doivent �tre ici
Les couleurs de base: On liste toutes les couleurs utilis�es avec un nom simple. Si plusieurs variations d'une couleur se retrouvent sur le site on peut utiliser diff�rents suffixes: dark, darker, light, lighter... Si le site contient trop de variation d'une couleur dans les maquettes, s'assurer avec le graphiste qu'elles sont justifi�es. Toutes les couleurs sont d�finies en tant que variables.
Les couleurs des �l�ment. On utilise $text-color pour la couleur g�n�rale du texte du site. On peut retrouver �galement $title-color, $subtitle-color, $link-color... Ces variables ont pour valeur une autre variable de couleur de base, ce qui permet de faire �voluer le site plus facilement et �tre bien plus clair.
La hauteur des �l�ments. Plusieurs �l�ments ont souvent une hauteur fixe: $header-height, $footer-height... Ce qui permet souvent de les r�utiliser vu que d'autres �l�ments se calent par rapport � ceux l� (un sous-menu par exemple). Ainsi en changeant la variable on �vite de tout racalculer.
Ne pas h�siter � ajouter des variables dans les blocs et page pour mieux comprendre l'adh�rence d'un �l�ment sur un autre. Par exemple:
input {
	height: 15px;
	width: calc(100% - 15px);
}
button {
	width: 15px;
	height: 15px;
	line-height: 15px;
}
Dans ce cas on met "15px" dans une variable, ce qui permettra de le modifier plus facilement si besoin, et de mieux comprendre que l'input et le button ont la m�me taille.
Nommage des �l�ments
Le d�coupage a permis de d�terminer les blocs qui sont communs ou sp�cifiques � chaque page.
Chaque bloc est identifi� par une classe:
.my-custom-block pour chaque bloc d'un type. Toujours terminer le nommage par "-block" pour bien identifier les �l�ments. ex: .text-block
.my-custom-block-variation pour les d�clinaisons possibles d'un bloc qu'on retrouve sur plusieurs pages. Cette classe surcharger une ou plusieurs r�gles, mais il faut appliquer la classe de base aux bloc ex: .text-block-bigger, .text-block-left
.my-custom-page pour les pages. On les nomme avec une classe qui se termine syst�matiquement par -page. ex: .home-page
.my-custom-page-my-custom-block pour cibler un bloc sp�cifiquement sur une page pour le surcharger. On doit retrouver le nom de la page et la classe du bloc surcharg�, et �ventuellement le nom du bloc sp�cifique pour le retrouver facilement. ex: .home-page-intro-text-block
Pour les �l�ments � l�int�rieur des blocs, on reprend le nom du bloc, suffix� de notre �l�ment. Par exemple : .header-block-title, .header-block-description�
De cette fa�on dans le scss on n�a pas besoin d�imbriquer les �l�ments dans le bloc, ce qui permet d�avoir un poids tr�s l�ger sur les r�gles css (et ne pas d�passer les 3 niveaux de complexit�, et tr�s facilement les �tendre dans les pages.
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

Produire du code optimis�
L'intention de s�lection
Une sur-qualification des s�lecteurs ressemble � div.promo. Vous obtiendrez s�rement le m�me r�sultat en utilisant simplement .promo
Un autre exemple d'un s�lecteur sur-qualifi� pourrait �tre ul.nav li a {}. Comme ci-dessus, nous pouvons supprimer ul puisque nous savons que .nav est une liste, il est aussi logique que a doit �tre dans un li, donc nous mettre � la di�te ul.nav li a {} pour obtenir simplement .nav a {}.
Au lieu d'utiliser les s�lecteurs pour cibler un �l�ment du DOM, il est souvent pr�f�rable de mettre une classe sur l'�l�ment que vous voulez explicitement styler. Prenons l'exemple pr�cis d'un s�lecteur comme .header ul {} �
Imaginons que ul est en effet le menu principal de notre site Web. il vit dans l'en-t�te et vous pensez que se sera le seul ul en ces lieux ; .header ul {} fonctionnera, mais ce n'est pas id�al ou souhaitable. Ce n'est pas � l'�preuve du temps et certainement pas assez explicite. D�s que nous ajouterons un autre ul pour cet en-t�te il va adopter le style de notre navigation principale. Il y a de grandes chances que ce ne soit pas voulu. Cela signifie que nous devons soit remanier une grande quantit� de codeou annuler beaucoup de styles sur les uls dans ce .header pour supprimer les effets de la s�lection globale.
L'intention de votre s�lecteur doit correspondre � la raison de votre style. Demandez-vous 'Est-ce-que je s�lectionne cela car c'est un ul � l'int�rieur de .header ou parce que c'est la navigation principale de mon site ?'. La r�ponse � cette question permettra de d�terminer votre s�lecteur.
Soyez explicites ; ciblez l'�l�ment que vous voulez modifier, pas son parent. Ne supposez jamais que le balisage ne changera pas. Codez des s�lecteurs qui ciblent ce que vous voulez, pas ce qui se trouve �tre d�j� l�.
Penser CSS 3
En 2016, on ne fait plus que du IE 9+, qui supporte bien le CSS 3 globalement. Par exemple:
:not, pour cibler tous les �l�ments sauf le premier ou le dernier, bien pratique pour mettre un s�parateur entre tous les �l�ments sauf le dernier ou le premier.
calc() pour �viter les margin n�gatifs ou certains calages hasardeux dans la dimension des �l�ments
le centrage d'�l�ments avec les translate(-50%)
mettre les �l�ments graphiques (icones...) dans les ::before ou ::after, pas dans des spans vides.
Pour les navigateurs r�cents on peut faire du flex pour bien aligner des �l�ments ou avoir des tailles harmonieuses, en laissant quand m�me le fallback pour IE 9 si besoin avec les inline-block
Ne jamais mettre de display: table, table-cell ou autre. Ces display sont r�serv�s aux tableaux uniquement. Il existe suffisamment de mani�res de centrer des �l�ments verticalement pour s'en passer. https://css-tricks.com/centering-css-complete-guide/