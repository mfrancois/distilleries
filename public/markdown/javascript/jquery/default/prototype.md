# Aplication (avec jQuery)


## Contents
- [Présentation](#doc-presentation)
- [Fichiers](#doc-files)


<a name="doc-presentation"></a>
## Présentation
Cette structure permet la création d'un regroupement de méthodes et la création d'un squelette pour initialiser une page web.
Vous pouvez retrouver ces fichiers [sur mon Gist](https://gist.github.com/mfrancois/9003214).

L'utilisation de ce genre de méthodes permet de classez les fonctions par catégories et de les regrouper.
Cella se rapproche des méthodes statics dans d'autres languages.


<a name="doc-files"></a>
## Fichiers

Dans cette exemple je mettrais trois fichier, le fichier `app.js` contiendras l'instanciation des plugins, ou autres méthodes (ex: création des sliders avec bxslider).
Le fichier `utils.js` est un exemple de regroupement de functions.
Le fichier `index.html` qui montreras comment inclures ces fichiers.

### app.js


    // Check instance
    if (typeof dist == "undefined" || !dist) {
        var dist = {};
    }
    if (typeof dist.Project == "undefined" || !dist.Project) {
        dist.Project = {};
    }
    dist.Project.Global = function () {
        this.init();
    };

    // ------------------------------------------------------------------------------------------------
    // ------------------------------------------------------------------------------------------------
    // ------------------------------------------------------------------------------------------------

    // Prototype
    dist.Project.Global.prototype = {

        ie8: (document.all && document.querySelector && !document.addEventListener) ? true : false,

        // --------------------------------------------------------------------------------------------

        init: function () {
            jQuery(document).ready(jQuery.proxy(this, 'onDocumentReady'));
            jQuery(window).load(jQuery.proxy(this, 'onWindowLoad'));
        },

        // --------------------------------------------------------------------------------------------

        onDocumentReady: function () {

        },

        // --------------------------------------------------------------------------------------------

        onWindowLoad: function () {

        },

        // --------------------------------------------------------------------------------------------
        // --------------------------------------------------------------------------------------------
        // --------------------------------------------------------------------------------------------

    };

    // ------------------------------------------------------------------------------------------------
    // ------------------------------------------------------------------------------------------------
    // ------------------------------------------------------------------------------------------------

    // Run instance
    var app = new dist.Project.Global();



#### Etudions les différentes parties

        // Check instance
        if (typeof dist == "undefined" || !dist) {
            var dist = {};
        }
        if (typeof dist.Project == "undefined" || !dist.Project) {
            dist.Project = {};
        }
        dist.Project.Global = function () {
            this.init();
        };

Permet la création du namespace et de l'objet Project s'il n'existe pas.
La fonction `dist.Project.Global` permet de lancer l'initialisation de la classe.



        dist.Project.Global.prototype = {

            ie8: (document.all && document.querySelector && !document.addEventListener) ? true : false,

            // --------------------------------------------------------------------------------------------

            init: function () {
                jQuery(document).ready(jQuery.proxy(this, 'onDocumentReady'));
                jQuery(window).load(jQuery.proxy(this, 'onWindowLoad'));
            },

            // --------------------------------------------------------------------------------------------

            onDocumentReady: function () {

            },

            // --------------------------------------------------------------------------------------------

            onWindowLoad: function () {

            },

            // --------------------------------------------------------------------------------------------
            // --------------------------------------------------------------------------------------------
            // --------------------------------------------------------------------------------------------

        };

La partie prototype permet d'ajouter des méthodes appelable dans l'objet. De base je place la méthode `init` qui est appelé par le constructeur `dist.Project.Global`.


### utils.js


    // Check instance
    if (typeof dist == "undefined" || !dist) {
        var dist = {};
        dist.singletons = {};
    }

    if (typeof dist.Common == "undefined" || !dist.Common) {
        dist.Common = {};
    }

    // ------------------------------------------------------------------------------------------------
    // ------------------------------------------------------------------------------------------------
    // ------------------------------------------------------------------------------------------------

    dist.Common.Util =
    {
       // Array Remove - By John Resig (MIT Licensed)
        array_remove: function(array, from, to) {
            var rest = array.slice((to || from) + 1 || array.length);
            array.length = from < 0 ? array.length + from : from;
            return array.push.apply(array, rest);
        },

        // Round a float/decimal number (dec = chiffres apres la virgule)
        roundNumber: function(num, dec) {
            var result = Math.round(num*Math.pow(10,dec))/Math.pow(10,dec);
            return result;
        }
    };



#### Etudions les différentes parties


    // Check instance
    if (typeof dist == "undefined" || !dist) {
        var dist = {};
        dist.singletons = {};
    }

    if (typeof dist.Common == "undefined" || !dist.Common) {
        dist.Common = {};
    }


Permet la création du namespace et de l'objet Common s'il n'existe pas.


        dist.Common.Util =
        {
           // Array Remove - By John Resig (MIT Licensed)
            array_remove: function(array, from, to) {
                var rest = array.slice((to || from) + 1 || array.length);
                array.length = from < 0 ? array.length + from : from;
                return array.push.apply(array, rest);
            },

            // Round a float/decimal number (dec = chiffres apres la virgule)
            roundNumber: function(num, dec) {
                var result = Math.round(num*Math.pow(10,dec))/Math.pow(10,dec);
                return result;
            }
        };


Cette partie montre la création d'un objet regroupant différentes méthodes.
Après la création de ces méthodes je peux les appeller directement à l'aide de

    dist.Common.Util.roundNumber(10.3333,2);

Rien ne vous empèche de créer d'autres function ou d'autres objets de regroupements.


    dist.Common.Str =
    {
        remove_symbole: function(str, char) {
            return str.replace(char,'');
        },
    };

    var res = dist.Common.Str.remove_symbole('Remove *','*');
    console.log(res);
    //Résultat Remove


### Index.html
Le fichier `index.html` montre une instanciation sur un élément DOM avec le passage d'un paramètre.


    <!DOCTYPE html>
    <html>
      <head>
        <meta charset="utf-8">

        <title></title>
        <meta name="description" content="">
        <meta name="viewport" content="width=device-width">
        <script src="//ajax.googleapis.com/ajax/libs/jquery/1.9.1/jquery.min.js" type="text/javascript"></script>

      <body>
        <div id="test"></div>
        <script type="text/javascript" src="js/app.js"></script>
        <script type="text/javascript" src="js/utils.js"></script>
      </body>
    </html>