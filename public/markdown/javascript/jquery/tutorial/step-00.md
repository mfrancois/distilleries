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
Cela va nous permettre de voir quelques notions de base qu'il ne faut jamais perdre de vue lors de la programmation javascript.
Nous allons voir différentes parties pour l'utilisation du javascript et nous finirons par la création d'un petit jeu simple le Tic Tac Toe.


Tout au long de ce tutorial vous allez être amenés à récupérer diverses branches.
Je vous invite à créer une copie du repository pour travailler et une copie pour suivre les explications.

<div class="alert alert-info">
Au long de ce premier tutorial j'utilise des fonctions qui fontionnent sur des navigateurs récents. Je ne m'occupe pas de la rétrocompatibilité pour éviter de trop surcharger le code.
</div>


<a name="doc-git"></a>
## GIT

Dans un premier temps vous devez récupérer le projet.
Pour se faire il vous suffit de taper la commande suivante

    git clone -v --recurse-submodules --progress --branch tutorial/step_00 "https://github.com/mfrancois/javascript-tutorial.git"

Une fois fini vous devriez avoir votre projet sur la branche `tutorial/step_00`.

<a name="doc-ide"></a>
## IDE

A présent, ouvrez le projet dans votre IDE favori (pour ma part PhpStorm).
Une fois le projet ouvert vous devriez avoir une arborescence comme ceci :


![IDE](/markdown/javascript/_images/jquery/tutorial/step_0/ide.jpg)

Le dossier step_00 contient les différentes étapes fonctionnelles.
Vous pouvez vous en inspirez en cas de souci particulier.

<a name="doc-ppa"></a>
## Mes premiers pas
Ce tutorial traiteras des manipulations javascript de base.
Dans cet exercice nous allons voir comment manipuler des éléments du `DOM` et gérer quelques évènements.

<a name="doc-hellow"></a>
### Hello World !

<a name="doc-affiche"></a>
#### Etape 1 : Affiche
Dans le monde de la programmation, nous commençons généralement par l'affichage du mot "Hello World".
Cette convention assez simple permet une utilisation de base de chaque langage.

Dans un premier temps, nous allons juste afficher cette phrase "Hello World" dans une alerte.
Pour se faire; ajoutez le code suivant dans la balise body :

    <script type="text/javascript">
        alert('Hello World !');
    </script>

Si vous exécutez la page dans votre navigateur <http://localhost/javascript-tutorial/>, vous devriez voir

<div class="alert alert-warning">
L'utilisation de localhost n'est possible que si vous avez un serveur local type Uwamp ou Wamp d'installé.
Je vous le conseil car par la suite, vous risquez d'être bloqués par les protocoles de sécurité du navigateur.
</div>

![alert](/markdown/javascript/_images/jquery/tutorial/step_0/alert.jpg)

<div class="alert alert-info">Vous pouvez retrouver le fichier ici https://gist.github.com/mfrancois/9076206#file-etape_1-html</div>

<a name="doc-dom"></a>
#### Etape 2 : Utilisation du DOM
Maintenant que vous affichez des alertes, nous allons voir comment injecter cette phrase dans le contenu de votre page.
Nous allons écrire le code javascript qui écrira cette phrase dans un div.
Pour se faire, ajoutez la balise suivante entre la balise body :

    <div id="hello"></div>

En dessous de ce dernier ajoutez le javascript qui injecte la phrase :

    <script type="text/javascript">
        document.getElementById('hello').innerHTML = "Hello World !";
    </script>


![innerhtml](/markdown/javascript/_images/jquery/tutorial/step_0/innerhtml.jpg)


Il existe plusieurs objets de base, les deux plus courants concernant la page sont `window` et `document`.
`document` est l'objet qui contient le html de votre page.
L'objet `window` représente la fenêtre de votre navigateur.
Pour récupérer des éléments de vote HTML, vous possédez une batterie de selecteurs.
Celui utilisé ici est `document.getElementById`. Il retourne l'élément du DOM qui à pour attribut `id` correspondant au paramètre. Dans notre cas le `id="hello"`.


 Il existent d'autres selecteurs comme :

 Selecteur | Résultat
 ---------- | ---------
 `document.getElementById` | Retourne l'élément DOM par rapport à son identifiant.
 `document.getElementsByClassName` | Retourne les éléments par rapport à leurs classes.
 `document.getElementsByTagName` | Retourne les éléments par rapport à leurs types (ex : div, input, p, span).


Pour finir l'attribut `innerHTML` permet de récupérer, ou d'initialiser, le contenu html d'un élément du DOM.
Dans notre cas, nous nous en servons pour injecter le contenu de la chaîne dans la div.

<div class="alert alert-info">Vous pouvez retrouver le fichier ici https://gist.github.com/mfrancois/9076206#file-etape_2-html</div>

<a name="doc-event"></a>
### Etape 3 : Les évènements
Alors qu'est ce qu'un évènement.
C'est très simple, un évènement est une action qui déclanche un appel vers une liste de fonction.

Vous me direz qu'elle est l'utilité ? Simplement détecter quand un utilisateur tape sur son clavier, ou alors quand il clique sur un élément ou même s'il redimentionne son navigateur.
Il faut garder à l'esprit que le javascript est un langage client et donc il permet d'intéragir avec lui.

Nous allons essayer de capter le clic sur notre élément "Hello World" et de changer le background de l'élément lors du clic.

     document.getElementById('hello').addEventListener('click',function(event){
        event.preventDefault();
        event.target.style.backgroundColor = "#00FFFF";

    });

Toujours pareil, nous récupérons l'élément dans le DOM, cette fois nous utilisons `addEventListener`.
Cette fonction permet d'attacher des évènements à un objet et d'associer une fonction à cet évènement.
Dans notre cas, nous attachons une fonction dite anonyme.

> Les fonctions anonymes sont des fonctions n'ayant pas de nom.
Parce que ces fonctions n'ont pas de nom, à l'endroit où l'on voudrait mettre leur nom, on trouve directement les instructions définissant la fonction introduites par une syntaxe particulière.

Etudions le contenu de la fonction.

    event.preventDefault();

Cette ligne permet d'empécher la propagation de l'évènement "click" plus loins.
Très pratique quand vous utilisez des évènements de "click" sur des liens.


    event.target.style.backgroundColor = "#00FFFF";

Permet de changer la couleur d'arrière plan sur un élément du DOM.
Pour avoir plus de details sur les informations contenu dans `style`, je vous invite à aller sur <http://www.w3schools.com/jsref/dom_obj_style.asp>

#### Avant le click
![avant](/markdown/javascript/_images/jquery/tutorial/step_0/innerhtml.jpg)

#### Après le click
![apres](/markdown/javascript/_images/jquery/tutorial/step_0/click.jpg)


<div class="alert alert-info">Vous pouvez retrouver le fichier ici https://gist.github.com/mfrancois/9076206#file-etape_3-html</div>

<a name="doc-ext"></a>
### Etape 4 : Externalisation du code
Depuis le début nous plaçons notre code javascript dans le corps de la page html.
Cette technique n'est pas très belle et peu recommandée.
Il faut externaliser le code pour faciliter la lecture et la maintenance.

Pour se faire, rien de plus simple :

* Créez un fichier app.js dans lequel nous mettrons le code javascript.
* Placer le code que vous avez mis entre les balises `<script>` dans ce fichier.
* Placer l'inclusion du fichier dans le head de l'application.


        <script type="text/javascript" src="app.js" ></script>


Vous devez vous retrouver avec deux fichiers; l'un qui ressemble à


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



Et l'autre qui ressemble à

    document.getElementById('hello').innerHTML = "Hello World !";
    document.getElementById('hello').addEventListener('click',function(event){
        event.preventDefault();
        event.target.style.backgroundColor = "#00FFFF";

    });


<div class="alert alert-info">Vous pouvez retrouver le fichier ici https://gist.github.com/mfrancois/9076206#file-app_etape_4-js</div>


Là vous me dites que rien ne s'affiche.
Ne paniquez pas, c'est tout à fait normal.
Comme nous manipulons le DOM mais que ce dernier n'est pas construit, rien ne s'affiche puisqu'il ne trouve pas le div.

Pour faire fonctionner ce code je vous invite à aller faire l'étape 5

<a name="doc-init"></a>
### Etape 5 : Initialisation du code suite à l'externalisation
Dans l'étape précédente nous avons vu comment externaliser un fichier.
Nous avons vu aussi que cette externalisation rend notre code non fonctionnel.
Pas de panique, nous allons voir comment rendre notre code exécutable par le navigateur quand se dernier à compilé le DOM.

Très simplement, il faut garder à l'esprit qu'une page html est un ensemble de balises représentant des éléments.
Ces éléments sont compiler par le moteur javascript pour former des noeuds c'est ce qu'on appelle le DOM.

>Le Document Object Model (ou DOM) est un standard du W3C qui décrit une interface indépendante de tout langage de programmation et de toute plate-forme, permettant à des programmes informatiques et à des scripts d'accéder ou de mettre à jour le contenu, la structure ou le style de documents XML et HTML1. Le document peut ensuite être traité et les résultats de ces traitements peuvent être réincorporés dans le document tel qu'il sera présenté.

Pour déclancher notre code au bon moment il suffit d'écouter un évènement pariculier.
Nous allons ajouter un écouteur sur l'objet window, pour comprendre cet évènement je vous invite à regarder cette page <http://www.w3schools.com/jsref/event_onload.asp>.


        window.addEventListener('load',function(){
            document.getElementById('hello').innerHTML = "Hello World !";
            document.getElementById('hello').addEventListener('click', function (event) {
                event.preventDefault();
                event.target.style.backgroundColor = "#00FFFF";

            });
        });


Cet évènement déclanche l'éxécution du code lorsque le DOM est pret.
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
Dans cette partie, nous allons creer une morpion (Tic Tac Toe de son vrai nom). Vous pouvez le voir en fonctionnement sur la page de démo en ligne <http://fiddle.jshell.net/wQG7a/>.
Avant de commencer, il faut réfléchir à quoi nous avons besoin.
Généralement je travaille sur papier avant même de coder.

Nous avons besoin de savoir le fonctionnement du morpion.

>Les joueurs inscrivent tour à tour leur symbole sur une grille qui n'a pas de limites ou qui n'a que celles du papier sur lequel on joue. Le premier qui parvient à aligner trois de ses symboles gagne un point.

Nous avons donc besoin :

* Une grille de 3x3.
* De deux symboles `X` et `O`.
* De deux joueurs.

<a name="doc-grille"></a>
### Grille
Nous allons créer la grille.
Pour se faire, je vais utiliser la balise `table` en html.
Je crée donc trois lignes et trois colonnes ce qui donne :


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


Le souci est que vous ne voyez pas forcément le tableau.
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
Pour se faire nous allons utiliser les objets en javascript pour éviter que ce soit le fouilli.
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


L'intégralité de cette structure est expliquée sur la page [Application (avec jQuery)](/javascript/jquery/default/prototype).
Dans notre cas, nous n'utiliserons que la structure mais pas jQuery.

**Par quoi commencer ?**

Tous simplement je commencerais par gérer le cochage des cases.
Pour se faire nous allons placer un évènement sur le tableau qui détectera l'appuis sur une cellule.

**Pourquoi pas directement sur une cellule ?**

Tout simplement pour éviter de multiplier les évènements.
Si vous placez un évènement par céllule vous aurez N évènements qui correspondent au nombre de cellule.
Si vous le placez juste sur le tableau vous en aurez un quoi qu'il arrive.

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
symBole | C'est un tableau contenant le symbole pour chaque joueur
currentPlayer | Permet de déterminer quel joueur doit jouer. En l'occurence l'index pars de 0 donc l'initialisation à 1 est pour le deuxième joueur.
numWin | Nombres de  symboles nécéssaires pour gagner, comme nous sommes dans un tableau 3x3 la valeure est 3.
idReset | Identifiant du bouton de reset que nous verrons par la suite.
idGrid | Identifiant du tableau
idCurrentPlayer | Identifiant de la zone qui affiche à qui est le tour (que nous verrons par la suite).
finished | Indique si la partie est finie ou non.

init
----
Nous constatons que cette méthode lance l'initialisation des évènements lorsque le DOM est pret.

init_event
----------
Attache l'évènement au tabkeau, lors du disptach la méthode appelée est `onClick`.


    init_event: function () {
        document.getElementById(this.idGrid).addEventListener('click', function (event) {
            app.onClick(event);
        });
        document.getElementById(this.idReset).addEventListener('click', function (event) {
            app.onReset(event);
        });
    },




onClick
-------

Cette méthode permet dans un premier temps de vérifier si la partie est finie.

* Si c'est le cas il ne se passe rien.
* Sinon on vérifie que l'élément du DOM est valide à l'aide d'une petite méthode implémentée dans l'objet `checkValidDom`.
* Puis on vérifie qu'il sagit bien d'une cellule et qu'elle est vide à l'aide de `isAlreadyUse`.


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

        checkValidDom: function (domElement) {
            if (typeof(domElement) != 'undefined' && domElement != null) {
                return true;
            }
            return false;
        }


<div class="alert alert-info">Controlle si l'élément n'est pas indéfini ou nul. A garder de côté car on s'en sert souvent en javascript.</div>


Une fois tous ces controles passés on lance le cochage de la case à l'aide de `check`.


isAlreadyUse
------------
Controle juste si l'élément est vide ou non pour donner la possibilité de le remplir.

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
Je vous invite à prendre du temps pour réfléchir à comment vous allez détecter qu'une grille est gagnante.
Habituellement c'est simple mais d'un point de vue informations il faut coder les scénarios de victoire.

Pour ce faire il faut garder à l'esprit qu'un morpion est juste un tableau avec des coordonnées pour chaqu'un des cases.
Pour m'aider à coder les scénarios de victoire, je schématise les coordonées.

![table_space](/markdown/javascript/_images/jquery/tutorial/step_0/table_space.jpg)

Comme vous pouvez le voir chacune des coordonnée est représentée par X:Y.

Maintenant listons les cas de victoires  :

* Quand une ligne est pleine de votre symbole.
* Quand une colonne est pleine de votre symbole.
* Quand une diagonale est pleine de votre symbole.

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

Nous allons boucler sur chaque ligne; nous allons controler chaque colonne par ligne et vérifier qu'il contient notre symbole.
Si ce n'est pas le cas on retourne false.

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

Cette fois, il faut parcourir colonne par colonne pour déterminer que les symboles sont ceux du joueur courant.
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


Cette méthode parcour la diagonale du tableau pour déterminer si tous les symboles sont ceux du joueur courant.
L'ordre d'éxécution donne :

    0:0
    1:1
    2:2


<a name="doc-end"></a>
### Finitions
Une fois la mécanique de jeux en place vous êtes presque opérationnel.
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
Vous pouvez par exemple faire une suivi des scores, ajouter des couleurs par joueur ou même agrandir la zone de jeu.


<a name="doc-next"></a>
## Par la suite
Dans un prochain tutorial nous allons voir ce même jeu, mais cette fois ci avec jQuery.
Si le javascript pur et dur vous interesse je vous concocterai un résolveur de Sudoku.
