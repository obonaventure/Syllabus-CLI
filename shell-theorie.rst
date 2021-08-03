.. -*- coding: utf-8 -*-
.. Copyright |copy| 2012, 2020 by `Olivier Bonaventure <http://perso.uclouvain.be/olivier.bonaventure>`_, Etienne Rivière, Christoph Paasch, Grégory Detal
.. Ce fichier est distribué sous une licence `creative commons <http://creativecommons.org/licenses/by-sa/3.0/>`_

.. _shell:

Utilisation d'un système Unix
=============================

Dans cette section, nous allons décrire comment utiliser un système Unix tel que GNU/Linux en mettant l'accent sur l'utilisation de la ligne de commande.

Utilitaires
^^^^^^^^^^^

Unix a été conçu à l'époque des mini-ordinateurs. Un mini-ordinateur servait plusieurs utilisateurs en même temps. Ceux-ci y étaient connectés par l'intermédiaire d'un terminal équipé d'un écran et d'un clavier. Les programmes traitaient les données entrées par l'utilisateur via le clavier ou stockées sur le disque. Les résultats de l'exécution des ces programmes étaient affichés à l'écran, sauvegardés sur disque ou parfois imprimés sur papier.

Unix ayant été initialement développé pour manipuler des documents contenant du texte, il comprend de nombreux utilitaires facilitant ces traitements. Chaque utilitaire Unix a été conçu pour réaliser correctement une fonction principale. Comme nous le verrons ensuite, il est possible de combiner intelligemment ces différents utilitaires pour réaliser des traitements plus complexes pour lesquel il n'existe pas d'utilitaire spécifiques.

Les utilitaires Unix permettant avant tout de manipuler des fichiers. La plupart permettent de traiter des fichiers contenant du texte.

Lorsque l'on lance une console ou un terminal, on se retrouve généralement face à une fenêtre qui affiche un message de bienvenue comme dans l'exemple ci-dessous.

.. image:: figures/terminal.png

Le message de bienvenue peut varier d'un ordinateur à l'autre. Il peut aussi dépendre de l'état du système ou afficher des informations mises en avant par son gestionnaire. Dans l'exemple ci-dessus, il indique que l'on se connecte sur un serveur utilisant Linux version 4.19 (Debian). Il affiche le copyright t les contraintes d'utilisation et indique la date de la dernière connexion. La ligne ``obo@ovh-obo:~$``  est l'endroit où l'on peut taper les différentes commandes.


Une des commandes les plus simples de Unix est `echo(1)`_ qui permet d'afficher de l'information à l'écran. La capture d'écran ci-dessous présente trois exemples d'utilisation de `echo(1)`_. Comme toutes les commandes Unix, `echo(1)`_ prend un ou plusieurs arguments qui sont ici séparés par des espaces. La première invocation de `echo(1)`_ affiche 123 sur le terminal. Sous Unix, le terminal est aussi appelé la sortie standard, nous y reviendrons bientôt. La deuxième commande affiche Bonjour. Enfin, la troisième permet d'afficher une très longue phrase qui se termine par une longue suite de points.


.. image:: figures/terminal2.png

Nous reviendrons sur `echo(1)`_ un peu plus tard car vous verrez que c'est une commande très utile. Les utilitaires Unix permettent surtout de manipuler des fichiers contenant du texte. Prenons comme exemple le fichier suivant auquel nous avons donné le nom ```fichier.txt```. Ce fichier contient les lignes suivantes.

.. code:: console

   Les sanglots longs
   Des violons
   De l’automne
   Blessent mon coeur
   D’une langueur
   Monotone.

   Tout suffocant
   Et blême, quand
   Sonne l’heure,
   Je me souviens
   Des jours anciens
   Et je pleure;
   
   Et je m’en vais
   Au vent mauvais
   Qui m’emporte
   Deçà, delà,
   Pareil à la
   Feuille morte.
	   
Ce poème de Paul Verlaine a servi de signal du lancement du débarquement allié qui a mis fin à la seconde guerre mondiale. Plusieurs utilitaires permettent de manipuler de tels fichiers textes. Plutôt que de présenter une copie d'écran pour chaque exemple, nous présentons à partir de maintenant la commande précédée du symbôle ``$`` suivie par les messages qui sont affichés sur le terminal.

Une des premières commandes que l'on utilise pour manipuler des fichiers textes est la commande `cat(1)`_. Celle-ci affiche simplement sur le terminal le contenu du fichier. Dans l'exemple ci-dessous, Unix exécute la commande `cat(1)`_ avec comme argument le nom ```fichier.txt``. Lors de son exécution, la commande `cat(1)`_ ouvre le fichier dont le nom est ``fichier.txt`` et affiche son contenu.

.. code:: console

   $ cat fichier.txt 
   Les sanglots longs
   Des violons
   De l’automne
   Blessent mon coeur
   D’une langueur
   Monotone.

   Tout suffocant
   Et blême, quand
   Sonne l’heure,
   Je me souviens
   Des jours anciens
   Et je pleure;

   Et je m’en vais
   Au vent mauvais
   Qui m’emporte
   Deçà, delà,
   Pareil à la
   Feuille morte.


Les commandes Unix telles que `cat(1)`_ prennent des arguments comme présentés ci-dessus. Le comportement de ces commandes peut aussi être modifié en spécifiant une ou plusieurs options. Ces options commencent généralement par un ou deux tirets (caractère ``-``). Un première exemple est le message d'aide succinct que ``cat(1)`_ affiche lorsque l'on l'exécute avec ```--help`` comme option. 

.. code:: console

   $ cat --help
   Usage: cat [OPTION]... [FILE]...
   Concatenate FILE(s) to standard output.
   
   With no FILE, or when FILE is -, read standard input.

     -A, --show-all           equivalent to -vET
     -b, --number-nonblank    number nonempty output lines, overrides -n
     -e                       equivalent to -vE
     -E, --show-ends          display $ at end of each line
     -n, --number             number all output lines
     -s, --squeeze-blank      suppress repeated empty output lines
     -t                       equivalent to -vT
     -T, --show-tabs          display TAB characters as ^I
     -u                       (ignored)
     -v, --show-nonprinting   use ^ and M- notation, except for LFD and TAB
     --help     display this help and exit
     --version  output version information and exit

   Examples:
     cat f - g  Output f's contents, then standard input, then g's contents.
     cat        Copy standard input to standard output.

   GNU coreutils online help: <https://www.gnu.org/software/coreutils/>
   Full documentation at: <https://www.gnu.org/software/coreutils/cat>
   or available locally via: info '(coreutils) cat invocation'


La quasi totalité des commandes Unix affichent un message d'aide de ce type lorsqu'elles sont appelées avec ```--help`` ou parfois ```-h`` comme option.   

.. ajouter l'exercice https://inginious.org/course/cli-linux/ccm-cat

Il y a trois commandes qui sont très proches de `cat(1)`_ et qui peuvent être utiles lorsque l'on doit consulter de longs fichiers texte. Tout d'abord, la commande `head(1)`_ permet de consulter le début d'un fichier. Sans option, `head(1)`_ affiche les dix premières lignes du fichier. Avec l'option ``-n `` suivie d'un entier (``x``), `head(1)`_ affiche les ``x`` premières lignes du fichier. La commande `tail(1)`_ fait la même chose pour la fin du fichier. Si vous consultez la page de manuel de `tail(1)`_, vous verrez qu'elle a beaucoup plus d'options que `head(1)`_. Il y a en effet plusieurs cas pratiques dans lesquels il est utile de lire la fin d'un fichier que son début, mais ceux-ci sortent du cadre de cette brève introduction à la ligne de commande.

.. code:: console

   $head -n 4 fichier.txt 
   Les sanglots longs
   Des violons
   De l’automne
   Blessent mon coeur
   $ tail --lines 3 fichier.txt 
   Deçà, delà,
   Pareil à la
   Feuille morte.

La commande `more(1)`_ permet de visualiser tout un long fichier "page par page". Elle afiche la première page du fichier et invite l'utilisateur à taper un caractère pour poursuivre l'affichage du fichier. Si vous tapez sur espace, `more(1)`_ avancera d'un écran. Si vous tapez sur le retour à la ligne, `more(1)`_ avancera d'une ligne. Si vous tapez sur ``/``, vous pouvez indiquer un mot à rechercher dans le fichier. `more(1)`_ lira le fichier jusqu'à trouver le mot que vous recherchez et l'affichera. Enfin en tapan ``h``, `more(1)`_ vous affichera une page d'aide précisant toutes les touches que vous pouvez presser durant l'exécution de `more(1)`_ et le rôle de chacune d'entre elles.
   
Plusieurs commandes permettent de faire des manipulations plus avancées sur les fichiers. `wc(1)`_ permet d'extraire différents compteurs (nombre de lignes, nombre de mots et nombre de caractères) d'un fichier texte.

.. code:: console

   $ wc -w fichier.txt 
   45 fichier.txt
   $ wc -m fichier.txt 
   268 fichier.txt
   $ wc -l fichier.txt 
   20 fichier.txt
   $ wc fichier.txt 
   20  45 283 fichier.txt

Avec l'option ``-w``, `wc(1)`_ affiche le nombre de mots tandis qu'avec l'option ``-m``, `wc(1)`_ affiche le nombre de caractères. Enfin, l'option ``-l`` permet de connaître le nombre de lignes du fichier. Sans option, `wc(1)`_ affiche le nombre de lignes, le nombre de mots et le nombre de caractères.

Une autre commande très utile est `grep(1)`_. Elle permet notamment d'extraire d'un fichier texte les lignes qui contiennent ou ne contiennent pas une chaîne de caractères passée en argument. `grep(1)`_ est très souvent utilisé pour extraire de l'information de fichiers texte. La façon la plus simple d'utiliser `grep(1)`_ est d'utiliser comme argument la chaine de caractères à rechercher suivi du nom du fichier.

.. code:: console

   $ grep je fichier.txt 
   Et je pleure;
   Et je m’en vais

`grep(1)`_ est une des commandes les plus puissantes de Unix. Nous n'aurons pas l'occasion de la présenter complètement. Elle supporte de nombreuses options comme par exemple ``-i`` qui considère les majuscules et minuscules comme équivalentes.

.. code:: console
          
   $ grep -i jE fichier.txt 
   Je me souviens
   Et je pleure;
   Et je m’en vais

Deux autres options peuvent être intéressantes. L'option ``-v`` demande à `grep(1)`_ d'afficher les lignes qui ne contiennent pas la chaîne de caractères passée en argument. L'option ``-c`` elle compte les lignes qui correspondent plutôt que de les afficher. Les options peuvent être combinées comme dans les exemples ci-dessous.

.. code:: console

   $ grep -v e fichier.txt 
   
   Tout suffocant
   
   $ grep -c je fichier.txt 
   2
   $ grep -ci je fichier.txt 
   3
   $ grep -c -i je fichier.txt 
   3

Il est aussi possible de préciser plus finement les lignes que l'on veut extraire d'un fichier texteavec `grep(1)`_. Cela se fait en donnant comme argument à `grep(1)`_ une `expression régulière` au lieu d'une simple chaîne de caractères. A titre d'exemple, le caractère ``^`` dans une expression régulière indique qu'il faut rechercher le mot qui la suit en début de ligne. Le caractère ``$`` indique qu'il faut rechercher le mot qui le précède uniquement en fin de ligne.

.. code:: console

   $ grep -e "r$" fichier.txt 
   Blessent mon coeur
   D’une langueur
   $ grep -e "^Et" fichier.txt 
   Et blême, quand
   Et je pleure;
   Et je m’en vais


Pour présenter les dernières commandes, nous allons ajouter un deuxième fichier. Celui-ci a comme nom ``points.csv``. Il est au format ``comma-separated values``, c'est-à-dire qu'il contient des mots et des valuers qui sont séparées par une virgule. La plupart des tableurs permettent de manipuler de tels fichiers, tout comme les commandes Unix comme nous allons le voir. 

.. code:: console

   $ cat points.csv 
   Jean, Dubois, 12, 17
   Julie, Durant, 19, 16
   Marc, Michel, 11, 16
   Antoine, Marchand, 15, 15
   Emilie, Michel, 17, 19
   Laurence, Dupont, 14, 18
   Vanessa, Dupond, 14, 12
   Simon, Sanzot, 8, 9

Une première commande intéressante pour manipuler de tels fichiers est la commande `sort(1)`_. Comme son nom l'indique, celle-ci permet de trier des fichiers texte dans une ordre particulier. Sans option, `sort(1)`_ trie les lignes dans l'ordre alphabétique.

.. code:: console

   $ sort points.csv
   Antoine, Marchand, 15, 15
   Emilie, Michel, 17, 19
   Jean, Dubois, 12, 17
   Julie, Durant, 19, 16
   Laurence, Dupont, 14, 18
   Marc, Michel, 11, 16
   Simon, Sanzot, 8, 9
   Vanessa, Dupond, 14, 12


`sort(1)`_ a trié les étudiants sur base de leur prénom. L'option ``-r`` permet d'avoir les lignes dans l'ordre alphabétique inverse. Pour pouvoir trier sur base du nom de famille ou des points obtenus, il suffit d'indiquer à `sort(1)`_ la structure du fichier. Dans un fichier ``csv``, les champs sont séparés par une virgule. Par convention, le premier champ dans chaque ligne est le champ ``1``, le second le ``2``, ... L'option ``-t`` permet d'indiquer le séparateur des champs et l'option ``-k`` le numéro du champ à utiliser pour le tri. 


.. code:: console

   $ sort -t "," -k 1 points.csv
   Antoine, Marchand, 15, 15
   Emilie, Michel, 17, 19
   Jean, Dubois, 12, 17
   Julie, Durant, 19, 16
   Laurence, Dupont, 14, 18
   Marc, Michel, 11, 16
   Simon, Sanzot, 8, 9
   Vanessa, Dupond, 14, 12
 
On peut maintenant trier sur base des noms de famille ou des points obtenus.

.. code:: console

   $ sort -t "," -k 2 points.csv
   Jean, Dubois, 12, 17
   Vanessa, Dupond, 14, 12
   Laurence, Dupont, 14, 18
   Julie, Durant, 19, 16
   Antoine, Marchand, 15, 15
   Marc, Michel, 11, 16
   Emilie, Michel, 17, 19
   Simon, Sanzot, 18, 10

.. code:: console

   $sort -r -t "," -k 4 points.csv
   Simon, Sanzot, 8, 9
   Emilie, Michel, 17, 19
   Laurence, Dupont, 14, 18
   Jean, Dubois, 12, 17
   Marc, Michel, 11, 16
   Julie, Durant, 19, 16
   Antoine, Marchand, 15, 15
   Vanessa, Dupond, 14, 12

Malheureusement, ce dernier tri ne donne pas le résultat attendu. On voudrait avoir en première ligne l'étudiant ou l'étudiante qui a le mieux réussi le cours. Or, ce n'est pas ce que la commande `sort(1)`_ affiche. C'est parce que la commande `sort(1)`_ fait un tri par ordre alphabétique par défaut. Pour obtenir un tri qui prend en compte les nombres (entiers ou réels), il faut utiliser l'option ``-n``.    

.. code:: console

   $ sort -n -r -t "," -k 4 points.csv
   Emilie, Michel, 17, 19
   Laurence, Dupont, 14, 18
   Jean, Dubois, 12, 17
   Marc, Michel, 11, 16
   Julie, Durant, 19, 16
   Antoine, Marchand, 15, 15
   Vanessa, Dupond, 14, 12
   Simon, Sanzot, 8, 9


Parfois, il est nécessaire d'extraire certains champs d'un fichier en format ``csv``. La commande `cut(1)`_ peut être très utile dans ce cas. Elle supporte plusieurs options. L'option ``-d`` permet d'indiquer le séparateur entre les différents champs du fichier. L'option ``-f`` est suivie de la liste des champs qu'il faut extraire du fichier.

.. code:: console
          
   $ cut -d "," -f 1,3 points.csv
   Jean, 12
   Julie, 19
   Marc, 11
   Antoine, 15
   Emilie, 17
   Laurence, 14
   Vanessa, 14
   Simon, 8


   
   .. Une description détaillée de l'ensemble de ces utilitaires sort du cadre de ce cours. De nombreux livres et ressources Internet fournissent une description détaillée. Voici cependant une brève présentation de quelques utilitaires de manipulation de texte qui peuvent s'avérer très utiles en pratique.

Notre dernier exemple est la commande `uniq(1)`_ qui permet de retirer d'un fichier *trié* les lignes qui sont identiques. A titre d'exemple, considérons le nouveau fichier ``noms.txt`` qui contient tous les noms de famille du fichier ``points.csv`` en ordre alphabétique.

.. code:: console

   $ cat noms.txt 
   Dubois
   Dupond
   Dupont
   Durant
   Marchand
   Michel
   Michel
   Sanzot

   
La commande `uniq(1)`_ permet de retirer toutes les lignes qui sont identiques dans ce fichier *trié*.

.. code:: console

   $ uniq noms.txt 
   Dubois
   Dupond
   Dupont
   Durant
   Marchand
   Michel
   Sanzot
       

.. Ajouter l'exercice https://inginious.org/course/cli-linux/qcm-sort
   
.. - `uniq(1)`_ : utilitaire permettant de filtrer le contenu d'un fichier texte afin d'en extraire les lignes qui sont uniques ou dupliquées (cela requiert que le fichier d'entrée soit trié, car ne compare que les lignes consécutives).
.. - `gzip(1)`_ et `gunzip(1)`_ : utilitaires permettant respectivement de compresser et de décompresser des fichiers. Les fichiers compressés prennent moins de place sur le disque que les fichiers standard et ont par convention un nom qui se termine par ``.gz``.
.. - `tar(1)`_ : utilitaire permettant de regrouper plusieurs fichiers dans une archive. Souvent utilisé en combinaison avec `gzip(1)`_ pour réaliser des backups ou distribuer des logiciels.
.. - `sed(1)`_ : utilitaire permettant d'éditer, c'est-à-dire de modifier les caractères présents dans un flux de données.
.. - `awk(1)`_ : utilitaire incluant un petit langage de programmation et qui permet d'écrire rapidement de nombreux programmes de manipulation de fichiers de texte.

.. topic:: Pages de manuel

  Les systèmes d'exploitation de la famille Unix contiennent un grand nombre de librairies, d'appels systèmes et d'utilitaires. Toutes ces fonctions et tous ces programmes sont documentés dans des pages de manuel qui sont accessibles via la commande ``man``. Les pages de manuel sont organisées en 8 sections.

   - Section 1: Utilitaires disponibles pour tous les utilisateurs
   - Section 2: Appels systèmes en C
   - Section 3: Fonctions de la librairie
   - Section 4: Fichiers spéciaux
   - Section 5: Formats de fichiers et conventions pour certains types de fichiers
   - Section 6: Jeux
   - Section 7: Utilitaires de manipulation de fichiers textes
   - Section 8: Commandes et procédure de gestion du système

  Dans le cadre de ce syllabus d'introduction, nous aborderons uniquement les fonctionnalités décrites dans la première sections des page de manuel. L'accès à une page de manuel se fait via la commande ``man`` avec comme argument le nom de la commande concernée. Vous pouvez par exemple obtenir la page de manuel de ``gcc`` en tapant ``man gcc``. ``man`` supporte plusieurs paramètres qui sont décrits dans sa page de manuel accessible via ``man man``. Chaque section du manuel Unix reprend une page d'introduction qui décrit brièvement les principales pages de cette section. L'introduction de la section 1 qui présente les principales commandes est disponible en `anglais <https://man7.org/linux/man-pages/man1/intro.1.html>`_ et ainsi qu'en `français <https://man.cx/intro(1)/fr>`_.

  Outre ces pages de manuel locales, il existe également de nombreux sites web où l'on peut accéder aux pages de manuels de différentes versions de Unix dont notamment :

   - les pages de manuel de `Debian GNU/Linux <http://manpages.debian.net/>`_
   - les pages de manuel de `FreeBSD <http://www.freebsd.org/cgi/man.cgi>`_
   - les pages de manuel de `MacOS <http://developer.apple.com/documentation/Darwin/Reference/ManPages/index.html>`_

  Dans la version en-ligne de ces notes, toutes les références vers un programme Unix, un appel système ou une fonction de la librairie pointent vers la page de manuel Linux correspondante. Les pages de manuel sont également disponibles sur de nombreux sites web, comme par exemple `https://www.man7.org/linux/man-pages/index.html <https://www.man7.org/linux/man-pages/index.html>`_ qui présente les dernières versions des pages de manuel de Linux en anglais. Certaines de ces pages de manuel ont étés traduite (parfois partiellement en français). Vous les trouverez notamment sur `https://man.cx/ <https://man.cx/>`_.

Fichiers et répertoires
^^^^^^^^^^^^^^^^^^^^^^^

Nous avons travaillé sur quelques fichiers. En pratique, un ordinateur contient souvent des milliers de fichiers. Les deux fichiers que nous avons utilisé dans la section précédente sont dans un répertoire. Un répertoire est une structure logique qui regroupe des fichiers et/ou d'autres répertoires. On peut imaginer le disque dur ou le SSD d'un ordinateur comme étant une grand armoire remplie de tiroirs. Chaque tiroir est un répertoire qui peut contenir des fichiers ou d'autres répertoires.

La première commande utile pour manipuler les fichiers qui sont stockés dans des répertoires est la commande `ls(1)`_ (pour `list`). Cette commande permet de lister les fichiers qui se trouve dans le répertoire courant par défaut ou dans un quelconque répertoire dont le nom est passé en argument.

.. code:: console

   $ ls
   fichier.txt  points.csv

Utilisée sans options et sans arguments, la commande `ls(1)`_ affiche les noms des fichiers et répertoires présents dans le répertoire actuel. L'exemple ci-dessus montre les deux fichiers nommés ``fichier.txt`` et ``points.csv``. La commande `ls(1)`_ supporte un grand nombre d'options. En voici quelques unes qui sont assez utiles en pratique. Les autres sont décrites dans la page de manuel de `ls(1)`_. L'option ``-l`` affiche des informations complémentaires sur chaque fichier comme le nom de son propriétaire, le groupe auquel celui-ci appartient, la date de dernière modification, la taille et les permissions du fichier.

.. code:: console

          $ ls -l
          total 8
          -rw-r--r-- 1 obo obo 283 Aug  2 15:34 fichier.txt
          -rw-r--r-- 1 obo obo 181 Aug  3 10:18 points.csv

La première ligne indique l'espace disque occupé par les fichiers du répertoire (dans ce cas, 8 KBytes). Ensuite, pour chaque fichier on trouve ses permissions, son propriétaire et le groupe auquel il appartient, la date de dernière modification et le nom du fichier.

Il est possible de modifier l'ordre dans lequel `ls(1)`_ affiche les différents fichiers d'un répertoire. Ainsi, l'option ``-S`` permet de les afficher par ordre décroissant de taille, bien pratique lorsqu'il faut rechercher les gros fichiers qui occupent de la place sur le disque due. L'option ``-t`` permet d'afficher d'abord les fichiers les plus récents. Très pratique pour retrouver le dernier fichier téléchargé par exemple.

Une commande intéressante de manipulation des fichiers est `touch(1)`_. Elle permet de mettre à jour la date de modification d'un fichier sans changer son contenu.

.. code:: console

   $ ls -lt
   total 8
   -rw-r--r-- 1 obo obo 181 Aug  3 10:18 points.csv
   -rw-r--r-- 1 obo obo 283 Aug  2 15:34 fichier.txt
   $ touch fichier.txt 
   $ ls -lt
   total 8
   -rw-r--r-- 1 obo obo 283 Aug  3 14:11 fichier.txt
   -rw-r--r-- 1 obo obo 181 Aug  3 10:18 points.csv

Utilisée sans argument, la commande `touch(1)`_ permet de créer un fichier vide.

.. code:: console

   $ touch vide.txt
   $ ls -lt
   total 8
   -rw-r--r-- 1 obo obo   0 Aug  3 14:13 vide.txt
   -rw-r--r-- 1 obo obo 283 Aug  3 14:11 fichier.txt
   -rw-r--r-- 1 obo obo 181 Aug  3 10:18 points.csv
   
Pour organiser tous ces fichiers, il est important de pouvoir les regrouper ensemble dans des répertoires

  
Shell
^^^^^

Avant le développement des interfaces graphiques telles que :term:`X11`, :term:`Gnome` ou :term:`Aqua`, l'utilisateur interagissait exclusivement avec l'ordinateur par l'intermédiaire d'un interpréteur de commandes. Dans le monde Unix, le terme anglais :term:`shell` est le plus souvent utilisé pour désigner cet interpréteur et nous ferons de même.

Un :term:`shell` est un programme qui a été spécialement conçu pour faciliter l'utilisation d'un système Unix via le clavier. De nombreux shells Unix existent. Les plus simples permettent à l'utilisateur de taper une série de commandes à exécuter en les combinant. Les plus avancés sont des interpréteurs de commandes qui supportent un langage complet permettant le développement de scripts plus ou moins ambitieux. Dans le cadre de ce cours, nous utiliserons `bash(1)`_ qui est un des shells les plus populaires et les plus complets. La plupart des commandes `bash(1)`_ que nous utiliserons sont cependant compatibles avec de nombreux autres shells tels que `zsh <http://www.zsh.org>`_ ou `csh <https://github.com/tcsh-org/tcsh>`_.

Bien que les interfaces graphiques se soient désormais généralisées, le shell reste un moyen d'interaction avec le système parfaitement complémentaire, particulièrement utile pour les informaticiens, ou toute personne devant automatiser des traitements et opérations sur un système informatique. Avec les interfaces graphiques actuelles, le shell est accessible par l'intermédiaire d'une application qui est généralement appelée ``terminal`` ou ``console``.

Lorsqu'un utilisateur se connecte à un système Unix, en direct ou à travers une connexion réseau, le système vérifie son mot de passe puis exécute automatiquement le shell qui est associé à cet utilisateur depuis son répertoire par défaut. Ce shell permet à l'utilisateur d'exécuter et de combiner des commandes. Un shell supporte deux types de commande : les commandes internes qu'il implémente directement et les commandes externes qui font appel à un utilitaire stocké sur disque. Un exemple de commande interne est `cd(1posix)`_ qui prend comme argument un chemin (relatif ou absolu) et y positionne le répertoire courant. Les utilitaires présentés dans la section précédente sont des exemples de commandes externes.

.. .. note:: Obtenir de l'aide sur une commande
..
..  La commande `man(1)`_ permet d'obtenir la documentation associée à une commande externe. Par exemple, `man ls` permet d'obtenir la documentation de la commande `ls` et en particulier de lister les arguments et paramètres reconnus par cette commande.
..
..  **Attention :** `man(1)`_ permet de spécifier dans quel section de la documentation la page de documentation doit être recherchée. Il existe en effet 8 sections. La page de manuel de `man(1)`_ liste ces sections : on l'obtient avec la commande `man man`. Par exemple, `printf` peut référer aussi bien en section (1) à une commande externe qu'en section (3) à la fonction de la librairie standard du langage C. `man printf` présente par défaut la première occurence, celle en section (1). Pour obtenir la documentation de la fonction `printf` de la librairie standard C il faut spécifier la section avec la commande `man 3 printf`.

Voici quelques exemples d'utilisation de commandes externes.

.. literalinclude:: src/exemple.out
        :language: console

.. spelling::

   supercalculateurs
   quadrimestre

Combiner des commandes
^^^^^^^^^^^^^^^^^^^^^^

La plupart des utilitaires fournis avec un système Unix ont été conçus pour être utilisés en combinaison avec d'autres. Cette combinaison efficace de plusieurs petits utilitaires est un des points forts des systèmes Unix par rapport à d'autres systèmes d'exploitation. On peut imaginer par exemple associer `sort(1)`_ et `head(1)`_ pour n'afficher que les premiers noms en ordre alphabétique d'une liste d'étudiants disponible initialement sous forme non triée. Afin de permettre cette combinaison, chaque programme Unix en cours d'exécution (appelé un *processus*) est associé à trois *flux* standards :

 - une entrée standard (:term:`stdin` en anglais) qui est un flux d'informations par lequel le processus reçoit les données à traiter. Par défaut, l'entrée standard est associée au clavier.
 - une sortie standard (:term:`stdout` en anglais) qui est un flux d'informations sur lequel le processus écrit le résultat de son traitement. Par défaut, la sortie standard est associée au terminal.
 - une sortie d'erreur standard (:term:`stderr` en anglais) qui est un flux de données sur lequel le processus écrira les messages d'erreur éventuels. Par défaut, la sortie d'erreur standard est associée au même terminal que :term:`stdout`.

La puissance du :term:`shell` vient de la possibilité de combiner des commandes en redirigeant les entrées et sorties standards. Les shells Unix supportent différentes formes de redirection. Tout d'abord, il est possible de forcer un programme à lire son entrée standard depuis un fichier plutôt que depuis le clavier. Cela se fait en ajoutant à la fin de la ligne de commande le caractère ``<`` suivi du nom du fichier à lire. Ensuite, il est possible de rediriger la sortie standard vers un fichier. Cela se fait en utilisant ``>`` ou ``>>``. Lorsqu'une commande est suivie de ``> file``, le fichier ``file`` est créé si il n'existait pas et remis à zéro si il existait, et la sortie standard de cette commande est redirigée vers le fichier ``file``. Lorsqu'un commande est suivie de ``>> file``, la sortie standard est sauvegardée à la fin du fichier ``file`` (si ``file`` n'existait pas, il est créé).

Voici un exemple d'utilisation des redirections :

.. literalinclude:: src/exemple2.out
        :language: console

.. note:: Rediriger la sortie d'erreur standard

 La redirection `> file` redirige par défaut la sortie standard vers le fichier `file`. La sortie d'erreur standard reste dirigé, quand à elle, vers le terminal de l'utilisateur. Il arrive toutefois que l'on souhaite diriger les messages d'erreur vers un fichier différent. On peut pour cela utiliser la notation `2> file_errors` (le  flux :term:`stdout` est numéroté 1 et le flux :term:`stderr` est numéroté 2; la notation `> file` est implicitement équivalente à `1> file`). 
 
 Si l'on souhaite rediriger à la fois :term:`stdout` et :term:`stderr` vers le même fichier on ne peux pas utiliser `> file 2> file` ! Il faut d'abord rediriger la sortie :term:`stderr` vers :term:`stdout`, puis diriger ce dernier vers le fichier. Le flux :term:`stdout` est noté `&1`, on utilise donc `2>&1 > file`.
  
 Des informations plus complètes sur les mécanismes de redirection de `bash(1)`_ peuvent être obtenues dans le `chapitre 20 <http://tldp.org/LDP/abs/html/io-redirection.html>`_ de [ABS]_.

Les shells Unix supportent un second mécanisme qui est encore plus intéressant pour combiner plusieurs programmes. Il s'agit de la redirection de la sortie standard d'un programme vers l'entrée standard d'un autre sans passer par un fichier intermédiaire. Cela se réalise avec le symbole ``|`` (:term:`pipe` en anglais). L'exemple suivant illustre quelques combinaisons d'utilitaires de manipulation de texte.

.. literalinclude:: src/exemple3.out
        :language: console

Le premier exemple utilise `echo(1)`_ pour générer du texte et le passer directement à `wc(1)`_ qui compte le nombre de caractères. Le deuxième exemple utilise `cat(1)`_ pour afficher sur la sortie standard le contenu d'un fichier. Cette sortie est reliée à `sort(1)`_ qui trie le texte reçu sur son entrée standard en ordre alphabétique croissant. Cette sortie en ordre alphabétique est reliée à `uniq(1)`_ qui la filtre pour en retirer les lignes dupliquées.




Scripts : les bases
^^^^^^^^^^^^^^^^^^^

Tout shell Unix peut également s'utiliser comme un interpréteur de commande qui permet d'interpréter des scripts. Un système Unix peut exécuter deux types de programmes :

 - des programmes exécutables en langage machine. C'est le cas de la plupart des utilitaires dont nous avons parlé jusqu'ici.
 - des programmes écrits dans un langage interprété. C'est le cas des programmes écrits pour le shell, mais également pour d'autres langages interprétés comme python_ ou perl_.

Lors de l'exécution d'un programme, le système d'exploitation reconnaît [#fexecbit]_ si il s'agit d'un programme directement exécutable ou d'un programme interprété en analysant les premiers octets du fichier. Par convention, sous Unix, les deux premiers caractères d'un programme écrit dans un langage qui doit être interprété sont ``#!``. Ils sont suivis par le nom complet de l'interpréteur qui doit être utilisé pour interpréter le programme.

Le programme `bash(1)`_ le plus simple est le suivant :

.. literalinclude:: src/hello.sh
   :language: bash

L'exécution de ce script shell retourne la sortie suivante :

.. literalinclude:: src/hello.sh.out
        :language: console

Par convention en `bash(1)`_, le caractère ``#`` marque le début d'un commentaire en début ou en cours de ligne. Comme tout langage, `bash(1)`_ permet à l'utilisateur de définir des variables. Celles-ci peuvent contenir des chaînes de caractères ou des nombres. Le script ci-dessous utilise deux variables, ``PROG`` et ``COURS`` et les utilise pour afficher un texte avec la commande ``echo``.

.. literalinclude:: src/hellovar.sh
   :language: bash
   
On note dans l'exemple ci-dessus l'utilisation du symbole ``$`` pour référer à la valeur de la variable. Dans la majorité des cas, cette notation suffit. Il y a une subtilité auxquelles ont doit faire attention : si il y a une ambiguïté possible sur le nom de la variable pour l'interpréteur il convient d'entourer son nom d'accolades ``{ }``. Par exemple, ``milieu = "mi"; echo do$milieuno`` affichera ``do`` seulement car l'interpréteur considère la seconde partie comme la variable ``$milieuno`` non définie et donc égale à la chaîne vide (et cela sans générer de message d'erreur). Avec ``echo do${milieu}no``, par contre, le résultat est celui attendu.

Un script `bash(1)`_ peut également prendre des arguments passés en ligne de commande. Par convention, ceux-ci ont comme noms ``$1``, ``$2``, ``$3``, ... Le nombre d'arguments s'obtient avec ``$#`` et la liste complète avec ``$@``. L'exemple ci-dessous illustre l'utilisation de ces arguments.

.. literalinclude:: src/args.sh
   :language: bash

L'exécution de ce script produit la sortie suivante :

.. literalinclude:: src/args.sh.out
        :language: console

Concernant le traitement des arguments par un script bash, il est utile de noter que lorsque l'on appelle un script en redirigeant son entrée ou sa sortie standard, le script n'est pas informé de cette redirection. Ainsi, si l'on exécute le script précédent en faisant ``args.sh arg1 > args.out``, le fichier ``args.out`` contient les lignes suivantes :

.. literalinclude:: src/args.out
        :language: console

Scripts : conditionnelles
^^^^^^^^^^^^^^^^^^^^^^^^^

Un script permet d'utiliser des structures de contrôle comme dans tout langage de programmation.

`bash(1)`_ supporte tout d'abord la construction conditionnelle ``if [ condition ]; then ... fi`` qui permet notamment de comparer les valeurs de variables. `bash(1)`_ définit de nombreuses conditions différentes, dont notamment :

 - ``$i -eq $j`` est vraie lorsque les deux variables ``$i`` et ``$j`` contiennent le même nombre.
 - ``$i -lt $j`` est vraie lorsque la valeur de la variable ``$i`` est numériquement strictement inférieure à celle de la variable ``$j``
 - ``$i -ge $j`` est vraie lorsque la valeur de la variable ``$i`` est numériquement supérieure ou égale à celle de la variable ``$j``
 -  ``$s = $t`` est vraie lorsque la chaîne de caractères contenue dans la variable ``$s`` est égale à celle qui est contenue dans la variable ``$t``
 - ``-z $s`` est vraie lorsque la chaîne de caractères contenue dans la variable ``$s`` est vide

D'autres types de test sont définis dans la page de manuel : `bash(1)`_. Le script ci-dessous fournit un premier exemple d'utilisation de tests avec `bash(1)`_.

.. literalinclude:: src/eq.sh
   :language: bash

Tout d'abord, ce script vérifie qu'il a bien été appelé avec deux arguments. Vérifier qu'un programme reçoit bien les arguments qu'il attend est une règle de bonne pratique qu'il est bon de respecter dès le début. Si le script n'est pas appelé avec le bon nombre d'arguments, un message d'erreur est affiché sur la sortie d'erreur standard et le script se termine avec un code de retour. Ces codes de retour sont importants car ils permettent à un autre programme, par exemple un autre script `bash(1)`_ de vérifier le bon déroulement d'un programme appelé. Le script :download:`src/eq.sh` utilise des appels explicites à `exit(1posix)`_ même si par défaut, un script `bash(1)`_  qui n'en contient pas retourne un code de retour nul à la fin de son exécution.

Un autre exemple d'utilisation des codes de retour est le script :download:`src/wordin.sh` repris ci-dessous qui utilise `grep(1)`_ pour déterminer si un mot passé en argument est présent dans un fichier texte. Pour cela, il exploite la variable spéciale ``$?`` dans laquelle `bash(1)`_ sauve le code de retour du dernier programme exécuté par le script.

.. literalinclude:: src/wordin.sh
   :language: bash

Ce programme utilise le fichier spécial ``/dev/null``. Celui-ci est en pratique l'équivalent d'un trou noir. Il accepte toutes les données en écriture mais celles-ci ne peuvent jamais être relues. ``/dev/null`` est très utile lorsque l'on veut ignorer la sortie d'un programme et éviter qu'elle ne s'affiche sur le terminal. `bash(1)`_ supporte également ``/dev/stdin`` pour représenter l'entrée standard, ``/dev/stdout`` pour la sortie standard et ``/dev/stderr`` pour l'erreur standard.

Les scripts servent souvent à réaliser des opérations sur des fichiers, et il est parfois nécessaire de pouvoir tester si un fichier est présent, n'est pas vide, etc. On peut alors utiliser les conditions suivantes :

 - ``-f file`` est vraie si ``file`` existe et est un fichier;
 - ``-s file`` est vraie si ``file`` n'est pas vide;
 - ``-r file``, ``-w file``, ``-x file`` est vraie si ``file`` peut, respectivement, être *lu*, *écrit* ou *exécuté* par l'utilisateur lançant le script;
 - ``-s file`` est vraie si ``file`` est le nom d'un répertoire.
 
L'exemple ci-dessous illustre l'utilisation des conditions sur les fichiers :

.. literalinclude:: src/exemple_if_files.sh
   :language: bash

On note l'utilisation du combinateur logique de négation ``!`` pour la troisième condition. Deux autres opérateurs logiques sont disponibles : ``-a`` est le ET logique (AND) et le ``-o`` est le OU logique (OR) :

 - ``-a`` renvoie une valeur positive (faux) si au moins une des deux conditions renvoie une valeur positive, et 0 sinon (vrai);
 - ``-o`` renvoie une valeur positive (faux) si les deux conditions renvoient une valeur positive, et 0 sinon (vrai).

La deuxième et la troisième condition de l'exemple ci-dessus peuvent ainsi être combinées de la manière suivante :

.. literalinclude:: src/exemple_if_files_compact.sh
   :language: bash

La structure ``case`` permet de vérifier une entrée contre une série de motifs. Cela est souvent utile, par exemple, pour l'analyse des paramètres fournis à un script (en utilisant ``-`` et ``--``). La description de ``case`` dépasse cependant le cadre de ce cours.

Scripts : boucles
^^^^^^^^^^^^^^^^^

On utilise régulièrement des boucles pour répéter une opération pour plusieurs argument. Voici un exemple d'utilisation de la boucle ``for`` :

.. literalinclude:: src/exemple_for.sh
   :language: bash

.. literalinclude:: src/exemple_for.sh.out
        :language: console

Une utilisation courante de la boucle ``for`` est pour répéter un même traitement sur tous les fichiers présents dans une liste. La boucle est alors un itérateur : pour chaque itération la variable `s` prend une des valeurs des éléments de la liste séparés par des espaces. 

Cet exemple utilise, par ailleurs, une autre construction utile de `bash(1)`_ : les symboles d'apostrophe inversée ``\```. Ceux-ci permettent d'obtenir le résultat (envoyé sur :term:`stdout`) de l'exécution de la commande qu'il englobent. Examinons en détail cette commande. Celle-ci combine en utilisant un :term:`pipe` les commandes `wc(1)`_ et `cut(1)`_. La première permet d'obtenir le nombre de ligne du fichier fourni en paramètre (utilisation de l'option ``-l``). Toutefois, la sortie de la commande contient trop d'information (par exemple, ``wc -l TP1-Hakim.txt`` renvoie ``      28 TP1-Hakim.txt``). Afin d'isoler l'information qui nous intéressent, l'utilitaire `cut(1)`_ est utilisé. Celui-ci permet ici de sélectionner quelle colonne (la première ici) conserver, lorsque les colonnes sont séparées par des espaces (comme spécifié en utilisant l'option ``-d' '`).

La boucle ``for`` peut aussi prendre comme entrée (liste sur laquelle itérer) une expression utilisant des caractères *joker* ``*`` ou ``?``. `bash(1)`_ transforme alors l'expression en la liste des noms de fichiers et répertoires dans le répertoire courant correspondant à l'expression :

 - ``*`` représente n'importe quelle suite de caractères (y compris la chaîne vide). ``ab*xyz`` correspond à, par exemple, ``abcdxyz`` ou ``abcxyz`` mais pas à ``abcdyz``.
 - ``?`` représente un caractère unique inconnu (mais pas la chaîne vide). ``ab?de`` correspond, ainsi, à ``abcde``, ``abXde`` mais pas à ``abde``.
 
Voici un exemple de l'utilisation du caractère ``*``, qui calcule une signature de chaque fichier sous la forme d'un *hash*  `SHA-1 <https://fr.wikipedia.org/wiki/SHA-1>`_ :

.. literalinclude:: src/exemple_for2.sh
   :language: bash

.. literalinclude:: src/exemple_for2.sh.out
        :language: console

`bash(1)`_ permet aussi l'utilisation de boucles ``while`` et ``until`` sur un principe similaire, mais nous ne les couvrirons pas dans ce cours.

De nombreuses références sont disponibles pour aller plus loin dans la maîtrise de `bash(1)`_ [Cooper2011]_.

.. rubric:: Footnotes

.. [#fexecbit] Sous Unix et contrairement à d'autres systèmes d'exploitation, le suffixe d'un nom de fichier ne joue pas de rôle particulier pour indiquer si un fichier contient un programme exécutable ou non. Comme nous le verrons ultérieurement, le système de fichiers Unix contient des bits de permission qui indiquent notamment si un fichier est exécutable ou non.