# [Kaggle Tweet Sentiment Extraction Competition](https://www.kaggle.com/c/tweet-sentiment-extraction/leaderboard): 1st place solution (Dark of the Moon team) 

Ce repository contient les solutions détaillées qui ont remporté la première place au concours de kaggle appelé "Tweet Sentiment Extraction" il y a 5 mois.

  ## Présentation de la compétition ##
  ## Présentation de la solution ##

   ### Tkenisation ###
**Qu'est-ce qu'un tokeniser ?**
Un tokenizer reçoit un flux de caractères, le décompose en tokens individuels (généralement des mots individuels) et produit un flux de tokens. Par exemple, un tokenizer d'espacement décompose le texte en tokens chaque fois qu'il voit un espacement. Il convertit le texte "Quick brown fox !" en termes ["Quick",  "brown", " fox !"].

![alt text](https://camo.githubusercontent.com/541a5e3521cf5b4c84c7ced36628841d8e66d58b7f2e51cded099a18c006d4e9/68747470733a2f2f68756767696e67666163652e636f2f6c616e64696e672f6173736574732f746f6b656e697a6572732f746f6b656e697a6572732d6c6f676f2e706e67)
Développé par huggingdace, propose une implémentation des tokenizers les plus utilisés aujourd'hui, en mettant l'accent sur les performances et la polyvalence

Extrêmement rapide (à la fois pour l'entraînement et la tokenisation), grâce à l'implémentation de Rust. Il faut moins de 20 secondes pour tokeniser un Go de texte sur l'unité centrale d'un serveur.
  - Facile à utiliser, mais aussi extrêmement polyvalent.
  - Conçu pour la recherche et la production.
  - La normalisation s'accompagne d'un suivi des alignements. Il est toujours possible d'obtenir la partie de la phrase originale qui correspond à un jeton donné.
  - Effectue tout le prétraitement : Tronquer, Tamponner, ajouter les tokens spéciaux dont votre modèle a besoin.
  
  
  
  
  
  ## [Plus de détails]
Ils ont fait un discours sur leur solution lors du meetup ODS Paris: [YouTube link](https://www.youtube.com/watch?v=S7soN-y5WMg)<br />
La présentation de leur solution : [SlideShare link](https://www.slideshare.net/ArtsemZhyvalkouski/kaggle-tweet-sentiment-extraction-1st-place-solution)
