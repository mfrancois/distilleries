# 2 - Les outils et le debug

- [Content](#doc-content)
- [GIT](#doc-git)
- [Les outils](#doc-tools)
    - [Interface de développement (IDE)](#doc-ide)
    - [Interface pour GIT](#doc-igit)
    - [Console sur Window](#doc-window)
    - [Outils pour debugger](#doc-tools2)
        - [Interface](#doc-interface)
        - [Utilisation de la console](#doc-console)
            - [Etape 1 les erreurs](#doc-errors)
            - [Etape 2 le debug par dichotomie](#doc-dicho)
            - [Etape 3 Utilisation des break points](#doc-bp)
        - [Emulation mobile](#doc-usem)
        - [L'inspecteur d'élément](#doc-elements)


<a name="doc-content"></a>
## Contents
Dans ce tutorial je vais vous présenter les outils que j'utilise pour développer et des technique pour debugger votre code.
Nous verrons comment debugger du javascript, inspecter des éléments et émuler une version mobile.

Tout au long de ce tutorial vous allez être amenés à récupérer diverses branches.
Je vous invite à créer une copie du repository pour travailler et une copie pour suivre les explications.


<a name="doc-git"></a>
## GIT

Dans un premier temps vous devez récupérer le projet.
Pour se faire il vous suffit de taper la commande suivante :

    git clone -v --recurse-submodules --progress --branch tutorial/step_02 "https://github.com/mfrancois/javascript-tutorial.git"

Une fois fini vous devriez avoir votre projet sur la branche `tutorial/step_02`.

<a name="doc-tools"></a>
## Les outils

<a name="doc-ide"></a>
### Interface de développement (IDE)

PhpStorm
--------

Pour ma part j'utilise [PhpStorm](http://www.jetbrains.com/phpstorm/) mais si vous ne faites pas de Php je vous conseille alors d'utiliser |WebStorm](http://www.jetbrains.com/webstorm/whatsnew/).

* Personnalisable au niveau thèmes.
* Bonne analyse de code.
* Gestion des environnements.
* Beaucoup de plugins (git,console, database, jshint, angular, markdown...).
* Multi plateforme.
* Possibilité de créer des script automatiques.


![IDE](/markdown/javascript/_images/jquery/tutorial/step_2/phpstorm.png)

SublimeText
--------

Toute fois j'aime utiliser un ide plus simple pour l'édition de document.
Pour ce faire j'utilise [SublimeText](http://www.sublimetext.com/), légé et gratuit il possèdes beaucoup de fonctionalités.
Certains développeur préfère l'utiliser pour sa sobriété, il est aussi très puissant dans la gestion du code.


![sublim](/markdown/javascript/_images/jquery/tutorial/step_2/sublim.png)

<a name="doc-igit"></a>
### Interface pour GIT
Beaucoup utilises GIT en ligne de commande pour ma part j'utilise [sourceTree](http://www.sourcetreeapp.com/).

![sourcetree](/markdown/git/_images/git/sourcetree.png)


Points positif
-------------

* Bare des favories
* Ouverture des projets en onglets
* Facilité de checkout des branches
* Facilité de reverse et de suivi des versions
* Pull multiple par defaut
* Affichage du nombres de pull/push en attente
* Multi plateform
* Possibilité d'utiliser le gitflow

Points négatif
-------------

* Ide plus difficile à prendre en mains.
* Pas de patch (création et import) sur la version window.
* Pas d'intégration dans le menu window

<a name="doc-window"></a>
### Console sur Window
Si vous êtes amené à travailler sur window je vous conseille d'utiliser [Cygwin](http://www.cygwin.com/) avec [Console 2](http://sourceforge.net/projects/console/files/).
Avec ce duo vous pourrais presque avoir l'impression de bosser sur une base unix.

* Cygwin vous permet d'utiliser les commandes shell sur window.
* Console 2 vous permet de faire du multi onglet avec la console de votre choix.


![cygwin](/markdown/javascript/_images/jquery/tutorial/step_2/cygwin.jpg)


Pour les utilisations de ssh sur window je vous invites à utiliser [mRemoteNG](http://www.mremoteng.org/), il vous permet de vous connecter automatiquement à vos serveurs ssh.
Le tout sécurisé par mot de passe.
Très pratique quand vous avez beaucoup de serveur à gérer.

![screenshot](/markdown/javascript/_images/jquery/tutorial/step_2/screenshot.png)


<a name="doc-tools2"></a>
### Outils pour debugger
Il existe une multitude d'outil pour debugger son code.
Le plus connu est [firebug](https://addons.mozilla.org/fr/firefox/addon/firebug/) pour les utilisateurs de firefox.
Pour ma part j'utilise les outils fournis par google; les [Chrome DevTools](https://developers.google.com/chrome-developer-tools/).

Dans ce tutorial je m'attarderais sur cette outil car c'est celui que je maitrise le mieux.
Il faut savoir que l'utilisation d'un debugger peut varier mais que dans les grandes lignes il reste le même, que se soit chrome ou firefox.


<div class="alert alert-info">
Les personnes qui font beaucoup de CSS préfères généralement utiliser firebug.
</div>

<a name="doc-interface"></a>
#### Interface
L'outil de google est très bien documenté <https://developers.google.com/chrome-developer-tools/>.
Dans cette partie je vais faire une description rapide et une explication d'un debugg rapide.


Ouvrez le panneaux de debugg pour ce faire apuyez sur `F12`.
Une fois ouvert vous devriez avoir plusieurs onglets.


![debugging](/markdown/javascript/_images/jquery/tutorial/step_2/javascript-debugging-overview.jpg)


Onglets | Utilisation
------- | -----------
Elements | Contient l'inspecteur de la page web.
Network | Contient les divers appels contenu dans la page.
Sources | Permet d'inspecter les fichiers externes et les éditer.
Timeline | Outil de benshmark et de monitoring
Profiles | Outil de profiling. Permet de détecter les goulots d'étranglements du code.
Resources | Permet de voir les différentes resources utilisé par la page (cookie, base local, session, web sql...)
Audits | Détermine les points à amélioré en ce qui concerne votre page.
Console | Outil pour l'affichage et l'éxécution de javascript

<a name="doc-console"></a>
#### Utilisation de la console
La console sera l'un de vos outils le plus récurrent.
Si des erreurs ou des warnings sont présent c'est dans cette fenêtre que vous le verrez.

Elle dispose d'un pannel assez important de fonctions pour l'utiliser <https://developers.google.com/chrome-developer-tools/docs/console>.


Méthode | Utilisation
------- | -----------
console.log | Affiche le contenu de l'objet ou de la chaine dans la console.
console.assert | Dispatch une erreur si le premier paramètre est définie à false.
console.error | Dispatch une erreur dans la console.
console.warn | Dispatch un warning dans la console.
console.group et  console.groupEnd| Permet de créer un groupe qui affiche l'intégralité des console.log entre ces deux instructions.
console.table | Permet d'afficher des structure de données ou des talbeau de façon lisible.


Nous allons voir l'utilisation de ces derniers dans des exemples concrets.

<a name="doc-errors"></a>
##### Etape 1 les erreurs
Dans cette étape nous allons afficher la console et provoquez des erreurs pour vour leurs affichages.
Pour ce faire allez dans le fichier index.html et placé le code suivant entre les balises `body` :


    <script type="text/javascript">
        var error = 'test
    </script>

Ouvez la page et appuyez sur `F12`.
Vous dezvriez avoir une fenêtre qui s'ouvre. Cliquez sur `console` et rechargé la page avec `F5`.

![error](/markdown/javascript/_images/jquery/tutorial/step_2/error.jpg)


<div class="alert alert-warning">
Nous rechargons la page car l'activation de la console demande généralement un rechargement pour afficher les différents méssages.
</div>

Vous constatez deux méssages.
Le second est un warning de chrome avec jQuery ne le prenez pas en compte.
Interréssons nous au premier qui l'erreur déclanché par notre code.

Vous voyez le lien à la droite `localhost/:10`; cliquez dessus.

![error](/markdown/javascript/_images/jquery/tutorial/step_2/showerror.gif)

Vous constatez que le debugguer vous amène directement à la ligne qui pose problème.
Très pratique pour déterminer d'où vien votre erreur.
Les erreurs peuvent aussi être déclanché par votre application à l'aide de `console.assert` ou `console.error`.


console.error
--------------
Pour tester je vous invite à créer un champs `input`, sur le quel nous attacherons un évènement.
Placer le code suivant entre les balises `body`.


    <div>
        <label for="testeur">For dispatch error write "error"</label>
        <input name="testeur" id="testeur" type="text" />
        <script type="text/javascript">
            jQuery(document).ready(function(){
                jQuery('#testeur').off('keyup').on('keyup',function(event){
                   var value = jQuery(this).val();
                    if(value == "error"){
                        console.error('An error as dispatch !');
                    }
                });
            });
        </script>
    </div>

Ce code très simple permet de déclancer une erreur si l'utilisateur tape error dans l'input.



![inputerror](/markdown/javascript/_images/jquery/tutorial/step_2/inputerror.gif)


console.assert
--------------
Pour éviter de faire des if vous pouvez utiliser `console.assert`.
Simplement reprennons le code précédent :


    if(value == "error"){
        console.error('An error as dispatch !');
    }


Nous pouvons le remplacer par :

    console.assert(!(value == "error"),'An error as dispatch !');

<div class="alert alert-warning">
Nous inversion la condition car assert dispatch l'erreur que si le premier paramètre est faux.
</div>

<a name="doc-dicho"></a>
##### Etape 2 le debug par dichotomie
L'une des techniques souvent utilisé, par les développeur, est le debug par dichotomie.
Souvent utilisé pour rechercher des donneés , il permet d'optimiser de nombreuses intéractions <http://fr.wikipedia.org/wiki/Dichotomie>.

Dans notre cas nous l'utilisons lorsque nous ne sonvont pas vraiment où le programme plante.
Pour ce faire prennez la moitiez de votre code et placez un `console.log`.
S'il s'affiche c'est que le soucis est dans la partie basse.
Prennez la moitié de la partie basse et répété l'opération jusqu'à cibler le coeur du problème.


<div class="alert alert-warning">
Cette méthode de debug est très limité et ne correspond pas à toutes les situations.
Cette technique est adapté à un language procéduralle, difficile à utiliser en événementielle.
</div>

console.log
-----------
Reprennons le contenu de l'éxercice précédent.
Ajoutons y des `console.log`, au début à la fin et au déclanchement de l'évènement.
Ce qui nous donnes :


    <div>
        <label for="testeur">For dispatch error write "error"</label>
        <input name="testeur" id="testeur" type="text" />
        <script type="text/javascript">
            jQuery(document).ready(function(){
                console.log('Init application');
                jQuery('#testeur').off('keyup').on('keyup',function(event){
                   console.log(event);
                   var value = jQuery(this).val();
                   console.assert(!(value == "error"),'An error as dispatch !');
                });
                console.log('End off application');
            });
        </script>
    </div>



![consolelog](/markdown/javascript/_images/jquery/tutorial/step_2/consolelog.gif)

Cette méthode peux prendre un ou N paramètres.
Dans le cas ou vous placez plusieurs paramètres il vous faudra utiliser les formateurs.

    console.log("%s has %d points", "Sam", "100");

Formateur | Description
---------- | ----------
%s | Formation string.
%d or %i | Format int.
%f | Format float.
%o | Format DOM element.
%O | Format objet.
%c | Permet d'appliquer du css.


<div class="alert alert-info">
Personnellement je ne met sert pas des formateurs puisqu'il recaste automatiquement les éléments lorsque vous utilisez un seul paramètre.
</div>


<a name="doc-bp"></a>
##### Etape 3 Utilisation des break points
L'une des techniques les plus efficace reste l'utilisation de point d'arrêt (break point).
Leurs utilisations peut vous semblez obscure au début, ils deviendront rapidement vos amis.


Vous avez deux possibilités pour utiliser les break points.
La première et de placer une instruction dans votre code javascript.
Reprennons l'exercice précédent et plaçons la commande `debugger` avant l'initialisation.



    <div>
        <label for="testeur">For dispatch error write "error"</label>
        <input name="testeur" id="testeur" type="text" />
        <script type="text/javascript">
            jQuery(document).ready(function(){
                debugger;
                console.log('Init application');
                jQuery('#testeur').off('keyup').on('keyup',function(event){
                   console.log(event);
                   var value = jQuery(this).val();
                   console.assert(!(value == "error"),'An error as dispatch !');
                });
                console.log('End off application');
            });
        </script>
    </div>


![debugger](/markdown/javascript/_images/jquery/tutorial/step_2/debugger.gif)

Comme vous pouvez le voir dans l'image cella vous permet d'arrêter l'éxécution du code à un endroit donnée.
A l'aide des outils placé sous la console vous pouvez voir :

* Les variables
* Le scope des appels
* Les piles d'appels
* Les autres break points

Avec les boutons de step vous pouvez faire avancer votre code de ligne en ligne, de break point en break point.

Cette technique de break point est pratique lorsque vous avez accés au code.
Vous pouvez toute fois, à l'aide de la console, placer un break point dans un code et même y ajouter des instruction suplémentaires.

Pour tester placer vous de à la ligne 17 dans votre console.
C'est la ligne suivante :


    console.assert(!(value == "error"),'An error as dispatch !');


Faites un clique droit sur le chiffre 18, puis un cliquez sur **Add conditionnal break point** et ajouter la condition suivante :

    value == "test"

Si vous tapez le mot test vous verrez la console s'arrêter sur cette ligne.


![condbreak](/markdown/javascript/_images/jquery/tutorial/step_2/condbreak.gif)

<a name="doc-usem"></a>
#### Emulation mobile


Les outils vous permet aussi de tester sur un rendu mobile.
Pour ce faire rien de plus simple :

* Cliquez sur *Settings* (la petite roue)
* Onglet *Overrides* chochez *Show 'Emulation'...*
* Allez sur l'onglet *Elements*
* Cliquez sur l'icon *Show console*
* Sur la fenêtre qui s'affiche en bas cliquez sur *Emulation*
* Choisissez *Device* et voila enjoy.


![emulate](/markdown/javascript/_images/jquery/tutorial/step_2/emulate.gif)

<a name="doc-elements"></a>
#### L'inspecteur d'élément
L'un des outils les plus utilie reste l'inspecteur d'élément.
Pou l'utiliser vous avez deux techniques. Soit par un clique droit et **Inspecter l'élément** soit en passant directement par l'onglet *Elements*.
Vous pourrez regarder l'intégraliter de votre page web et affichez les éléments dans la console.
Il vous permet de modifier le code css ou html de la page pour faire des tests et vérifier l'interprétation de votre code.


![elements](/markdown/javascript/_images/jquery/tutorial/step_2/elements.gif)
