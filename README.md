# Documentation

## Sommaire

* Convention BEM
* Font-Face
* Pseudo attributs
* REM, EM, %, VW Sizing
* Keyframes
* Responsive, Media queries
* GridLayout
* Flexbox Grid
* Parcel-bundler (installation)
* JavaScript, fonction sympa
* MySQL, créer une base de donnée
* GitHub
* Liens utiles

## Convention BEM

* B -> Block
* E -> Element
* M -> Modifier

```html
<!-- mainList = Block -->
<!-- --xmas = Modifier -->
<ul class="mainList mainList--xmas">
  <!-- __item = Element -->
  <li class="mainList__item">
    <!-- __itemLink = Element -->
    <a class="mainList__itemLink mainList__itemLink--isActive" href="/home">Home</a>
  </li>
  <!-- __item = Element -->
  <li class="mainList__item">
    <!-- __itemLink = Element -->
    <a class="mainList__itemLink" href="/home">About</a>
  </li>
  <!-- __item = Element -->
  <li class="mainList__item">
    <!-- __itemLink = Element -->
    <a class="mainList__itemLink" href="/home">Works</a>
  </li>
</ul>
```

Exemple en SCSS :
```css
.mainList {
  display: flex;
  justify-content: space-between;
  &--xmas {
    background: green;
  }
  &__item {
    list-style: none;
  }
  &__itemLink {
    color: red;
    &--isActive {
      color: white;
    }
  }
}
```

Exemple en CSS du rendu :
```css
.mainList {

}
.mainList--xmas {

}
.mainList__item {

}
.mainList__itemLink {

}
.mainList__itemLink--isActive {

}
```

## Font-Face

Grâce à @font-face on peut utiliser des polices de caractère non-standard, c’est-à-dire
des polices de caractère autre que celles considérée comme étant 100% compatible
à tous les navigateurs pour le web. (Arial, Helvetica, Times New Roman, Times,
Courier, Verdana, etc.).
En permettant aux auteurs de fournir leurs propres polices, il n'est plus nécessaire de
dépendre uniquement des polices qui sont installées sur les postes des utilisateurs.
La règle @font-face peut être utilisée au niveau global d'une feuille de style et
également au sein d'un groupe lié à une règle @ conditionnelle.

Afin d’intégrer une typographie dans un site web, il faut utiliser une police de caractère
True Type (se terminant par l’extension .ttf) ou OpenType (se terminant par l’extension
.otf).
Une fois notre police saisie, il faut la convertir à l’aide d’un générateur tel que Webfont
Font Squirrel.
Il est nécessaire de convertir tous les Polices téléchargé en 4 formats différents
: eot, woff, ttfet svg pour s’assurer qu'il est utilisable pour tous les navigateurs.

Pour finir, dans notre feuille de style .css, à @font-face on renseigne la police utilisé
dans font-family ainsi que le chemin de nos 4 formats de police dans src.

```css
@font-face {
   font-family: "Open Sans Regular";
   src: url("../fonts/OpenSans-Regular.ttf");
}

.message {
   font-family: "Open Sans";
}
```

## Pseudo attributs

Les pseudo attributs `before` et `after` permettent de créer des noeuds HTML en CSS.
Ils sont essentiellement utilisés pour ajouter des ornements, des décorations ... On
peut bien entendu faire des animations avec, les positionner par rapport à leur parent
(relative / absolute). **Ils doivent obligatoirement avoir un `content: ''`**
afin de s'afficher.

```html
<section class="cover">
  <h1 class="cover__mainTitle">Présentation des pseudo-attributs</h1>
</section>
```

```css
.cover {
  background: #FDFDFD;
  padding: 20px;
  &__mainTitle {
    text-align: center;
    font-size: 24px;
    color: green;
    position: relative;
    &::before,
    &::after {
      position:absolute;
      content: '';
      display: block;
      width: 50px;
      height: 50px;
      background: green;
      top: 0;
    }
    &::before {
      left: 0;
    }
    &::after {
      right: 0;
    }
  }
}
```

Les pseudo attributs `first-child`, `last-child` et `nth-child(an+b)` permettent de cibler un élément qui est le premier/dernier/nombre élément fils par rapport à son élément parent.

```html
<nav class="navigation">
  <ul class="mainList">
    <li class="mainList_item">Home</li>
    <li class="mainList_item">Works</li>
    <li class="mainList_item">About</li>
    <li class="mainList_item">Contact</li>
    <li class="mainList_item">Social</li>
  </ul>
</nav>
```

```css
.mainList_item {
  text-decoration : none;
  font-size: 20px;
  color: #000;
  &:first-child {
    color: red;
  }
  &:nth-child(3) {
    color: green;
  }
  &:last-child {
    color: blue;
  }
}
```

## REM, EM, %, VW Sizing

### EM
* Relative à la taille de son parent direct.

```css
.cover {
  font-size: 100%;
  /* 100% = 16px */
  &__mainTitle {
    /* 1em = 16px / .8em =/= 16px */
    font-size: .8em;
  }
}
```

### REM

* Le REM est basé sur la taille de la racine (soit la balise <html>) qui, par défault a une valeur de 16px.
Afin d'éviter tout calcul, il est nécessaire de l'écraser en donnant une base de 10px soit 62.5%.
* Le REM est intéressant à utiliser si les media-queries employées sont en rem également. Cela vous permettra
de garder des proportions égales lorsqu'on va redimensionner la page.
* Ses proportions seront également gardées quand l'utilisateur zoomera dans votre page.

```css
html {
  /* 62.5% === 10px */
  font-size: 62.5%;
}
.mainTitle {
  /* 1.6rem == 16px */
  font-size: 1.6rem;
  /* 32rem === 320px */
  width: 32rem;
}
```

### VW(idth) / VH(ieght)

* Unités relatives à la taille de votre écran (peu importe le device)
* Attention au VH et à son contenu. 100vh === 100vh quoi qu'il arrive.
* VW : très utile pour les interfaces fluides.

## Keyframes animations :

La règle @keyframes permet de définir les étapes qui composent la séquence d'une animation CSS. Cela permet de contrôler une animation plus finement que ce qu'on pourrait obtenir avec les transitions.

```css
.blinking {
   color: #93B7BE;
   -webkit-animation: blinkAnimation 1s infinite;
}

@-webkit-keyframes blinkAnimation {
   0% {
      color: #93B7BE;
   }
   50% {
      color: #000;
   }
   100% {
      color: #93B7BE;
   }
}
```

## Responsive, Media Queries les plus utilisées :

* Sera sur toutes les résolutions
```css
.header {
  height: 400px;
}
```

* Media queries pour mobile
```css
@media (max-width: 480px) {
  /* Affichage sur mobile uniquement */
  .nom-de-class {

  }
}
```

* Media queries pour tablette
```css
@media (max-width: 768px) {
  /* Affichage sur tablette uniquement */
  .nom-de-class {

  }
}
```

* Media queries pour desktop
```css
@media (max-width: 1366px) {
  /* Affichage sur desktop uniquement*/
  .nom-de-class {

  }
}
```

* Media queries pour desktop-large
```css
@media (min-width: 961px) {
  /* Affichage sur desktop-large uniquement*/
  .nom-de-class {

  }
}
```

## GridLayout

Css GridLayout va permettre de positionner les éléments dans la page avec un système de templating.

```html
<div class="container">
  <div class="item item1"></div>
  <div class="item item2"></div>
  <div class="item item3"></div>
  <div class="item item4"></div>
  <div class="item item5"></div>
  <div class="item item6"></div>
</div>
```

Initialiser GridLayout

```css
.container {
  display: grid;
}
```

Définir des lignes, des colonnes et des goutières

```css
.container {
  display: grid;
  grid-template-columns: 150px 150px 150px;
  grid-template-rows: 150px 150px;
  grid-gap: 1rem;
}
```

## Flexbox Grid

* Télécharger [flexboxgrid](http://flexboxgrid.com/) et mettre dans un dossier (.min.css) css avec le style.

* **Ne jamais utilisé de margin ou padding sur les class="col-xxx" quand on utilise une grille**

* col-xs > desktop / col-sm > tablette / col-lg > téléphone etc.
* offset permet de "sauter" des collonnes.

```html
<div class="container">
  <div class="row">

    <div class="col-xs-6 col-lg-4" >
      <h2> Titre 1</h2>
      <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Temporibus fugit eligendi quo quia praesentium. Nam facere, est modi enim corporis perspiciatis, provident cumque.</p>
    </div>

    <div class="col-xs-6 col-lg-4">
      <h2>Titre 2</h2>
      <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Dolore ad provident molestiae reprehenderit explicabo aliquid atque incidunt unde amet.</p>
    </div>

    <div class="col-xs-6 col-lg-4">
      <h2>Titre 3</h2>
      <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Laborum rerum eum, quae voluptatum omnis aut eligendi, placeat ullam suscipit!</p>
    </div>

    <div class="col-xs-6 col-lg-6">
      <h2>Titre 4</h2>
      <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Perferendis, eos aliquam sed quas optio porro architecto doloribus dicta. Rem voluptatibus corporis, molestias eos atque, sint!</p>
    </div>

    <div class="col-xs-12 col-lg-5 col-lg-offset-1">
      <h1>Titre 5</h1>
      <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Deserunt error hic, autem sapiente delectus magni expedita. Eveniet blanditiis quod provident.</p>
    </div>

  </div>
</div>
```


## Parcel-bundler (installation)

Pré requis : node.js

Dans un dossier de dévelloppement, ecrire depuis FastShell :

* mkdir parcel-bundler -> cd parcel-bundler
* npm init
* npm install -g parcel-bundler
* mkdir src -> cd src
* touch index.html index.js
* mkdir styles -> cd styles
* touch styles.scss
* mkdir global && mkdir components && mkdir mixins
* touch global/`_variables.scss` && touch global/`_reset.scss` && touch mixins/`_forsize.scss`
* cd .. -> npm install
* touch .postcssrc
* npm install autoprefixer
* touch .babelrc
* npm install -D babel-preset-env

Pour lancer le serveur :
* npm start


# JavaScript

## Local storage

Pour sauvegarder dans le local storage la variable item :

```js
window.localStorage.setItem("itemName", item);
```

Pour mettre dans la variable item la sauvegarde du local storage :

```js
var item = window.localStorage.getItem("itemName");
```

# MYSQL

Connexion au serveur MySQL :
* mysql -u *USER* root -p *PASSWORD*

Créer une base de donnée :
* CREATE DATABASE *NomDeLaBdD*

Utiliser une base de donnée :
* USE *NomDeLaBdD*

Créer une table :

```mysql
CREATE table `NomDeLaTable`(
`id` INT UNSIGNED NOT NULL AUTO_INCREMENT,
  `page`       varchar(110),
  `title`      varchar(70),
  `h1`         varchar(3000),
  `p`          varchar(100),
  `span-class` varchar(50),
  `span-text`  varchar(100),
  `img-alt`    varchar(2048),
  `img-src`    varchar(30),
  `nav-title`  varchar(100),
  primary key (`page`)
);
```

Afficher une Table :
* DESC *NomDeLaTable*


# GitHub :

Récupérer un repositories :
* git clone https://lien-du-repo.git

Linker son dossier de travail à un répo GitHub :
* git remote add origin (url du github)

**Travailler sur le master est déconseillé, voir interdit selon les projets pour cela utiliser les branchs :**

* git checkout -b (nom de la branch) : créer une nouvelle branch
* git checkout (nom de la branch) : changer de branch

Push un projet sur GitHub :

* git add .
* git commit -m "message"
* git push origin (nom de la branch )

Pull un projet de GitHub :

* git pull origin (nom de la branch)


## Liens utiles :
* [Caniuse](https://caniuse.com/) : "c'est compatible partout ou pas?"
* [FrontEndQuizz](https://github.com/h5bp/Front-end-Developer-Interview-Questions)
* [CssNext](http://cssnext.io/)
* [MDN web docs](https://developer.mozilla.org/fr/)
