# Outils de textométrie 

Ce script propose des outils de textométrie utilisables sur un corpus de textes en format structuré, téléchargés via le script ModOAP_Telechargement_structure_texte_doc_Gallica

Le corpus est attendu sous la forme d'un dossier sur un Google Drive contenant un fichier .json par document du corpus.

Le corpus doit être pré-traité lors de la première utilisation grâce à la cellule Prétraiter un dossier corpus.

Il nécessite de synchroniser un compte Google Drive.

La détection de mise en page utilise l'outil Layout Parser décrit sur https://github.com/Layout-Parser/layout-parser

Ce carnet utilise majoritairement la bibliothèque de TAL Spacy (https://spacy.io/)

## Utilisation

### Préparation du corpus

1. Ouvrir le carnet dans l'interface Google Colab et se connecter à un compte Google Drive 

2. Lancer la première cellule "Préparation du script et synchronisation d'un Google Drive" et cliquer sur le lien généré pour synchroniser un compte Drive si demandé.
Cette cellule importe les bibliothèques nécessaires à l'utilisation du carnet, et connecte un compte Drive.

3. Préparer un corpus : un dossier sur le drive contenant directement les documents au format .json (un document par fichier)
Si un corpus a déjà été pré-traité

4. Renseigner le chemin vers le dossier Google Drive contenant le corpus dans la cellule "Prétraiter un dossier corpus", puis lancer la cellule. 
Cette cellule crée dans le dossier un fichier .nlp par document .json. Si le corpus a déjà été pré-traité par ce script et que les fichiers .nlp sont déjà présents dans le dossier, cette cellule peut être passée et le corpus peut être directement importé dans la cellule suivante.

5. Renseigner le chemin vers le dossier Google Drive contenant le corpus dans la cellule "Importer un dossier corpus prétraité", puis lancer la cellule.

Une fois le corpus importé, les calculs peuvent être opérés au choix.

### Recherche par terme

- **Choix des pré-traitements pour le calcul des occurrences les plus répandues**:
Cette cellule précise les pré-traitements linguistiques opérés uniquement pour le calcul de la cellule suivante "Fréquences des termes les plus présents dans le corpus". 
Deux traitements au choix : 
mots_grammaticaux = filtre des mots grammaticaux autres que les noms, adjectifs, verbes, participes et adverbes
lemmatisation = généralisation des verbes à leur forme infinitive et des noms, pronoms, déterminants et adjectifs au masculin singulier

- **Fréquences des termes les plus présents dans le corpus** :
Préciser le nombre des termes les plus fréquents à afficher et lancer la cellule. 
Cette cellule se base sur les pré-traitements définis dans la cellule précédente. 

- **Evolution du nombre d'occurrences de termes au fil du temps** :
Entrer entre 1 et 4 termes dans les champs correspondants, puis lancer la cellule pour obtenir un graphique des occurrences de ces termes en fonction des années des documents du corpus.

- **Calcul des cooccurrences pour un terme** :
	- Spécifier un terme en requête
	- Spécifier la direction du voisinage considéré (gauche ou droit)
	- Spécifier le nombre de cooccurrences à afficher
	- Lancer la cellule
Cette cellule filtre les mots grammaticaux uniquement 

- **Calcul des cooccurrences pour un terme en fonction des relations syntaxiques** :
	- Spécifier un terme
	- Spécifier le nombre de cooccurrences à afficher
	- spécifier la nature de la relation syntaxique
Similaire à la cellule précédente, mais n'affiche que les cooccurrences associées à la relation syntaxique spécifiée :
La relation dépendants_syntaxiques affiche les cooccurrences qui dépendent de la requête (ex : un adjectif qualificatif qui dépend d'un nom)
La relation tete_syntaxique affiche les cooccurrences dont dépend la requête (ex : un nom dont dépend un adjectif ou un verbe dont dépend un nom)

- **Calcul des syntagmes nominaux les plus fréquents contenant un terme donné** :
	- Spécifier un terme
	- Spécifier le nombre de syntagmes à afficher
Cette cellule affiche les syntagmes nominaux (principalement les groupes nominaux) comprenant le terme donné en requête. Permet notamment d'observer les différentes formes que peut prendre un nom dans le corpus. 

### Recherche par patrons morphosyntaxiques :

1. **Construction du patron**
Construire le patron dans cette cellule pour pouvoir lancer les calculs des deux cellules suivantes. 

	- Spécifier un patron dans le champ **patron** comprenant 1 à 4 termes (texte, lemme ou catégorie grammaticale).
	- Préciser le type de chaque terme dans les champs en dessous 
	- Lancer la cellule
	
TEXT = le texte précis du terme
LEMMA = la forme lemmatisée du terme
POS = la catégorie grammaticale du terme selon le code Universal Dependencies précisé dans le carnet.
VIDE = si moins de 4 termes

- **Fréquences des segments correspondant au patron les plus répandus dans le corpus**
Cette cellule nécessite que le patron ait été constitué dans la cellule précédente.

	- Spécifier le nombre de segments max à afficher
	- Lancer la cellule

- **Analyse des concordances du patron**
Cette cellule nécessite que le patron ait été constitué dans la cellule "Construction du patron".
	- Préciser la fenêtre de voisinage pour l'affichage du patron (nombre de mots à gauche et à droite du patron à considérer)
	- Lancer la cellule
	
### Similarité vectorielle

1. **Segmentation du corpus en phrases et vectorisation du lexique**
Segmenter et vectoriser le corpus dans cette cellule pour pouvoir lancer les calculs des deux cellules suivantes. 
Lancer cette cellule. 

- **Calcul des termes dont les vecteurs sont les plus proches d'un terme donné en requête**
	- Spécifier un terme présent dans le corpus
	- Spécifier le nombre de termes sémantiquement similaires à afficher
	- Lancer la cellule
