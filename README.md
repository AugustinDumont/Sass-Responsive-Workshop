# Sass-Responsive Workshop by Augustin Dumont

## A propos : 

Ce workshop est réalisé dans le cadre d'une formation réalisée @ BeCode. 
Il est basé et construit autour d'un cours UDEMY réalisé par Jonas Schmedtmann et intitulé "Advanced CSS and Sass : Flexbox, Grid, Animations and More!". A tous ceux et celles qui souhaitent améliorer leurs compétences en HTML, CSS, SASS, je le recommande vivement. 

Je compte vous partager ce que j'en ai retenu en réalisant un One Page design et responsive. 

Dans le repository, sont à dispositions : 

- Le fichier JSON avec différentes dependencies
- Les fichiers de bases, pré-complétés et organisés = file_starter
- Les fichiers avec le résultat escompté = file_finish
- Les différentes images utilisées

Bonne lecture ! 

## Objectifs :

### Sass / Scss

- Avoir une meilleure compréhension de Sass et plus particulièrement Scss. 
- Comment organiser l'architecture de ses fichiers? 
- Comment utiliser les fonctionnalités variables, mixins, imports, ect?
- Comment utiliser l'indentation BEM?

### Responsive design

- Media queries
- Mobile first VS Desktop first
- Responsive images CSS
- Responsive images HTML
- Supports
- Média

### Tricks and tips

- Comment customiser un contact form?

***


## I. INSTALLATION ET INTRODUCTION

$ npm install

## package.json

### Depedencies : 

- node-sass : compiler scss vers css dans style.css
- autoprefixer, postcss-cli : ajoute tous les préfixs nécessaires (ex :-webkit)
- concat : concater le code lors du build
- npm-run-all : to run multiple script lors du build

Avant de commencer à travailler : $ npm run watch:sass

Avant de déployer en ligne : $ npm run build:css 

Cette seconde commande à utiliser en fin de développer va compiler le code, concataner, compresser et ajouter tous les préfixs nécessaires. 

## II. ARCHITECTURE DES DOSSIERS ET FICHIERS

Comme indiquer précédemment, nous allons compiler du SCSS vers du CSS. Plus précisément, c'est notre fichier mains.scss qui sera compilé vers le fichier style.css. C'est ce dernier qui sera ensuite analysé lors de la lecture du script traditionnel 

```
<link rel="stylesheet" href="css/style.css">
```

présent dans le <head> de notre index.html. 

L'architecture SCSS permet de décomposer le code scss de notre projet. 

Avantages : lisibilité, organisation, réutilisation, transmission de code. 

Comme vous pouvez le voir, nous retrouvons différents dossiers, avec différents fichiers dont chacun est importé dans le fichier parent main.scss.

Remarque : les fichiers importés commence tous par un underscore. 

### PRESENTATION DES DIFFERENTS DOSSIERS ET FICHIERS

### ABSTRACTS FILE: 
Fait référence aux outils Sass : variables, fonctions, mixins et autre fichiers de configuration, etc. qui seront utilisés dans les autres fichiers .scss

>_functions.scss

>_mixins.scss

>_variable.scss


### BASE FILE: 
Contient le code passe-partout du projet. Y compris les styles standard tels que les réinitialisations et les règles typographiques, qui sont couramment utilisés tout au long de votre projet.

>_animations.scss

>_base.scss

>_grid.scss

>_typography.scss

>_utilities.scss


### COMPONENTS FILE: 
Contient tous vos styles de boutons, carrousels, curseurs et composants de page similaires (pensez aux widgets). Votre projet contiendra généralement un grand nombre de fichiers de composants - car l'ensemble du site / de l'application doit être principalement composé de petits modules.


>_button.scss

>_form.scss

>_popup.scss


### LAYOUT FILE: 
Contient tous les styles impliqués dans la mise en page de votre projet. Tels que les styles pour votre en-tête, pied de page, navigation et le système de grille


>_footer.scss

>_header.scss

>_navigation.scss


### PAGE FILE: 
 Tous les styles spécifiques aux pages individuelles seront placés ici. Par exemple, il n'est pas rare que la page d'accueil de votre site nécessite des styles spécifiques à une page qu'aucune autre page ne reçoit.


>_home.scss

>_other_page.scss

[Plus d'infos à ce sujet, cliquez ici](https://itnext.io/structuring-your-sass-projects-c8d41fa55ed4)



***

## II. RAPPEL SUR LES DIFFERENTES UNITES DE MESURE

Utiliser des unités de mesure relatives est primoridal pour l'adaptation responsive de notre design. 

- vh / vw
- % 
- em (obtained from current or parent fontsize)
- rem (obtained from root fontsize)
- px

Par défaut, notre root font-size = 100% = 16px et par conséquent, 1rem = 16px. 
En modifiant la font-size dans notre balise html à 62,5%, notre root font-size sera = à 10px et 1rem = 10px. 


```
html {
    // This defines what 1rem is
    font-size: 62.5%; //1 rem = 10px; 10px/16px = 62.5%

    @include respond(tab-land) { // width < 1200?
        font-size: 56.25%; //1 rem = 9px, 9/16 = 50%
    }

    @include respond(tab-port) { // width < 900?
        font-size: 50%; //1 rem = 8px, 8/16 = 50%
    }
    
    @include respond(big-desktop) {
        font-size: 75%; //1rem = 12, 12/16
    }
}
```

En préférant l'utilisation des rem aux px, il nous suffira de modifier la valeur de notre root font, pour modifier l'ensemble des unités utilisées dans notre code et ce, de manière proportionnelle ! 

***

## C'EST PARTI !

L'installation et l'introduction sont terminées, c'est parti ! 

Voici un aperçu de l'ensemble des modifications apportées dans différents fichiers. Il vous suffit de comparer les fichier _starter et _ finish pour voir les différents ajouts. 

N'oubiez pas de lancer le compilateur dans votre terminal en vous situant à la racine de votre projet: 

$ npm run watch:sass

***


## 1. HEADER

Comment rendre des images responsives directement dans le CSS?

Vous conviendrez qu'il n'est pas nécessaire de charger une image qui fait plus de 2000px pour un device dont la taille de l'écran est inférieure. 

A l'inverse, quand la résolution de l'écran le permet, pourquoi se priver d'afficher une image haute résolution? 

Ouvrez le fichier _header_starter.scss

1. Pourquoi utiliser des vh? 
2. Ajout du -webkit pour le clip-path
3. Ajout du @supports pour le clip-path
4. Ajout du @media pour adapter la résolution de l'image en fonction de la taille et/ou de la résolution de l'écran.

***

## 2. FOOTER

Comment rendre des images responsives directement dans le HTML?

Ouvrez le fichier index_starter.html

Comme vous pouvez le constater, nous avons une baliser < img > assez traditionnelle. 
Celle-ci ne permet pas beaucoup de flexibilité et ne s'adaptera aux nécessités du design ou du device. 

```
<img class="footer_image src="img/logo-white.png" alt="logo">
```

Voyons voir quels autres éléments HTML nous pouvons utiliser pour faire face à cette problématique. 


- L'élément HTML < picture >

L'élément HTML < picture > est un conteneur utilisé afin de définir zéro ou plusieurs éléments < source > destinés à un élément < img >. **Le navigateur choisira la source la plus pertinente** selon la disposition de la page (les contraintes qui s'appliquent à la boîte dans laquelle l'image devra être affichée), selon l'appareil utilisé (la densité de pixels de l'affichage par exemple avec les appareils hiDPI) et selon les formats pris en charge (ex. WebP pour les navigateurs Chromium ou PNG pour les autres). Si aucune correspondance n'est trouvée parmi les éléments < source >, c'est le fichier défini par l'attribut src de l'élément < img > qui sera utilisé.

- L'élement HTML < source >

L'élément HTML < source > définit différentes ressources média pour un élément < picture >, < audio > ou < video >. C'est un élément vide : il ne possède pas de contenu et ne nécessite pas de balise fermante. Il est généralement utilisé pour distribuer le même contenu en utilisant les différents formats pris en charge par les différents navigateurs (media queries).

Avec l'élément < picture >, **il faut toujours inclure un élément < img > comme image de secours**, avec un attribut alt qui garantit une certaine accessibilité.


- L'attribut srcset

**L'attribut srcset permet de définir une image adaptée au terminal de consultation en ciblant la taille de l'écran, et également la densité de pixels.** 

Au sein de cet attribut srcset, les spécifications prévoient deux types de descripteurs permettant de conditionner le chargement des ressources :

le descripteur "x" sélectionne l'image en fonction de la densité de pixel (pixel ratio) de l'écran. 

Le descripteur "w" sélectionne l'image en fonction de sa taille et de l'adéquation à la surface de l'écran. 

Si nous désirons changer l'image en fonction d'un format mobile ou desktop et adapter la résolution à l'écran de l'utilisateur, voila le code qu'il est préférable d'utiliser. 

```
<picture class="footer__logo">
    <source srcset="img/logo-white-small-1x.png 1x, img/logo-white-small-2x.png 2x" media="(max-width: 37.5em)">
        <img srcset="img/logo-white-1x.png 1x, img/logo-white-2x.png 2x" alt="Full logo" src="img/logo-white-2x.png">
</picture>
```



## 3. ABOUT

Dans le footer, nous avons utilisé le descripteur "x" afin d'indiquer les différentes images mises à disposition pour le navigateur. 

Ici, nous utiliserons l'indicateur "w". 

1. Indiquer les deux images à disposition + leur taille. 300w = 300px et 1000w = 1000px
2. Calculer le ratio de la taille de chaque image en fonction de nos différents breakpoints

    - max-width: 900px ou 56.25em   152px / 900px = 17vw
    - max-width: 600px ou 37.5em   152px / 600px = 25vw
    - autre devices : 300px

3. Faites le test en simulant le changement de résolution dans votre inspecteur et observer la "current source" de l'image. S'il est préférable de choisir l'image supérieure à 300px, le navigateur le fera. 

```
<img srcset="img/nat-1.jpg 300w, img/nat-1-large.jpg 1000w"
        sizes="(max-width: 56.25em) 17vw, (max-width: 37.5em) 25vw, 300px" alt="Photo 1"
        class="composition__photo composition__photo--p1" src="img/nat-1-large.jpg">

<img srcset="img/nat-2.jpg 300w, img/nat-2-large.jpg 1000w"
        sizes="(max-width: 56.25em) 17vw, (max-width: 37.5em) 25vw, 300px" alt="Photo 2"
        class="composition__photo composition__photo--p2" src="img/nat-2-large.jpg">

<img srcset="img/nat-3.jpg 300w, img/nat-3-large.jpg 1000w"
        sizes="(max-width: 56.25em) 17vw, (max-width: 37.5em) 25vw, 300px" alt="Photo 3"
        class="composition__photo composition__photo--p3" src="img/nat-3-large.jpg">
```

























