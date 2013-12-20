# Installation

- [GIT & Bower](#git)
- [Dépendances](#dep)


<a name="git"></a>
## GIT & Bower

Dans un premier temps récupérez le projet, faites un checkout avec le nom que vous désirez :


    git@github.com:mfrancois/validUpload.git


Une fois fait allez dans le projet et installer les dépendances a l'aide de bower


    bower install


<div class="alert alert-dismissable alert-info">
Si vous n'avez pas bower installez le https://github.com/bower/bower
</div>


<a name="dep"></a>
## Dépendances
Il faut savoir que l'outil se sert de divers librairies :


    "dependencies": {
           "jquery": "~1.10.2",
           "validationEngine": "~2.6.4",
           "plupload": "~2.0.0",
           "bootstrap": "~3.0.0"
    }


Packagist | Utilisation
--------- | ------------
`jquery` | Framework de base nécéssaire pour l'utilisation de autres librairies
`validationEngine` | Framework de validation de formulaires https://github.com/posabsolute/jQuery-Validation-Engine
`plupload` | Framework d'upload de fichiers http://www.plupload.com/
`bootstrap` | Utilisé uniquement pour la démo

Une fois installé exécuté le fichier `index.html` vous devriez voir la page de démonstration.


![liste](/markdown/validupload/_images/demo.png)
