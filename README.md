# diamonds
Browsable BPMN documentation, assorted with IST test cases

Script pour assurer la cohérence entre tests IST et documentation (Firefox only) :

doc/ForApproval/index2.html?state=&svgTarget=CustomerLifecycle


PRODUCTION ET CONSULTATION DE LA DOCUMENTATION 

Les graphes BPMN sont produits avec Camunda modeler et exportés en svg dans un folder unique.

Grâce à une convention stricte sur les noms de fichiers, les références entre graphes sont gérées par un script qui établit dynamiquement les liens en scannant le repository avant d'afficher chaque svg.

Les documents manquants apparaissent en rouge, les documents disponibles en vert. Les cases vertes sont cliquables.

De la sorte : 
- On peut browser la documentation sans avoir à maintenir un système de liens.
- On voit clairement ce qui manque.
- Il suffit de modifier les svg pour mettre le système à jour.

L'adresse web se met à jour quand on navigue (query string), on peut dès lors partager des urls de documents spécifiques.

On dispose de boutons home / back / forward et d'un breadcrumb pour faciliter la navigation entre graphes.


STATUT DE LA DOCUMENTATION : WORKFLOW DE VALIDATION

A droite du breadcrumb, on voit le statut de chaque document : draft (orange), approved (vert), rework (magenta) :

doc/ForApproval/index2.html?state=&svgTarget=VirtualCard

Si on clique sur le status, on obtient les noms des auteurs, ainsi que des personnes responsables des approvals reçus et à recevoir : 

doc/ForApproval/index2.html?state=status&svgTarget=VirtualCard

Cette ligne est extraite d'une table de statut, table qui pour le moment doit être maintenue indépendamment des BPMN (Je n'ai pas trouvé comment la norme XML de BPMN ou Camunda Modeler pourraient permettre de stocker ces infos au niveau du document lui-même, mais je n'ai pas dit mon dernier mot.)

La table peut être consultée en ligne : il suffit de cliquer sur "Documentation Progress" à droite :

doc/ForApproval/index2.html?state=progress&svgTarget=VirtualCard

La table est maintenue à l'aide de Excell et enregistrée en XML. Pour l'instant on ne dispose pas de schéma pour la valider mais il faut respecter le format pour que ça fonctionne.


GESTION DES TESTS IST : 

Chaque ligne de statut est conçue pour implémenter la méthode Diamond : un fichier Excell au format IST pour chaque workflow BPMN, puis un fichier Excell pour chaque test case à exécuter ou à automatiser.

Exemple :

Un workflow :
doc/ForApproval/index2.html?state=&svgTarget=ConfirmRate

Son status avec trois références (visibles dans les 2 colonnes de droite) :
doc/ForApproval/index2.html?state=status&svgTarget=ConfirmRate

Une référence à la matrice IST : 
doc/ForApproval/confirmRate_ist.xlsx

Deux test cases ( dans cette matrice, seuls deux test cases ont été documentés : les cas 'Happy' et 'RejectRate' ) :
doc/ForApproval/confirmRate_happy_tst.xlsx
doc/ForApproval/confirmRate_rejectRate_tst.xlsx

Les noms des fichiers Excel pour les IST et pour les test cases sont normalisés, de sorte que les références sont maintenues dans le fichier d'ensemble à l'aide de simples mots-clés.


EVOLUTIONS :

Dans l'idéal, on devrait ajouter deux colonnes à droite de la table des status.

1 - Référence aux documents de projets disponibles : specs, résultats de tests, etc.
2 - Liens vers les tests automatisés, dans les différents environnements.

Certains starting points BPMN (cercles blancs) figurant dans les graphes comprennent les urls qui pointent, sur la plateforme à tester, vers le début des use cases décrits par ces mêmes graphes. Il serait possible de rendre cliquables ces urls, pour pouvoir accéder à chaque use case tout en lisant la doc.

**********
