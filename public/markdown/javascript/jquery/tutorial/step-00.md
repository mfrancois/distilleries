# 0 - Manipulation de base

- [Content](#doc-content)
- [GIT](#doc-git)
- [IDE](#doc-ide)
- [Mes premiers pas](#doc-ppa)
    - [Hello World !](#doc-hellow)
        - [Etape 1 : Affiche](#doc-affiche)
        - [Etape 2 : Utilisation du DOM](#doc-dom)
        - [Etape 3 : Les évènements](#doc-event)
        - [Etape 4 : Externalisation du code](#doc-ext)
        - [Etape 5 : Initialisation du code suite à l'externalisation](#doc-init)
    - [Tic Tac Toe](#doc-morpion)
        - [Grille](#doc-grille)
        - [Structure javascript et évènements](#doc-struct)
        - [Mécanique de jeux](#doc-meca)
        - [Finitions](#doc-end)
        - [Evolutions](#doc-evol)
 - [Par la suite](#doc-next)

<a name="doc-content"></a>
## Contents
Dans ce tutorial nous allons commencer par l'utilisation de javascript sans librairie ni framework.
Cella vas nous permettrent de voirs quelques notions de bases qu'il ne faut jamais perdres de vue lors de la programmation javascript.
Nous allons voir différentes partie pour l'utilisation du javascript et nous finirons par la création d'un petit jeux simple le Tic Tac Toe.


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

Le dossier step_00 contient les différentes étapes fonctionnel.
Vous pouvez vous en inspirez en cas de soucis particulier.

<a name="doc-ppa"></a>
## Mes premiers pas
Ce tutorial traiteras des manipulations javascript de bases.
Dans cette exercice nous allons voir comment manipuler des éléments du `DOM` et gérer quelques évènements.

<a name="doc-hellow"></a>
### Hello World !

<a name="doc-affiche"></a>
#### Etape 1 : Affiche
Dans le monde de la programmation, nous commençons généralement par l'affichage du mot "Hello World".
Cette convention assez simple permet une utilisation de bases de chaque languages.

Dans un premier temps nous allons juste afficher dans une alert cette phrase.
Pour ce faire ajouter le code suivant  dans la balise body :

    <script type="text/javascript">
        alert('Hello World !');
    </script>

Si vous exécutez la page dans votre navigateur <http://localhost/javascript-tutorial/>, vous devriez voir

<div class="alert alert-warning">
L'utilisation de localhost est possible que si vous avez un serveur local type Uwamp ou Wamp d'installé.
Je vous le conseil car par la suites vous risques d'êtres bloqué par les protocoles de sécurités du navigateur.
</div>

![alert](/markdown/javascript/_images/jquery/tutorial/step_0/alert.jpg)

<div class="alert alert-info">Vous pouvez retrouver le fichier ici https://gist.github.com/mfrancois/9076206#file-etape_1-html</div>

<a name="doc-dom"></a>
#### Etape 2 : Utilisation du DOM
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

<a name="doc-event"></a>
### Etape 3 : Les évènements
Alors qu'es ce qu'un évènement.
C'est très simple un évènement est une action qui déclanche un appel vers une listes de functions.

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

<a name="doc-ext"></a>
### Etape 4 : Externalisation du code
Depuis le début nous plaçons notre code javascript dans le corp de la page html.
Cette technique n'est pas très belle et peut recommandé.
Il faut externaliser le code pour faciliter la lecture et la maintenance.

Pour ce faire rien de plus simple :

* Créez un fichier app.js dans le quel nous mettrons le code javascript.
* Placer le code que vous avez mis entres les balises `<script>` dans ce fichier.
* Placer l'inclusion du fichier dans le head de l'application.


        <script type="text/javascript" src="app.js" ></script>


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

<a name="doc-init"></a>
### Etape 5 : Initialisation du code suite à l'externalisation
Dans l'étape précédente nous avons vus comment externaliser un fichier.
Nous avons vue aussi que cette externalisation rend notre code non fonctionnel.
Pas de panique nous allons voir comment rendre notre code exécutable par le navigateur quand se dernier à compilé le DOM.

Très simplement il faut garder à l'esprit qu'une page html est un enssamble de balises représentant des éléments.
Ces éléments sont compiler par le moteur javascript pour former des noeud c'est ce qu'on appel le DOM.

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

<a name="doc-morpion"></a>
## Tic Tac Toe
Dans cette partie nous allons crée une morpion (Tic Tac Toe de son vrai nom). Vous pouvez le foir en fonctionnement sur la page de démo en ligne <http://fiddle.jshell.net/wQG7a/>.
Avant de commencer il faut réfléchir à quoi nous avons besoins.
Généralement je travail sur papier avant même de coder.

Nous avons besoins de savoir le fonctionnement du mopion.

>Les joueurs inscrivent tour à tour leur symbole sur une grille qui n'a pas de limites ou qui n'a que celles du papier sur lequel on joue. Le premier qui parvient à aligner trois de ses symboles gagne un point.

Nous avons donc besoin :

* Une grille de 3x3.
* De deux symboles `X` et `O`.
* De deux joueurs.

<a name="doc-grille"></a>
### Grille
Nous allons crée la grille.
Pour ce faire je vais utiliser la balise `table` en html.
Je crée donc trois lignes et trois collonnes ce qui donne


    <table id="grid">
        <tr>
            <td></td>
            <td></td>
            <td></td>
        </tr>
        <tr>
            <td></td>
            <td></td>
            <td></td>
        </tr>
        <tr>
            <td></td>
            <td></td>
            <td></td>
        </tr>
    </table>


Le soucis est que vous ne voyais pas forcément le tableau.
Pour le rendre visible je vais ajouter du css entre les balises `head`


            <style>
                table,
                tr,
                td
                {
                    text-align: center;
                    border: 1px solid gray;
                }
                tr{
                    height: 40px;
                }
                td{
                    width: 40px;
                    height: 40px;
                }
            </style>


Vous devriez voir un tableau comme celui qui suit.


![table](/markdown/javascript/_images/jquery/tutorial/step_0/table.jpg)

<a name="doc-struct"></a>
### Structure javascript et évènements

Maintenant que nous avons notre tableau il faut commencer la partie javascript.
Pour ce faire nous allons utiliser les objets en javascript pour éviter que ce soit le fouilli.
Remplacer le contenu de `app.js` par :



    if (typeof dist == "undefined" || !dist) {
        var dist = {};
    }
    if (typeof dist.Game == "undefined" || !dist.Game) {
        dist.Game = {};
    }

    dist.Game.Global = function () {
        this.init();
    };

    // ------------------------------------------------------------------------------------------------
    // ------------------------------------------------------------------------------------------------
    // ------------------------------------------------------------------------------------------------
    // Prototype
    dist.Game.Global.prototype = {



        // --------------------------------------------------------------------------------------------
        init: function () {

        }



    };


    // ------------------------------------------------------------------------------------------------
    // ------------------------------------------------------------------------------------------------
    // ------------------------------------------------------------------------------------------------
    // Run instance
    var app = new dist.Game.Global();


L'intégralité de cette structure est expliqué sur la page [Application (avec jQuery)](/javascript/jquery/default/prototype).
Dans notre cas nous n'utiliserons que la structure mais pas jQuery.

**Par quoi commencer ?**

Tous simplement je commencerais par gérer le cochage des cases.
Pour ce faire nous allons placer un évènement sur le tableau qui détectera l'appuis sur une céllule.

**Pourquoi pas directment sur une cellule ?**

Tout simplement pour éviter de multiplier les évènements.
Si vous placer un évènement par céllule vous aurrais N évènements qui correspondes au nombres de céllule.
Si vous le placez juste sur le tableau vous en aurrais un quoi qu'il arrive.

Ajoutez le code suivant dans la partie prototype  :


        symBole: ['X', 'O'],
        currentPlayer: 1,
        numWin: 3,
        idReset: 'reset',
        idGrid: 'grid',
        idCurrentPlayer: 'currentPlayer',
        finished: false,

        // --------------------------------------------------------------------------------------------
        init: function () {
            window.addEventListener('load', function () {
                app.init_event();
            });
        },

        // --------------------------------------------------------------------------------------------

        init_event: function () {
            document.getElementById(this.idGrid).addEventListener('click', function (event) {
                app.onClick(event);
            });
        },

Paramètres | Fonctionnement
---------- | -------------
symBole | C'est un tableau contenant le symbole pour chaques joueurs
currentPlayer | Permet de déterminer quel joueur doit jouer. En locurence l'index pars de 0 donc l'initialisation à 1 est pour le deuxième joueur.
numWin | Nombres de  symboles nécéssaires pour gagner, comme nous sommes dans un tableau 3x3 la valeure est 3.
idReset | Identifiant du bouton de reset que nous vérons par la suite.
idGrid | Identifiant du tableau
idCurrentPlayer | Identifiant de la zone qui affiche à qui est le tour (que nous vérons par la suite).
finished | Indique si la partie est fini ou non.

init
----
Nous constatont que cette méthode lance l'initialisation des évènements lorsque le DOM est près.

init_event
----------
Attache l'évènement au talbeau, lors du disptache la méthode appelé est `onClick`.



    onClick: function (event) {
            event.preventDefault();
            var elt = event.target;

            if (this.finished) {
                return false;
            }

            if (this.checkValidDom(elt) && elt.tagName.toUpperCase() == 'TD') {
                if (this.isAlreadyUse(elt)) {
                    return false;
                }

                this.check(elt);
            }
        },


onClick
-------
Cette méthode pert dans un premier temps de vérifier si la partie est fini.

* Si c'est le cas il ne se passe rien.
* Sinon on vérifie que l'élément du DOM est valide à l'aide d'une petite méthode implémenté dans l'objet `checkValidDom`.
* Puis on vérifie qu'il sagit bien d'une cellule et qu'elle est vide à l'aide de `isAlreadyUse`.


        checkValidDom: function (domElement) {
            if (typeof(domElement) != 'undefined' && domElement != null) {
                return true;
            }
            return false;
        }


<div class="alert alert-info">Controlle si l'élément n'est pas indéfinie ou null. A garder de côté car on s'en sert souvent en javascript.</div>


Une fois tous ces controles passé on lance le cochage de la case à l'aide de `check`.


isAlreadyUse
------------
Controle juste si l'élément est vide ou non pour donner la possibiliter de le remplir.

    isAlreadyUse: function (elt) {

        if (this.checkValidDom(elt) && elt.innerHTML != '') {
            return true;
        }

        return false;
    },



check
-----
Cette méthode remplis à l'aide du symbole associé au joueur et lance la méthode qui permet de savoir si on à gagné.
Sinon c'est au joueur suivant.

    check: function (elt) {
        if (this.checkValidDom(elt) === false) {
            return false;
        }
        elt.innerHTML = this.symBole[this.currentPlayer];

        if (this.isWinGame()) {
            this.finished = true;
            alert('Player ' + (this.currentPlayer + 1) + ' wins !!!');
        } else {
            this.nextPlayer();
        }

    },



<a name="doc-meca"></a>
### Mécanique de jeux
Avant de continuer à vous décrire les méthodes.
Je vous invites à prendre du temps pour réfléchir à comment vous allez détecter qu'une grille est gagnante.
Habituellement c'est simple mais d'un point de vue informations il faut coder les scénarios de victoire.

Pour ce faire il faut garder à l'esprit qu'un morpion est juste un tableau avec des coordonnées pour chaqu'un des cases.
Pour m'aider à coder les scénarios de  victoire de schématise les coordonées.

![table_space](/markdown/javascript/_images/jquery/tutorial/step_0/table_space.jpg)

Comme vous pouvez le voir chaqu'une des coordinées est représenté par X:Y.

Maintenant listons les cas de victoires  :

* Quand une ligne est pleines de votre symbole.
* Quand une colone est pleines de votre symbole.
* Quand une diagonale est pleines de votre symbole.

Dans la méthode `isWinGame` nous allons faire appel à trois méthodes. Une méthode pour les lignes, une méthode pour les colonnes et une pour la diagonale.


    isWinGame: function () {
        var table = document.getElementById(this.idGrid);
        var lines = table.getElementsByTagName('TR');

        if (this.isWinLines(lines)) {
            return true;
        }
        if (this.isWineCols(lines)) {
            return true;
        }
        if (this.isWinDiagonal(lines)) {
            return true;
        }
        return false;
    },


isWinLines
----------


    isWinLines: function (lines) {
        if (this.checkValidDom(lines) === false) {
            return false;
        }

        for (var i = 0; i < lines.length; i++) {
            if (this.isWinLine(lines[i])) {
                return true;
            }
        }

        return false;
    },

    isWinLine: function (line) {
        if (this.checkValidDom(line) === false) {
            return false;
        }

        var col = line.getElementsByTagName('TD');
        for (var i = 0; i < col.length; i++) {
            if (col[i].innerHTML != this.symBole[this.currentPlayer]) {
                return false;
            }
        }

        return true;
    },

Nous allons boucler sur chaques lignes, par ligne nous allons controller chaques colonnes et vérifier qu'il contient notre symbole.
Si ce n'est pas le cas on retourn false.

    0:0
    0:1
    0:2

    1:0
    1:1
    1:2

    2:0
    2:1
    2:3


isWineCols
----------


     isWineCols: function (lines) {
        for (var col = 0; col < this.numWin; col++) {
            var isSame = true;

            for (var i = 0; i < lines.length; i++) {
                var cols = lines[i].getElementsByTagName('TD');
                if (cols[col].innerHTML != this.symBole[this.currentPlayer]) {
                    isSame = false;
                    break;
                }
            }

            if (isSame === true) {
                return isSame;
            }
        }

        return false;
    },

Cette fois il faut parcourir colonne par colonne pour déterminer que les symboles sont celui du joueur courrent.
Ce qui signifie que l'ordre d'exécution est :

    0:0
    1:0
    2:0

    0:1
    1:1
    2:1

    0:2
    1:2
    1:2


isWinDiagonal
------------


    isWinDiagonal: function (lines) {
        for (var col = 0; col < this.numWin; col++) {
            var cols = lines[col].getElementsByTagName('TD');
            if (cols[col].innerHTML != this.symBole[this.currentPlayer]) {
                return false;
            }
        }
        return true;
    },


Cette méthode parcour la diagonale du tableau pour déterminer si tous les symbile son celui du joueur courrent.
L'ordre d'éxécution donne :

    0:0
    1:1
    2:2


<a name="doc-end"></a>
### Finitions
Une fois la mécanique de jeux en place vous êtres presques opérationnel.
Il ne vous manque plus qu'a faire une victoire et un reset.



Dans le fichier app.js
----------------------

    onReset: function (event) {
        var table = document.getElementById(this.idGrid);
        var lines = table.getElementsByTagName('TR');

        for (var i = 0; i < lines.length; i++) {
            var cols = lines[i].getElementsByTagName('TD');
            for (var j = 0; j < cols.length; j++) {
                cols[j].innerHTML = '';
            }
        }

        this.currentPlayer = 1;
        this.nextPlayer();
    },


    check: function (elt) {
            if (this.checkValidDom(elt) === false) {
                return false;
            }
            elt.innerHTML = this.symBole[this.currentPlayer];

            if (this.isWinGame()) {
                this.finished = true;
                alert('Player ' + (this.currentPlayer + 1) + ' wins !!!');
            } else {
                this.nextPlayer();
            }

    },



Dans le html
------------

    <table id="grid">
        <tr>
            <td></td>
            <td></td>
            <td></td>
        </tr>
        <tr>
            <td></td>
            <td></td>
            <td></td>
        </tr>
        <tr>
            <td></td>
            <td></td>
            <td></td>
        </tr>
    </table>
    <div>
        <button id="reset" value="reset">Restart</button>
        <span id="currentPlayer">&nbsp;</span>
    </div>


<a name="doc-evol"></a>
### Evolutions
Vous avez maintenant les connaissances pour ajouter les fonctionalités que vous voulez.
Vous pouvez par exemple faire une suivit des scores, ajouter des couleurs par joueur ou même agrandire la zone de jeux.


<a name="doc-next"></a>
## Par la suite
Dans un prochain totorial nous allons voir ce même jeux mais cette fois si avec jQuery.
Si je le javascript pure et dure vous interesse je vous concoterais un résolveur de Sudoku.
