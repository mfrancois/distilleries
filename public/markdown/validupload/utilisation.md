# Utilisations

- [Exemple d'utilisation de base](#base)
- [Exemple d'utilisation d'upload multiple](#multi)
- [Exemple d'initialisation de contenu](#content)
- [Events](#events)

<a name="base"></a>
## Exemple d'utilisation de base

![Simple](/markdown/validupload/_images/simple.png)


#### Html

    <fieldset>
         <label>Single upload</label>
         <div class="uploader_conteneur"></div>
     </fieldset>

#### Javascript

         jQuery(document).ready(function () {
             jQuery('.uploader_conteneur').validUpload({
                 filters: [
                     {title: "Image files", extensions: "jpg,gif,png"},
                     {title: "Zip files", extensions: "zip"}
                 ]
             });
         });


<a name="multi"></a>
## Exemple d'utilisation d'upload multiple

![Multiple](/markdown/validupload/_images/multiple.png)

#### Html

    <fieldset>
        <label>Upload multiple</label>
        <div class="uploader_multiple"></div>
    </fieldset>


#### Javascript

         jQuery('.uploader_multiple').validUpload({
             dataUploader: {
                 runtimes: 'html5,flash,html4',
                 url: 'components/plupload/examples/upload.php',
                 flash_swf_url: 'components/plupload/js/Moxie.swf',
                 chunk_size: '1mb',
                 multi_selection: true,
                 unique_names: true
             }
         });


<a name="content"></a>
## Exemple d'initialisation de contenu


### Upload simple

![File](/markdown/validupload/_images/simple.jpg)

#### Html

    <fieldset>
        <label>Upload simple</label>
        <div class="uploader_conteneur_defaut"></div>
    </fieldset>


#### Javascript

         jQuery('.uploader_conteneur_defaut').validUpload({
             default_value:'test.jpg'
         });


### Upload multiple

![File](/markdown/validupload/_images/multiple.jpg)



#### Html

    <fieldset>
        <label>Upload multiple</label>
        <div class="uploader_multiple_default"></div>
    </fieldset>


#### Javascript

         jQuery('.uploader_multiple_default').validUpload({
              dataUploader: {
                  runtimes: 'html5,flash,html4',
                  url: 'components/plupload/examples/upload.php',
                  flash_swf_url: 'components/plupload/js/Moxie.swf',
                  chunk_size: '1mb',
                  multi_selection: true,
                  unique_names: true
              },
              default_value:'test_1.jpg,test_2.png,test_3.tiff'
          });


<a name="events"></a>
## Events


Event | Param | Description
----- | ----- | -----------
`onFilesAdded` | Uploader (up),  information sur les fichiers (file) | Appelé à chaque fois qu'une personne ajoute un fichier.
`onUploadProgress` | Uploader (up),  information sur le fichier (file) | Appelé à chaque progression de l'uplaod de fichier.
`onUploadInit` | Uploader (up), paramètre d'instanciation du composant d'upload | Appelé une fois que le composant est initialisé.
`onFileUploaded` | Uploader (up), fichier conerné (file), et les informations sur le retour de l'upload (requête) | Appelé une fois que le fichier est uploadé correctement.
`onUploadError` | Uploader (up) et l'erreur (err) | Appelé une fois qu'une erreurs est lancé par le composant plupload..
`onInit` | Instance de l'objet (this) | Appelé une fois que l'objet est fini d'être instantié.
`onInitTemplate` | Instance de l'objet (this) | Appelé une fois que le template est injecté dans son conteneur.
`onInitDisplay` | Instance de l'objet (this) | Appelé une fois que les éléments sont masqués ou affichés (remove,finished...) en fonction du contenue de l'input.
`onInitEvent` | Appelé une fois que les évnèments sont initialisés.



### Exemple d'implémentation d'évènement


#### Html


    <form class="form-inline" role="form">
        <fieldset>
            <label>Event upload</label>

            <div class="uploader_event"></div>
        </fieldset>
        <hr/>
        <pre class="console pre-scrollable">

        </pre>
    </form>


#### Javascript

    jQuery('.uploader_event').validUpload({
        onFilesAdded: function (up, file) {
            log(' ');
            log('---------------------------');
            log('START onFilesAdded');
            plupload.each(file, function (files) {
                log('File : ' + files.name);
            });
            log('END onFilesAdded');
            log('---------------------------');

        },
        onUploadProgress: function (up, file) {
            log(' ');
            log('---------------------------');
            log('START onUploadProgress');
            log('File : ' + file.name + " ======> " + file.percent + " %");
            log('END onUploadProgress');
            log('---------------------------');

        },
        onUploadInit: function (up, params) {
            log(' ');
            log('---------------------------');
            log('START onUploadInit');
            log('Runtime : ' + params.runtime);
            log('END onUploadInit');
            log('---------------------------');

        },
        onFileUploaded: function (up, file, info) {
            log(' ');
            log('---------------------------');
            log('START onFileUploaded');
            log('File : ' + file.name);
            log('END onFileUploaded');
            log('---------------------------');

        },
        onUploadError: function (up, err) {
            log(' ');
            log('---------------------------');
            log('START onFileUploaded');
            log('Error : ' + err);
            log('END onFileUploaded');
            log('---------------------------');
        },

        onInit: function (obj) {
            log(' ');
            log('---------------------------');
            log('START onInit');
            log('END onInit');
            log('---------------------------');
        },
        onInitTemplate: function (obj) {
            log(' ');
            log('---------------------------');
            log('START onInitTemplate');
            log('END onInitTemplate');
            log('---------------------------');
        },
        onInitData: function (obj) {
            log(' ');
            log('---------------------------');
            log('START onInitData');
            log('END onInitData');
            log('---------------------------');
        },
        onInitDisplay: function (obj) {
            log(' ');
            log('---------------------------');
            log('START onInitDisplay');
            log('END onInitDisplay');
            log('---------------------------');
        },
        onInitEvent: function (obj) {
            log(' ');
            log('---------------------------');
            log('START onInitEvent');
            log('END onInitEvent');
            log('---------------------------');
        }
    });



### Exemple d'utilisation avec une file d'image

![File](/markdown/validupload/_images/file.png)


#### Html

     <form class="form-inline" role="form">
        <fieldset>
            <label>Upload multiple</label>

            <div class="uploader_multiple_file"></div>
        </fieldset>
        <hr/>
    </form>

#### Javascript

    jQuery('.uploader_multiple_file').validUpload({
        dataUploader: {
            runtimes: 'html5,flash,html4',
            url: 'components/plupload/examples/upload.php',
            flash_swf_url: 'components/plupload/js/Moxie.swf',
            chunk_size: '1mb',
            multi_selection: true,
            unique_names: true,
            resize: {width: 320, height: 240, quality: 90},
            filters: [
                {title: "Images files", extensions: "jpg,jepg,tiff,gif,png,ico"}
            ]
        },
        default_value: 'image1.jpg,image2.jpg',
        onFileUploaded: function (up, file, info) {
            if (typeof(file.target_name) != 'undefined') {
                var tpl = '<img src="http://mon_url/' + file.target_name + '" alt="" />';
                var $elt = jQuery('#' + file.id).children("div:nth-child(2)");
                $elt.prepend(tpl);
            }
        },
        onAfterAddOneItem: function (file) {
            if (typeof(file.target_name) != 'undefined') {
                var tpl = '<img src="http://mon_url/' + file.target_name + '" alt="" />';
                var $elt = jQuery('#' + file.id).children("div:nth-child(2)");
                $elt.prepend(tpl);
            }
        }
    });