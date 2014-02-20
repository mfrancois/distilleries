# 2 - Les outils et le debug

- [Content](#doc-content)
- [GIT](#doc-git)
- [Les outils](#doc-tools)
    - [Interface de développement (IDE)](#doc-ide)
    - [Interface pour GIT](#doc-igit)
    - [Console sur Window](#doc-window)
    - [Outils pour debugger](#doc-tools)


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


<a name="doc-tools"></a>
### Outils pour debugger
Il existe une multitude d'outil pour debugger son code.
Le plus connu est [firebug](https://addons.mozilla.org/fr/firefox/addon/firebug/) pour les utilisateurs de firefox.
Pour ma part j'utilise les outils fournis par google; les [Chrome DevTools](https://developers.google.com/chrome-developer-tools/).

Dans ce tutorial je m'attarderais sur cette outil car c'est celui que je maitrise le mieux.
Il faut savoir que l'utilisation d'un debugger peut varier mais que dans les grandes lignes il reste le même, que se soit chrome ou firefox.


<div class="alert alert-info">
Les personnes qui font beaucoup de CSS préfères généralement utiliser firebug.
</div>


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


#### Utilisation de la console
La console sera l'un de vos outils le plus récurrent.
Si des erreurs ou des warnings sont présent c'est dans cette fenêtre que vous le verrez.

Elle dispose d'un pannel assez important de fonctions pour l'utiliser <https://developers.google.com/chrome-developer-tools/docs/console>.


Méthode | Utilisation
------- | -----------
console.log | Affiche le contenu de l'objet ou de la chaine dans la console.
console.error | Dispatch une erreur dans la console.
console.warn | Dispatch un warning dans la console.
console.group et  console.groupEnd| Permet de créer un groupe qui affiche l'intégralité des console.log entre ces deux instructions.
console.table | Permet d'afficher des structure de données ou des talbeau de façon lisible.


Nous allons voir l'utilisation de ces dernier dans des exemples concrets.



#### Utilisation des break points
@todo

#### Utilisation de l'inspecteur d'élément
@todo

