# WorkshopReverseEngineering

## Introduction

<img src="https://github.com/Thibauut/WorkshopReverseEngineering/assets/91698852/f179c5db-3c61-446d-958c-af50493d8f88" width="30%" height="30%" alt="Ghidra">

Ce workshop à pour objectif de vous apprendre à utiliser **Ghidra**, en vous initiant au reverse-engineering.
**Ghidra** est un puissant outil développé par la NSA mis récemment à la disposition du public. Cet outil vous permet de décompiler des exécutables afin d’effectuer
une analyse de code d’un fichier binaire.

Dans ce repo github vous y trouverez une archive zip partagée dans laquelle se trouve différents exécutables compilés pour Linux 64 bits et MacOS Silicon.<br/>

Chaque exécutable correspond à un challenge. Lorsque vous lancerez un exécutable vous verrez apparaître dans votre terminal un message vous invitant à réessayer.
L’objectif du workshop est de trouver la bonne façon d’exécuter chaques binaires pour que ceux-ci affichent “Success!”.<br/>

Pour trouver les bonnes façons d’exécuter les binaires et d’avoir la bonne sortie, il faut évidemment faire du reverse-engineering avec l’aide de **Ghidra**.
Les différents challenges sont regroupés par thème, par ordre croissant de difficulté.<br/>

Chaque challenge est indépendant des autres, réussir un challenge n’est pas requis pour tenter de réussir le suivant. Les challenges sont le résultat d’un petit programme écrit en C n'excédant pas 80 lignes.

## Téléchargement et lancement de Ghidra

Pour commencer, installer **Ghidra** en téléchargeant le programme disponible sur https://ghidra-sre.org. Extraire l’archive zip obtenue et lancez avec le programme avec la commande suivante:
```
./ghidraRun
```
Attention, il est obligatoire de posséder l'environnement d'exécution Java (à partir de Java 11).

## Utilisation de Ghidra

Si vous connaissez déjà **Ghidra**, passez cette étape et foncez directement vers les Challenges. Après le lancement de Ghidra, vous obtenez la fenêtre d’ouverture contenant tous les
projets précédemment créés. Au premier lancement il n’y a pas de projet, il faut donc en créer un. Faite le en cliquant sur File > New Project.<br/><br/>

<kbd>
<img width="502" alt="Capture d’écran 2024-02-14 à 14 59 43" src="https://github.com/Thibauut/WorkshopReverseEngineering/assets/91698852/d7dbf948-9b62-4551-9dff-4c14539a5260">
</kbd><br/><br/>

A l’étape suivante, sélectionnez “Non-Shared Project” comme type de projet, puis cliquez sur “Next”.<br/><br/>
<kbd>
<img width="502" alt="Capture d’écran 2024-02-14 à 15 08 25" src="https://github.com/Thibauut/WorkshopReverseEngineering/assets/91698852/ad0cfa96-3db4-4c5a-a78d-bf5894cd858b"><br/>
</kbd><br/><br/>

Sélectionnez ensuite le dossier de sauvegarde de votre projet, ainsi que son nom. Cela peut être ce que vous voulez. Une fois fait, cliquez sur “Finish”.<br/><br/>
<kbd>
<img width="502" alt="Capture d’écran 2024-02-14 à 15 12 12" src="https://github.com/Thibauut/WorkshopReverseEngineering/assets/91698852/ad59c7f4-6868-4c67-a0bd-2e2c51ab6886"><br/>
</kbd><br/><br/>

Maintenant cette étape terminée, votre projet est présent dans la fenêtre d’ouverture. Le projet est actuellement vide, pour ajouter un binaire à examiner, faites “File > Import File”.
Vous pouvez importer autant de fichier que souhaité dans un projet.<br/><br/>
<kbd>
  <img width="502" alt="Capture d’écran 2024-02-14 à 15 14 57" src="https://github.com/Thibauut/WorkshopReverseEngineering/assets/91698852/55262d7d-2467-47e6-8323-382d9cb2523c"><br/>
</kbd><br/><br/>

Dans la fenêtre d’exploration de fichier sélectionnez le fichier à examiner, puis validez le en cliquant sur “Select File to Import” ou en double-cliquant sur le fichier. Une fenêtre d’option doit s’ouvrir, vérifiez que le format du binaire est “ELF” si vous etes sur Linux ou “Mac OS X Mach-O” sur macOS (s'il est proposé si non laissez comme tel) puis cliquez sur “OK”.<br/><br/>

<kbd>
  <img width="502" alt="Capture d’écran 2024-02-14 à 15 19 20" src="https://github.com/Thibauut/WorkshopReverseEngineering/assets/91698852/5d995ed8-af0d-4e7e-9ba7-09136f5d64f5"><br/>
</kbd><br/><br/>

La prochaine fenêtre est seulement informative. Vous pouvez déjà vous renseignez sur l'exécutable ici. Certaines erreurs devraient s’afficher au bas de la fenêtre, ignorez les. Cliquez ensuite sur “OK”.<br/><br/>
<kbd>
  <img width="702" alt="Capture d’écran 2024-02-14 à 15 20 37" src="https://github.com/Thibauut/WorkshopReverseEngineering/assets/91698852/7ee471e9-4adf-40f5-af0b-f38f6888b66c"><br/>
</kbd><br/><br/>

Double cliquez ensuite sur votre fichier importé dans la fenêtre d’ouverture. Le CodeBrowser va s’ouvrir. Au premier lancement Ghidra vous indique si vous souhaitez analyser l'exécutable, choisissez “Yes” évidemment.<br/><br/>
<kbd>
  <img width="502" alt="Capture d’écran 2024-02-14 à 15 22 15" src="https://github.com/Thibauut/WorkshopReverseEngineering/assets/91698852/8a70ef7e-e1a2-4ff1-bf8f-5363a9093437"><br/>
</kbd><br/><br/>

La prochaine fenêtre vous permet de paramétrer ce qui va être analysé. Laissez les paramètres par défaut et cliquez sur “Analyse". S'il y a des erreurs ou des warnings ne les prenez pas en compte et passez a la suite.<br/>
Le CodeBrowser est maintenant 100% opérationnel et vous allez pouvoir analyser l'exécutable<br/><br/>
<kbd>
  <img width="1002" alt="Capture d’écran 2024-02-14 à 15 24 35" src="https://github.com/Thibauut/WorkshopReverseEngineering/assets/91698852/d26b1786-8ee9-47b8-a544-9967140d3d01"><br/>
</kbd><br/><br/>

Sur la partie gauche de la fenêtre se trouve un cadre appelé “Symbol Tree”. Naviguer dans les dossiers présentés pour trouver les informations repérées par **Ghidra** dans l’exécutable. Commencez par trouver la fonction main, puis cliquez dessus.

La partie centrale de la fenêtre contient le cadre appelé “Listing”, il contient toutes les informations du binaire. En se déplaçant et en cliquant dans le cadre Listing, il est possible de visualiser le code correspondant en C dans le cadre de droite.

A droite se trouve le cadre appelé “Decompiler”, il contient un code C généré par **Ghidra** à partir du binaire. A l’aide d’un clic droit, il est possible de modifier des informations dans le code tel que la signature d’une fonction ou le type d’une variable par exemple. Si un cadre est fermé par erreur, il est possible de le réouvrir en le trouvant dans le menu “Window”.

## Challenges

### Thème 1 - Password

#### Challenges 1 à 4
Ces exercices contiennent le mot de passe écrit en brut dans le code. Il suffit juste de trouver un moyen de transmettre le mot de passe au binaire.

### Thème 2 - Chiffrement et offuscation

#### Challenge 5
César lui-même utilisait cette méthode dans ses correspondances secrètes. Faîte attentioncependant, l’humour de ce challenge est très subtile.

#### Challenge 6
En 1995 Microsoft sort officiellement Windows 95. Pour utiliser ce nouveau système d'exploitation, les utilisateurs étaient invités à entrer un code de licence pour éviter les versions piratées. Il se trouve que l’algorithme vérifiant les codes de licences n’est pas très robuste, pouvez-vous le casser ?

#### Challenge 7
Microsoft à appris de son erreur et sort deux nouvelles versions de son système, Windows 95 B et C, avec un tout nouvel algorithme de vérification de code de licence. Vous pensez vraiment que cet algorithme est robuste cette fois-ci ?

### Thème 3 - Tricks

#### Challenge 8
Dans ce challenge il vaut faudra un peu de chance, ou un peu de ruse.

#### Challenge 9
https://www.youtube.com/watch?v=HodRJ1cdW-0
