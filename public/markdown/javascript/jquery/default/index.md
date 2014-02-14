# Plugin jQuery


## Contents
- [Présentation](#doc-presentation)
- [Fichiers](#doc-files)


<a name="doc-presentation"></a>
## Présentation
Cette structure permet la création de plugins jquery multi instanciable avec passage de paramètres.
Vous pouvez retrouver ces fichiers [sur mon Gist](https://gist.github.com/mfrancois/9003066).
L'utilisation de plugins est faite pour créer du code réutilisable et sufisament générique pour correspondre à un besoin.

### Exemples

* [bxSlider](http://bxslider.com/) pour la créations de sliders
* [validUpload](http://distilleri.es/validupload) pour l'utlisation d'uploads
* [validationEngine](https://github.com/posabsolute/jQuery-Validation-Engine) pour la validation de formulaires


<a name="doc-files"></a>
## Fichiers
Dans cette exemple je mettrais deux fichier, le fichier `distExemple.js` qui contiendras mon plugin et le fichier `index.html` qui montreras une instanciation.

### distExemple.js
Le nom du fichier est à changer (dist Préfix de distilleries), il faut remplacer `distExemple` par le nom de votre plugin.
Il faut aussi remplacer `distExemple` dans le code javascript.


    (function($)
    {
        $.distExemple = function(element, options)
        {
            this.settings = $.extend(true, {}, $.distExemple.defaults, options);
            this.element = element;
            this.init();
        }
        $.extend($.distExemple,
        {
            defaults:
            {
            },
            prototype:
            {
                init: function()
                {
                    this.initData();
                    this.initEvent();
                },
                initData: function()
                {
                },
                initEvent: function()
                {
                }
            }
        });
        $.fn.distExemple = function(options)
        {
            return this.each(function()
            {
                if (undefined == $(this).data('distExemple'))
                {
                    $(this).data('distExemple', new $.distExemple(this, options));
                }
            });
        }
    })(jQuery);


### Ajouts de méthodes
Vous pouvez ajouter des méthodes dans la partie `prototype`.


    displayHello: function()
    {
        alert('Hello');
    }


### Préfix des selecteurs
Comme vous vous trouvez dans un plugins qui s'applique à un élément DOM il est conseillez d'utiliser un scope pour vous selections.

     initData: function()
     {
        $(this.settings.selectorPagination,this.element).html('');
     },



`this.settings.selectorPagination` fait appel au paramètres passé soit à l'instanciation soit par défault dans l'objet `default`.
`this.element` est l'objet sur le quel s'applique l'instance du plugins.
Nous récupérons donc la pagination en fonction de cette anglobeur.


### Rester dans le scope
Vous pouvez appeller une méthode en interne à l'aide du pointeur `this`.

#### Exemple

     init: function()
     {
        this.initData();
        this.initEvent();
     }

Pour les évènement c'est un peut différent. Pour ne pas perdre le scope j'utilise [`jQuey.proxy`](https://api.jquery.com/jQuery.proxy/).

    $(this.element).off('click').on('click',$.proxy(this, 'onClick'));

#### Exemple avec tout le plugin



    (function($)
    {
        $.distExemple = function(element, options)
        {
            this.settings = $.extend(true, {}, $.distExemple.defaults, options);
            this.element = element;
            this.init();
        }
        $.extend($.distExemple,
        {
            defaults:
            {
                selectorPagination:'div.paginate'
            },
            prototype:
            {
                init: function()
                {
                    this.initData();
                    this.initEvent();
                },
                initData: function()
                {
                    $(this.settings.selectorPagination,this.element).html('');
                },
                initEvent: function()
                {
                    $(this.element).off('click').on('click',$.proxy(this, 'onClick'));
                },

                onClick:function(event){
                    console.log(event);
                }
            }
        });
        $.fn.distExemple = function(options)
        {
            return this.each(function()
            {
                if (undefined == $(this).data('distExemple'))
                {
                    $(this).data('distExemple', new $.distExemple(this, options));
                }
            });
        }
    })(jQuery);



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
        <script type="text/javascript">
          jQuery(document).ready(function(){
            jQuery('#test').distExemple({
              'params1':true
            });
          });
        </script>
        <script type="text/javascript" src="js/distExemple.js"></script>
      </body>
    </html>