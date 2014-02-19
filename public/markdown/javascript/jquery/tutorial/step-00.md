# 0 - Manipulation de base

- [Content](#doc-content)
- [GIT](#doc-git)
- [IDE](#doc-ide)
- [Mes premiers pas](#doc-ppa)
- [Configuration](#doc-config)

<a name="doc-content"></a>
## Contents

Tout au long de ce tutorial vous allez être amené à récupérer divers branches.
Je vous invite à crée une copie du repository pour travailler et une copie pour suivre les explications.


<div class="alert alert-info">
Au long de ce premier tutorial j'utilise des fonctions qui fontionne sur des navigateurs récent. Je ne m'occupe pas de la rétrocompatibilité pour éviter de trop surcharger le code.
</div>


<a name="doc-git"></a>
## GIT

Dans un premier temps vous devez récupérer le projet.
Pour ce faire il vous suffit de taper a commande suivante

    git clone -v --recurse-submodules --progress --branch tutorial/step_00 "https://github.com/mfrancois/javascript-tutorial.git"

Une fois fini vous devriez avoir votre projet sur la branche `tutorial/step_00`.

<a name="doc-ide"></a>
## IDE

A présent ouvrez le projet dans votre IDE favori (pour ma part PhpStorm).
Une fois le projet ouvert vous devriez avoir une arborescence comme ceci :


![IDE](/markdown/javascript/_images/jquery/tutorial/step_0/ide.jpg)

<a name="doc-ppa"></a>
## Mes premiers pas
Ce tutorial traiteras des manipulations javascript de bases.
Dans cette exercice nous allons voir comment manipuler des éléments du `DOM` et gérer quelques évènements.

### Hello Worl !

#### Etape 1
Dans le monde de la programmation, nous commençons généralement par l'affichage du mot "Hello World".
Cette convention assez simple permet une utilisation de bases de chaque languages.

Dans un premier temps nous allons juste afficher dans une alert cette phrase.
Pour ce faire ajouter le code suivant  dans la balise body :

    <script type="text/javascript">
        alert('Hello World !');
    </script>

Si vous exécutez la page dans votre navigateur <http://localhost/javascript-tutorial/>, vous devriez voir

![alert](/markdown/javascript/_images/jquery/tutorial/step_0/alert.jpg)

<div class="alert alert-info">Vous pouvez retrouver le fichier ici https://gist.github.com/mfrancois/9076206#file-etape_1-html</div>

#### Etape 2
Maintenant que vous affichez des alerts nous allons voir comment injecter cette phrase dans le contenue de votre page.
Pour ce faire nous allons écrire le code javascript qui écrira dans un div cette phrase.
Pour ce faire ajouter la balise suivant entre la balise body :

    <div id="hello"></div>

En dessous de ce dernier ajoutez le javascript qui inject la phrase :

    <script type="text/javascript">
        document.getElementById('hello').innerHTML = "Hello World !";
    </script>


![innerhtml](/markdown/javascript/_images/jquery/tutorial/step_0/innerhtml.jpg)


`document` est l'objet qui content le html de votre page. Il existe plusieurs objets de bases les deux plus courrent concernant la page est `window` et `document`.
L'objet `window` représente la fenêtre de votre navigateur.
Pour résupérer des éléments de vote HTML vous possédé une batterie de selecteurs.
Cellui utilisé ici est `document.getElementById`. Il retourne l'élément du DOM qui à pour attribut `id` correspondant au paramètre. Dans notre cas le `id="hello"`.


 Il existent d'autres selecteur comme :

 Selecteur | Résultat
 ---------- | ---------
 `document.getElementById` | Retourne l'élément DOM par rapport à son identifiant.
 `document.getElementsByClassName` | Retourne les éléments par rapport à leurs classes.
 `document.getElementsByTagName` | Retourne les éléments par rapport à leur type (ex : div, input, p, span).


Pour finir l'attribut `innerHTML` permet de récupérer, ou d'initiliser, le contenu html d'un élément du DOM.
Dans notre cas nous nous en servons pour injecter le contenu de la chaine dans la div.

<div class="alert alert-info">Vous pouvez retrouver le fichier ici https://gist.github.com/mfrancois/9076206#file-etape_2-html</div>

### Etape 3
Maintenant nous allons voir les évènements.
Alors qu'es ce qu'un évènement. C'est très simple un évènement est une action qui déclanche un appel vers une listes de functions.

Vous me direz qu'elle est l'utilité ? Simplement détecter quand un utilisateur tape sur son clavier, ou alors quand il clique sur un élément ou même s'il redimentionne son navigateur.
Il faut garder à l'esprit que le javascript est un language client et donc il permet d'intéragir avec lui.

Nous allons éssayer de capter le clique sur notre élément Hello World et au click changer le background de ce dernier.

     document.getElementById('hello').addEventListener('click',function(event){
        event.preventDefault();
        event.target.style.backgroundColor = "#00FFFF";

    });

Toujours pareil nous récupérons l'élément dans le DOM, cette fois nous utilisons `addEventListener`.
Cette fonction permet d'attacher des évènement à un objet et d'associer une fonction à cette évènement.
Dans notre cas nous attachons une fonction dite annonyme.

> Les fonctions anonymes sont des fonctions n'ayant pas de nom.
Parce que ces fonctions n'ont pas de nom, à l'endroit où l'on voudrait mettre leur nom, on trouve directement les instructions définissant la fonction introduites par une syntaxe particulière.

Etudions le contenu de la fonction.

    event.preventDefault();

Cette ligne permet d'empécher la propagation de l'évènement click plus loins.
Très pratique quand vous utiliser des évènements de click sur des liens.


    event.target.style.backgroundColor = "#00FFFF";

Permet de changer la couleur d'arrière plans sur un élément du DOM.
Pour avoir plus d'informations sur les informations contenu dans `style`, je vous invite à aller sur <http://www.w3schools.com/jsref/dom_obj_style.asp>

#### Avant le click
![avant](/markdown/javascript/_images/jquery/tutorial/step_0/innerhtml.jpg)

#### Après le click
![apres](/markdown/javascript/_images/jquery/tutorial/step_0/click.jpg)


<div class="alert alert-info">Vous pouvez retrouver le fichier ici https://gist.github.com/mfrancois/9076206#file-etape_3-html</div>


### Etape 4
Depuis le début nous plaçons notre code javascript dans le corp de la page html.
Cette technique n'est pas très belle et peut recommandé.
Il faut externaliser le code pour faciliter la lecture et la maintenance.

Pour ce faire rien de plus simple :

* Créez un fichier app.js dans le quel nous mettrons le code javascript.
* Placer le code que vous avez mis entres les balises `<script>` dans ce fichier.
* Placer l'inclusion du fichier dans le head de l'application.


        <script type="text/javascript" src="app.js" />


Vous devez vous retrouver avec deux fichier l'un qui ressamble à


    <!DOCTYPE html>
    <html>
    <head>
        <title>Tutorial Javascript</title>
        <script type="text/javascript" src="app.js" ></script>
    </head>
    <body>
    <div id="hello"></div>
    <script type="text/javascript">
    </script>

    </body>
    </html>


<div class="alert alert-info">Vous pouvez retrouver le fichier ici https://gist.github.com/mfrancois/9076206#file-etape_4-html</div>



Et l'autre qui ressamble à

    document.getElementById('hello').innerHTML = "Hello World !";
    document.getElementById('hello').addEventListener('click',function(event){
        event.preventDefault();
        event.target.style.backgroundColor = "#00FFFF";

    });


<div class="alert alert-info">Vous pouvez retrouver le fichier ici https://gist.github.com/mfrancois/9076206#file-app_etape_4-js</div>


Là vous me dites mais rien ne s'affiche.
Ne paniquez pas c'est tout à fait normal.
Comme nous manipulons le DOM mais que ce dernier n'est pas construit rien ne s'affiche puisqu'il ne trouve pas le div.

Pour faire fonctionner ce code je vous invite à aller faire l'étape 5

### Etape 5
Dans l'étape précédente nous avons vus comment externaliser un fichier.
Nous avons vue aussi que cette externalisation rend notre code non fonctionnel.
Pas de panique nous allons voir comment rendre notre code exécutable par le navigateur quand se dernier à compilé le DOM.

Très simplement il faut garder à l'esprit qu'une page html est un enssamble de balises représentant des éléments.
Ces éléments sont compiler par le moteur javascript pour former des noeud c'est ce qu'on appel le DOM

>Le Document Object Model (ou DOM) est un standard du W3C qui décrit une interface indépendante de tout langage de programmation et de toute plate-forme, permettant à des programmes informatiques et à des scripts d'accéder ou de mettre à jour le contenu, la structure ou le style de documents XML et HTML1. Le document peut ensuite être traité et les résultats de ces traitements peuvent être réincorporés dans le document tel qu'il sera présenté.

Pour déclancher notre code au bon moment il suffit découter un évènement pariculié.
Nous allons ajouter un écouteur sur l'objet window, pour comprendre cette évènement je vous invite à regarder cette page <http://www.w3schools.com/jsref/event_onload.asp>.


        window.addEventListener('load',function(){
            document.getElementById('hello').innerHTML = "Hello World !";
            document.getElementById('hello').addEventListener('click', function (event) {
                event.preventDefault();
                event.target.style.backgroundColor = "#00FFFF";

            });
        });


Cette évènement déclanche l'éxécution du code lorsque le DOM est prèt.
Il n'est pas spécifique à l'objet `window`, il peut marcher sur d'autres éléments comme :

* `body`
* `frame`
* `frameset`
* `iframe`
* `img`
* `input type="image"`
* `link`
* `script`
* `style`


<div class="alert alert-info">Vous pouvez retrouver le fichier ici https://gist.github.com/mfrancois/9076206#file-app_etape_5-js</div>




### Etape 6
Morpion




