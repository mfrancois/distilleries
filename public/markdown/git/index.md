# GIT

## Contents
- [Présentation](#doc-presentation)
- [Particularités techniques](#doc-tec)
- [Fonctionnement](#doc-func)
- [Quelques commandes](#doc-commandes)


<a name="doc-presentation"></a>
## Présentation
Git est un logiciel de gestion de versions décentralisé.
C'est un logiciel libre créé par Linus Torvalds, créateur du noyau Linux, et distribué selon les termes de la licence publique générale GNU version 2.


![logo](/markdown/git/_images/git.png)

<a name="doc-tec"></a>
## Particularités techniques

Similaire en cela à BitKeeper, Git ne repose pas sur un serveur centralisé.
C'est un outil de bas niveau, qui se veut simple et performant, dont la principale tâche est de gérer l'évolution du contenu d'une arborescence.


Git indexe les fichiers d'après leur somme de contrôle calculée avec la fonction SHA-1.
Quand un fichier n'est pas modifié, la somme de contrôle ne change pas et le fichier n'est stocké qu'une seule fois.
En revanche, si le fichier est modifié, les deux versions sont stockées sur le disque.


Git n'était pas, au départ, à proprement parler un logiciel de gestion de versions.
Linus Torvalds expliquait que, « par bien des aspects, vous pouvez considérer Git comme un système de fichiers : il permet un adressage associatif, et possède la notion de versionnage, mais surtout, a été conçu en résolvant le problème du point de vue d'un spécialiste des systèmes de fichiers. Il n'y avait donc aucun intérêt à créer un système de gestion de version traditionnel. ».
Il a aujourd'hui évolué pour intégrer toutes les fonctionnalités d'un gestionnaire de versions.

Git est considéré comme performant, au point que certains autres logiciels de gestion de version (Darcs, Arch), qui n'utilisent pas de base de données, se sont montrés intéressés par le système de stockage des fichiers de Git pour leur propre fonctionnement1,2.
Ils continuent toutefois à proposer des fonctionnalités plus évoluées.

Les serveurs Git utilisent par défaut le port 9418 pour le protocole spécifique à GIT. Les protocoles HTTP, HTTPS et SSH (et leurs ports standard) peuvent aussi être utilisés.


<a name="doc-func"></a>
## Fonctionnement

Git possède deux structures de données : une base d'objets et un cache de répertoires.

Il existe quatre types d'objets :

* l'objet blob, qui représente le contenu d'un fichier (l'origine de cette dénomination est probablement à chercher dans les Binary Large OBjects des bases de données).
* l'objet tree (mot anglais signifiant « arbre »), qui est une liste d'objets de type blobs et des informations associées à chaque blob, tel que le nom du fichier et les permissions. Cet objet décrit l'arborescence des sources à un instant donné.
* l'objet commit, résultant de l'opération du même nom (de l'anglais, « commettre », « perpétrer », « s'engager », « décider », ici dans le sens de « confirmer », « valider ») et, qui donne accès à l'historique d'une arborescence de source. Il contient un message de log, un objet arbre et pointe vers un ou plusieurs objets commit parents.
* l'objet tag (étiquette) qui est une manière de représenter un commit spécifique. Il est en général utilisé pour marquer certains commits, par exemple par un numéro ou un nom de version (2.1 ou bien Hardy Heron).

La base des objets peut contenir n'importe quel type d'objets.
Une couche intermédiaire, utilisant des index (les sommes de contrôle), établit un lien entre les objets de la base et l'arborescence des fichiers.

Chaque objet est identifié par une somme de contrôle SHA-1 de son contenu.
Git calcule la somme de contrôle et utilise cette valeur pour déterminer le nom de fichier de l'objet.
L'objet est placé dans un répertoire dont le nom correspond aux deux premières lettres de la somme de contrôle.
Le reste de la somme de contrôle constitue alors le nom du fichier pour cet objet.
Git enregistre chaque révision dans un fichier en tant qu'objet blob unique.

Les relations entre les objets blobs sont déterminées en examinant les objets commit.
En général, les objets blobs sont stockés dans leur intégralité en utilisant la compression de la zlib.
Ce principe peut rapidement consommer une grande quantité de place disque ; de ce fait, les objets peuvent être combinés dans des archives, qui utilisent la compression différentielle (c'est-à-dire que les blobs sont enregistrés sous la forme de différences par rapport aux autres blobs).


<a name="doc-commandes"></a>
## Quelques commandes

Git dispose notamment des commandes suivantes (pour une liste complète, consultez la page de manuel Git) :

* `git init` crée un nouveau dépôt.
* `git clone` clone un dépôt distant.
* `git add` ajoute de nouveaux objets blobs dans la base des objets pour chaque fichier modifié depuis le dernier commit. Les objets précédents restent inchangés.
* `git commit` intègre le haché d'un objet tree et les hachés des objets commits parents pour créer un nouvel objet commit.
* `git branch` crée une nouvelle branche de développement.
* `git merge` fusionne plusieurs branches de développement.
