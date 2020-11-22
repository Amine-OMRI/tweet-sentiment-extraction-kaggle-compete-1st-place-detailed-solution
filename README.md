# [Kaggle Tweet Sentiment Extraction Competition](https://www.kaggle.com/c/tweet-sentiment-extraction/leaderboard): 1st place solution (Dark of the Moon team) 

Ce repository contient les solutions détaillées qui ont remporté la première place de la compétition kaggle appelé "Tweet Sentiment Extraction" il y a 5 mois.

  ## Présentation de la compétition 
  La compétition portait sur l'extraction de sentiments, ci-dessous un résumé sur le sujet :

"Mon chien ridicule est incroyable." [sentiment : positif]</br>
Avec tous les tweets qui circulent à chaque seconde, il est difficile de dire si le sentiment derrière un tweet spécifique aura un impact sur la marque d'une entreprise ou d'une personne parce qu'il est viral (positif), ou s'il dévastera les profits parce qu'il a un ton négatif. Il est important de saisir les sentiments dans la langue, à un moment où les décisions et les réactions sont créées et mises à jour en quelques secondes. Mais quels mots conduisent réellement à la description des sentiments ? Dans cette compétition, l'objectif est de choisir la partie du tweet (mot ou phrase) qui reflète le sentiment.
Quels mots des tweets reflètent un sentiment positif, négatif ou neutre ? tout en utilisant les outils d'apprentissage automatique ?</br>
Dans ce concours, ils ont extrait les phrases de la plateforme ["Data for Everyone"](https://appen.com/resources/datasets/). L'ensemble de données est intitulé "Analyse du sentiment": Emotion in Text".</br>
L'objectif de ce concours est de construire un modèle qui peut faire la même chose - examiner le sentiment étiqueté pour un tweet donné et déterminer quel mot ou phrase le soutient le mieux.</br>
   ### Evaluation
La métrique utilisée dans cette compétition est le score Jaccard au niveau des mots. Vous trouverez ici une bonne description de la similarité de Jaccard pour les chaînes de caractères.

Une implémentation Python basée sur les liens ci-dessus:
```ruby
def jaccard(str1, str2): 
    a = set(str1.lower().split()) 
    b = set(str2.lower().split())
    c = a.intersection(b)
    return float(len(c)) / (len(a) + len(b) - len(c))
```
La similarité ou l'intersection Jaccard sur l'union est définie comme la taille de l'intersection divisée par la taille de l'union de deux ensembles. Prenons l'exemple de deux phrases :
-Phrase 1 : AI is our friend and it has been friendly
-Phrase 2 : AI and humans have always been friendly
![alt text](https://miro.medium.com/max/463/1*u2ZZPh5er5YbmOg7k-s0-A.png)



  ## Présentation de la solution 

   ### Tkenisation 
**Qu'est-ce qu'un tokeniser ?**
Un tokenizer reçoit un flux de caractères, le décompose en tokens individuels (généralement des mots individuels) et produit un flux de tokens. Par exemple, un tokenizer d'espacement décompose le texte en tokens chaque fois qu'il voit un espacement. Il convertit le texte "Quick brown fox !" en termes ["Quick",  "brown", " fox !"].

![alt text](https://camo.githubusercontent.com/541a5e3521cf5b4c84c7ced36628841d8e66d58b7f2e51cded099a18c006d4e9/68747470733a2f2f68756767696e67666163652e636f2f6c616e64696e672f6173736574732f746f6b656e697a6572732f746f6b656e697a6572732d6c6f676f2e706e67)
Développé par huggingdace, propose une implémentation des tokenizers les plus utilisés aujourd'hui, en mettant l'accent sur les performances et la polyvalence

Extrêmement rapide (à la fois pour l'entraînement et la tokenisation), grâce à l'implémentation de Rust. Il faut moins de 20 secondes pour tokeniser un Go de texte sur l'unité centrale d'un serveur.
  - Facile à utiliser, mais aussi extrêmement polyvalent.
  - Conçu pour la recherche et la production.
  - La normalisation s'accompagne d'un suivi des alignements. Il est toujours possible d'obtenir la partie de la phrase originale qui correspond à un jeton donné.
  - Effectue tout le prétraitement : Tronquer, Tamponner, ajouter les tokens spéciaux dont votre modèle a besoin.
  
  
  
  
  
  ## Pour plus de détails sur leur solution
Ils ont fait un discours sur leur solution lors du meetup ODS Paris: [YouTube link](https://www.youtube.com/watch?v=S7soN-y5WMg)<br />
La présentation de leur solution : [SlideShare link](https://www.slideshare.net/ArtsemZhyvalkouski/kaggle-tweet-sentiment-extraction-1st-place-solution)
