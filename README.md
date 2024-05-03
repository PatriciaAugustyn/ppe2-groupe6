# Manuel d'utilisateur

### Recommandation

Avant de commencer, il faudra s'assurer d'avoir installer Python et mettre à jour la liste des paquets en utilisant la commande:

```
sudo apt update
```

Ensuite, installez Python 3 en tapant la commande:
```
sudo apt install python3
```

Ensuite, pour utiliser les programmes, nous vous recommandons de créer un environnement virtuel pour installer les libraires :
```
python3 -m venv venv

source venv/bin/activate
```

Ensuite, vous pouvez installer les librairies :
```
pip install python-dateutil feedparser spacy stanza
```

Puis installer, le package utilisé dans le script pour SpaCy :

```
python3 -m spacy download fr_core_news_sm

python3 -m spacy download fr_core_news_lg
```

Pour utiliser la librairie Trankit, nous vous recommandons d'appliquer ces lignes de commandes pour favoriser l'utilisation  :

```
git clone git@github.com:nlp-uoregon/trankit.git
cd trankit
pip install .
```

Installer la librairie Networkx dans l'environnement virtuel :

```pip install networkx[default]```

Cette commande installe aussi les paquets : pytz, tzdata, scipy, pyparsing, pillow, kiwisolver, fonttools, cycler, contourpy, pandas, matplotlib. Si vous ne souhaitez pas installer  les librairies associées :

```pip install networkx```

---------

Pour utiliser ElementTree (etree), vous n'avez pas besoin d'installer quoi que ce soit séparément car il s'agit d'un module intégré à la bibliothèque standard de Python. Cela signifie qu'il est disponible dès l'installation de Python et ne nécessite pas d'installation supplémentaire.
pour ce qui est des options:

- nous avons le choix pour l'outil de lecture du corpus entre:
```
 -r {etree,feedparser}
```

- nous avons l'option pour le nom du fichier de sortie:
```
 -o OUTPUT_FILE
```

Pour lire un flux unique avec etree:

```
python3 read_corpus.py chemin_vers_le_fichier -o fichier_sortie.xml  -r etree
```

Pour lire un flux unique avec feedparser:
```
python3 read_corpus.py chemin_vers_le_fichier -o fichier_sortie.xml  -r feedparser
```

---------------

Pour lire un flux de corpus RSS avec etree:
```
python3 read_corpus.py chemin_vers_le_corpus -o fichier_sortie.xml  -r etree
```

Pour lire un flux de corpus avec feedparser:
```
python3 read_corpus.py chemin_vers_le_corpus -o fichier_sortie.xml  -r feedparser
```

Pour appliquer les filtres nous avons le choix entre ces options:

- Pour afficher le résultat sur le terminal:
```
[--print_to_stdout]
```

- Pour le choix de l'outil de parcours du corpus:
```
[-i {glob}]
```

- Pour le filtre de la date de début:
```
[-s START_DATE]
```

- Pour le filtre de la date de fin:
```
[-e END_DATE]
```

- Pour le filtre de la catégorie:
```
[-c [CATEGORIES ...]]
```

- Pour le filtre de la source
```
[--sources [SOURCES ...]]
```

Pour lancer le programme **read_corpus.py**, vous pouvez lancer ces lignes de commande :
```
python3 read_corpus.py chemin_vers_le_corpus -z xml -o fichier_sortie.xml -r feedparser -i glob -s 2024-02-11 -e 2024-02-12 -c Sports --source Figaro
```

```
python3 read_corpus.py chemin_vers_le_corpus -o fichier_sortie.xml  -r etree -i glob -s 2024-01-26 -e 2024-01-29  --source France Info
```

------------------------------------------

Pour utiliser les modules json et pickle en Python aucune action n'est nécessaire car ils sont inclus dans la bibliothèque standard de Python, ce qui signifie qu'ils sont disponibles dès que vous avez une installation de Python fonctionnelle.
Nous avons le choix entre ces options:

- Pour sérialiser:
```
[-z {json,pickle,xml}]
```

- Pour désérialiser
```
[-l {json,pickle,xml}]
```
Pour lancer le programme **read_corpus.py** pour la sérialisation, vous pouvez lancer ces lignes de commande :

```
python3 read_corpus.py chemin_vers_le_dossier -z pickle -o test-output.pkl -r feedparser -i glob -c Politique --sources Figaro
python3 read_corpus.py chemin_vers_le_dossier -z json -o test-output.json -r feedparser -i glob -c Politique --sources Figaro
python3 read_corpus.py chemin_vers_le_dossier -z xml -o test-output.xml -r etree -i glob -c Politique --sources Figaro
```

Tandis que pour la désérialisation, nous avons les lignes de commandes suivantes:
```
python3 read_corpus.py chemin/vers/le/fichier.json -l json
python3 read_corpus.py chemin/vers/le/fichier.pickle -l pickle
python3 read_corpus.py chemin/vers/le/fichier.xml -l xml
```

---------------------

Pour lancer les programmes **demo_xxx.py**, vous pouvez lancer ces lignes de commande :

```
python3 demo_spacy.py
python3 demo_trankit.py
python3 demo_stanza.py
```

> Les scripts de démo vous permettent d'introduire les outils d'analyse morphosyntaxique (Stanza | SpaCy | Trankit), afin de récupérer pour un texte chaque token. Par exemple, vous obtiendrez la forme, le lemme et la partie du discours.

Pour lancer le script **analyzers.py**, vous pouvez lancer ces lignes de commande :

```
python3 analyzers.py output.json -l json -s json -o analyzed_stanza-corpus.json -a stanza
python3 analyzers.py output.xml -l xml -s xml -o analyzed_stanza-corpus.xml -a stanza
python3 analyzers.py output.pkl -l pickle -s pickle -o analyzed_stanza-corpus.pkl -a stanza

analyzers.py [-h] [-l {json,pickle,xml}] [-s {json,pickle,xml}] [-o OUTPUT_FILE]
                    [-a {spacy,stanza,trankit}]
                    input_file
```

> Ce script permet d'obtenir une version du corpus qui, pour chaque article, contient le résultat des analyses de l'outil Stanza.

Les arguments de ce programme sont :

- "input_file" : fichier d'entré en format sérialisé
- "-l", "--load-serialized" : extension du fichier d'entré
- "-s", "--save-serialized" : format de sortie
- "-o", "--output-file" : nom du fichier de sortie
- "-a", "--analyzer" : choix de l'analyseur (stanza, spacy, trankit)

----------------------

Pour lancer les programmes **demo_deps_xxx.py**, vous pouvez lancer ces lignes de commande :

```
python3 demo_deps_stanza.py
python3 demo_deps_spacy.py
python3 demo_deps_trankit.py
```

> Ces scripts permettent d'analyser un texte en obtenant des informations sur les dépendant, les gouverneurs et la nature du lien.

Pour lancer le programme **analyzers.py**, vous pouvez lancer ces lignes de commande :
```
python3 analyzers.py output.json -l json -s json -o analyzed_stanza-corpus.json -a stanza
```

> Ce script intégrera les dépendances syntaxiques fournies par Stanza et mettra à jour la sérialization json

Exemple de **commande bash** pour combiner plusieurs fonctions :

```
python3 read_corpus.py chemin_vers_le_corpus -z json -o output.json -r feedparser -i glob -c Politique --sources Figaro | python3 analyzers.py output.json -l json -s json -o analyzed_stanza-corpus.json -a stanza python3 patterns.py analyzed_stanza-corpus.json -l json
```

> Cette commande permet de charger un corpus précédemment sauvegardé, l’analyse avec Stanza outils et sauvegarde le résultat.

-------------------------------------

Pour lancer le programme **patterns.py**, vous pouvez lancer cette ligne de commande :

```
python patterns.py analyzed_stanza-corpus.json -l json

patterns.py [-h] [-l {json,pickle,xml}] input_file
```

> Cette commande charge le corpus sauvegardé au format json, extrait des patrons et sauvegarde le résultat sous un csv.

Les arguments possibles sont :

- "input_file" : le corpus sérialisé à insérer
- "-l", "--load-serialized" : format des données d'entrées


------------------------

Pour lancer le programme **visualisation.py**, vous pouvez lancer la ligne de commande :

```
python3 visualisation.py -c exemple-information_mutuelle.tsv -n VERB-prendre-obj -s 5 -lu oui -ha oui

visualisation.py [-h] [-c CORPUS] [-n NOEUD] [-s SEUIL] [-ha {oui,non}] [-lu {oui,non}]
```

> Cette commande permet de créer un fichier XML avec l'extension .gexf, permet de créer un graphe personnalisé en fonction des arguments sités ci-dessous.
> Le graphe sortant de cette commande contiendra les éléments suivants : le noeud de départ est VERB-prendre-obj, tout les éléments ont une information mutuelle supérieure ou égale à 5, les hapax et liens uniques sont gardés. Afin de visualiser le graphe vous pouvez l'ouvrir dans Gephi Lite.

Les arguments de ce programme sont :

- "-c", "--corpus" : Indiquer le corpus d'entrée sous format tsv.
- "-n", "--noeud" : Indiquer le noeud principal du graphe souhaité. Veuillez l'indiquer sous la forme POS-lemme-relation, ex : NOUN-avion-nmod ou VERB-lutter-contre.
- "-s", "--seuil" : Indiquer le seuil minimum d'information mutuelle.
- "-ha", "--hapax" : Indiquer si on souhaite prendre les hapax (lemme présent qu'une seule fois dans le corpus). 'oui' indique la présence d'hapax, 'non' l'inverse.
- "-lu", "--lien-unique" : Indiquer si on souhaite prendre les patterns présents qu'une seule fois. 'oui' indique la présence de lien unique, 'non' l'inverse.


Pour lancer le programme **visualisation_networks.py**, vous pouvez lancer la ligne de commande :

```
python3 visualisation_networkx.py -c ../exemple-information_mutuelle.tsv -s 5 --hapax --lien-unique -o mon_graphe.gexf -n VERB-prendre-obj

visualisation_networkx.py [-h] -c CORPUS [-s SEUIL] [--hapax] [--lien-unique] -o OUTPUT -n NOEUD
```

> Ce programme fait la même chose que le précèdent avec la librairie networkx.

Les arguments sont :

- "-c", "--corpus" : Chemin vers le fichier corpus TSV.
- "-s", "--seuil" : Seuil minimum d'information mutuelle.
- "--hapax" : Appliquer le filtre hapax.
- "--lien-unique" : Appliquer le filtre de liens uniques.
- "-o", "--output" : Chemin du fichier de sortie GEXF.
- "-n", "--noeud" : Noeud central sous forme CATEGORIE-LEMME-RELATION.


Pour lancer le programme **build_graph.py**, vous pouvez lancer la ligne de commande :

```
python3 build_graph.py -c VERB-prendre-obj -s 2 -i 5 -u -f ../exemple-information_mutuelle.tsv graphe.gexf

build_graph.py [-h] [-c C] [-s S] [-i I] [-u] [-f] input_file output_file
```

> Ce programme est le plus performant et remplie toutes les attentes dans la production des graphes.

Les arguments de ce programme sont :

- "input_file" : tableau avec les IM
- "output_file" : fichier de sortie en gexf
- "-c" : nœud cible de départ
- "-s" : nombre de pas dans le graphe (steps)
- "-i" : information mutelle minimum
- "-u" : filtre les relations uniques
- "-f" : filtre les feuilles
