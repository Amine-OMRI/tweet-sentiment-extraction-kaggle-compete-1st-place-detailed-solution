# [Kaggle Tweet Sentiment Extraction Competition](https://www.kaggle.com/c/tweet-sentiment-extraction/leaderboard): 1st place solution (Dark of the Moon team) 

Ce repository contient la solution détaillée qui ont remporté la première place de la compétition kaggle appelé "Tweet Sentiment Extraction" il y a 5 mois.
  ### l'équipe qui a remporté la compétition, composée de:
   [Heartkilla](https://www.kaggle.com/aruchomu): Artsem Zhyvalkouski Data Scientist</br>
   [Hikkiiii](https://www.kaggle.com/wochidadonggua): Hikkiiii NLP Data scientist Beijing, Beijing, China</br>
   [Theo](https://www.kaggle.com/theoviel): Théo Vie Chercheur scientifique à Paris, Île-de-France, Franc</br>
   [Cl_ev](https://www.kaggle.com/cl2ev1): Anton travaille dans l'IT London, England, United Kingdom</br>
 ### Le notebook ["roberta_base.ipynb"](https://github.com/Amine-OMRI/tweet-sentiment-extraction-kaggle-compete-1st-place-detailed-solution/blob/main/roberta_base.ipynb) représente l'un des modèles de premier niveau réalisé par [Heartkilla](https://www.kaggle.com/aruchomu) : Artsem Zhyvalkouski le code source est sous `src/1st_level/roberta_base/` sur le [repo git](https://github.com/heartkilla/kaggle_tweet/tree/master/src/1st_level/roberta_base) où ils ont mis le code de leur solution</br>
 
 ## Présentation de la compétition 
   La compétition portait sur l'extraction de sentiments, ci-dessous un résumé sur le sujet :

  "My ridiculous dog is amazing." [sentiment: positive]</br>
  Avec tous les tweets qui circulent à chaque seconde, il est difficile de dire si le sentiment derrière un tweet spécifique aura un impact sur la marque d'une     entreprise ou d'une personne parce qu'il est viral (positif), ou s'il dévastera les profits parce qu'il a un ton négatif. Il est important de saisir les           sentiments dans la langue, à un moment où les décisions et les réactions sont créées et mises à jour en quelques secondes. Mais quels mots conduisent réellement   à la description des sentiments ? Dans cette compétition, l'objectif est de choisir la partie du tweet (mot ou phrase) qui reflète le sentiment.
  Quels mots des tweets reflètent un sentiment positif, négatif ou neutre ? tout en utilisant les outils d'apprentissage automatique ?</br>
  Dans ce concours, ils ont extrait les phrases de la plateforme ["Data for Everyone"](https://appen.com/resources/datasets/). L'ensemble de données est intitulé   "Analyse du sentiment": Emotion in Text".</br>
  L'objectif de ce concours est de construire un modèle qui peut faire la même chose - examiner le sentiment étiqueté pour un tweet donné et déterminer quel mot     ou phrase le soutient le mieux.</br>
   ### Tâche
   - Pour un tweet donné, prédire quel mot ou quelle phrase reflète le mieux le sentiment étiqueté
   ### Data
  ○ Train: 27k tweets</br>
  ○ Public / private test: 4k / 8k tweets 
  | Texte (donné) | Sentiment (donné) | texte_sélectionné (target) |
  | :---: | :---: | :---: |
  | J'aime beaucoup la chanson Love Story de Taylor Swift | positive | j'aime |
  | je dois récupérer mon ordinateur réparé | neutre | je dois récupérer mon ordinateur réparé |
  | trop triste, tu vas me manquer ici à San Diego ! ! | négatif | trop triste | </br>
  
  </br>Fichiers
  - train.csv - Le jeux de données d'entrainement
  - test.csv - Le jeux de données de test 
  - sample_submission.csv - un exemple de fichier de soumission dans le format correct</br>
  
  Colonnes
  - textID - un identifiant unique pour chaque fragment de texte</br>
  - text - Le texte du tweet</br>
  - sentiment - le sentiment général du tweet</br>
  - selected_text - (Que pour les données d'entrainement) le texte qui reflète le sentiment du tweet</br>
  
   ### Evaluation
  La métrique utilisée dans cette compétition est le [score Jaccard](https://en.wikipedia.org/wiki/Jaccard_index) au niveau des mots. Vous trouverez [ici](https://towardsdatascience.com/overview-of-text-similarity-metrics-3397c4601f50) une bonne description de la similarité de Jaccard pour les chaînes de caractères.</br>
  ![alt text](https://neo4j.com/docs/graph-algorithms/current/images/jaccard.png)

  Une implémentation Python basée sur les liens ci-dessus:
  ```ruby
  def jaccard(str1, str2): 
      a = set(str1.lower().split()) 
      b = set(str2.lower().split())
      c = a.intersection(b)
      return float(len(c)) / (len(a) + len(b) - len(c))
  ```
  La similarité ou l'intersection Jaccard sur l'union est définie comme la taille de l'intersection divisée par la taille de l'union de deux ensembles. Prenons     l'exemple de deux phrases :</br>
  - Phrase 1 : AI is our friend and it has been friendly</br>
  - Phrase 2 : AI and humans have always been friendly</br>
  ![alt text](https://miro.medium.com/max/463/1*u2ZZPh5er5YbmOg7k-s0-A.png)</br>
  ==> Pour les deux phrases ci-dessus, nous obtenons une similarité Jaccard de 5/(5+3+2) = 0,5 qui est la taille de l'intersection de l'ensemble divisée par la   taille totale de l'ensemble.


 ## Présentation de la solution 
  Pratiquement toutes les tâches de l'NLP sont maintenant résolues à l'aide des Transformers et Cette solution est aussi basée sur ces derniers.
  - Les transformateurs (Transformers) tels que BERT, RoBERTa, BART, CamemBERT etc. sont devenus l'état de l'art en NLP
  - pré-entraînés sur une grande quantité de textes
  - Un peu long à entraîner
  - Peut être utilisé pour ces tâches dans le cadre du NER (Reconnaissance d'entités nommées (Named-entity recognition)) ou de l'QA (Question Answering)
  - la solution basée sur la QA a donné les meilleurs résultats

   ![alt text](https://raw.githubusercontent.com/huggingface/transformers/master/docs/source/imgs/transformers_logo_name.png)</br>
   
   l'etat de l'art pour le traitement de langage naturel de pour Pytorch et TensorFlow 2.0 </br>
   🤗 Transformers (anciennement connu sous le nom de pytorch-transformers et pytorch-pretrained-bert) fournit des architectures à usage général (BERT, GPT-2, RoBERTa, XLM, DistilBert, XLNet...) pour la compréhension du langage naturel (TALN / NLP) et la génération du langage naturel (NLG) avec plus de 32 modèles pré-entraînés dans plus de 100 langues et une interopérabilité profonde entre TensorFlow 2.0 et PyTorch.</br>
   🤗 Transformers fournit des milliers de modèles pré-entrainés pour effectuer des tâches sur des textes telles que la classification, l'extraction d'informations, la réponse à des questions (QA), le résumé, la traduction, la génération de texte, etc. dans plus de 100 langues. </br>
   voici la [documentation](https://github.com/huggingface/transformers) des transformers sur leur repo github.</br>
   Ci-dessous, quelques exemples :
  - [Masked word completion with BERT](https://huggingface.co/bert-base-uncased?text=Paris+is+the+%5BMASK%5D+of+France)
  - [Name Entity Recognition with Electra](https://huggingface.co/dbmdz/electra-large-discriminator-finetuned-conll03-english?text=My+name+is+Sarah+and+I+live+in+London+city)
  - [Text generation with GPT-2](https://huggingface.co/gpt2?text=A+long+time+ago%2C+)
  - [Natural Langugage Inference with RoBERTa](https://huggingface.co/roberta-large-mnli?text=The+dog+was+lost.+Nobody+lost+any+animal)
  - [Summarization with BART](https://huggingface.co/facebook/bart-large-cnn?text=The+tower+is+324+metres+%281%2C063+ft%29+tall%2C+about+the+same+height+as+an+81-storey+building%2C+and+the+tallest+structure+in+Paris.+Its+base+is+square%2C+measuring+125+metres+%28410+ft%29+on+each+side.+During+its+construction%2C+the+Eiffel+Tower+surpassed+the+Washington+Monument+to+become+the+tallest+man-made+structure+in+the+world%2C+a+title+it+held+for+41+years+until+the+Chrysler+Building+in+New+York+City+was+finished+in+1930.+It+was+the+first+structure+to+reach+a+height+of+300+metres.+Due+to+the+addition+of+a+broadcasting+aerial+at+the+top+of+the+tower+in+1957%2C+it+is+now+taller+than+the+Chrysler+Building+by+5.2+metres+%2817+ft%29.+Excluding+transmitters%2C+the+Eiffel+Tower+is+the+second+tallest+free-standing+structure+in+France+after+the+Millau+Viaduct)
  - [Question answering with DistilBERT](https://huggingface.co/distilbert-base-uncased-distilled-squad?text=Which+name+is+also+used+to+describe+the+Amazon+rainforest+in+English%3F&context=The+Amazon+rainforest+%28Portuguese%3A+Floresta+Amaz%C3%B4nica+or+Amaz%C3%B4nia%3B+Spanish%3A+Selva+Amaz%C3%B3nica%2C+Amazon%C3%ADa+or+usually+Amazonia%3B+French%3A+For%C3%AAt+amazonienne%3B+Dutch%3A+Amazoneregenwoud%29%2C+also+known+in+English+as+Amazonia+or+the+Amazon+Jungle%2C+is+a+moist+broadleaf+forest+that+covers+most+of+the+Amazon+basin+of+South+America.+This+basin+encompasses+7%2C000%2C000+square+kilometres+%282%2C700%2C000+sq+mi%29%2C+of+which+5%2C500%2C000+square+kilometres+%282%2C100%2C000+sq+mi%29+are+covered+by+the+rainforest.+This+region+includes+territory+belonging+to+nine+nations.+The+majority+of+the+forest+is+contained+within+Brazil%2C+with+60%25+of+the+rainforest%2C+followed+by+Peru+with+13%25%2C+Colombia+with+10%25%2C+and+with+minor+amounts+in+Venezuela%2C+Ecuador%2C+Bolivia%2C+Guyana%2C+Suriname+and+French+Guiana.+States+or+departments+in+four+nations+contain+%22Amazonas%22+in+their+names.+The+Amazon+represents+over+half+of+the+planet%27s+remaining+rainforests%2C+and+comprises+the+largest+and+most+biodiverse+tract+of+tropical+rainforest+in+the+world%2C+with+an+estimated+390+billion+individual+trees+divided+into+16%2C000+species)
  - [Translation with T5](https://huggingface.co/t5-base?text=My+name+is+Wolfgang+and+I+live+in+Berlin)</br>
  
   **Comment BERT apprend**
   BERT apprend de façon non supervisée, l'entrée se suffit à elle même, pas besoin de labelliser, qualifier quoi que ce soit, on se servira uniquement de l'entrée, et de plusieurs manières. Nous appellerons ça le MLM pour "Masked language model". Nous allons décortiquer ce que le modèle tente d'apprendre.</br>
Notations : **[CLS]** indique un début de séquence, **[SEP]** une séparation, en général entre deux phrases, **[MASK]** un mot masqué</br>
  **Les mots masqués (MLM):**
  Ici la séquence d'entrée a été volontairement oblitérée d'un mot, le mot masqué, et le modèle va apprendre à prédire ce mot masqué.</br>
  Entrée = [CLS] the man went to [MASK] store [SEP] </br>
  Entrée = [CLS] the man [MASK] to the store [SEP]</br>
  **La phrase suivante (NSP):**
  Ici le modèle doit déterminer si la séquence suivante (suivant la séparation[SEP]) est bien la séquence suivante. Si oui, IsNext sera vrai, le label sera IsNext, si non, le label sera NotNext.</br>
  Entrée = [CLS] the man went to [MASK] store [SEP] he bought a gallon [MASK] milk [SEP]</br>
  Label = IsNext</br>
  Entrée = [CLS] the man [MASK] to the store [SEP] penguin [MASK] are flight ##less birds [SEP]</br>
  Label = NotNext</br>
  [Source ici. Architecture globale de "The Transformer"](https://lesdieuxducode.com/images/blog/pauldenoyes@expaceocom/BERT-Transformer-Architecture-Globale.png)

  ### Question answering solution (QA)
   Dans leur solution, ils ont mis en place différents mécanismes, tels que la reconnaissance des entités nommées NER et le Question answering, pour répondre aux questions qui ont le mieux fonctionné, ils ont considéré le sentiment comme la question et la sous-phrase ou le mot comme la réponse, et ils l'envoient au transformateur suivi d'une couche dense / fully connected et une Softmax pour prédire deux ensembles de prababilités.</br>
le premier ensemble contient les probabilités pour chaque token, que le token soit le **Début** du texte sélectionné</br>
le deuxième ensemble contient les probabilités pour chaque token, que le token soit la **Fin** du texte sélectionné</br>
   - Question: sentiment
   - Answer: texte sélectionné
    ![alt text](https://github.com/Amine-OMRI/tweet-sentiment-extraction-kaggle-compete-1st-place-detailed-solution/blob/main/model_architecture.png?raw=true)
  ## Les modèles utilisés
  ### Les modèles du premier niveau
   **Les modèles de [Heartkilla](https://www.kaggle.com/aruchomu):**</br>
   RoBERTa-base-squad2, RoBERTa-large-squad2,DistilRoBERTa-base, base XLNet
   - Il a fait un pré-entrainement sur SQuAD 2.0</br>

      1) Il a utilisé le GPU Colab Pro pour RoBERTa-large et il a fallu environ 6h pour l'entraîner avec 5 folds et 4 époques sans optimisation particulière. 
         [Hikkiiii](https://www.kaggle.com/wochidadonggua)a également entraîner RoBERTa-large, 2V100, APEX(O1), il a fallu environ 220s par époque 
      2) RoBERTa-base-squad2 est disponible pré-entrainé par [HuggingFace](https://huggingface.co/deepset/roberta-base-squad2).

   - Certains d'entre eux sont déjà pré-entrainés sur SQuAD 2.0, ce qui fait que non seulement le pré-entrainement initial fonctionne, mais aussi la tâche de pré-      entrainement fonctionnais bien.</br>
   - Il a modifié l'architecture (Fine tuning) en effectuant une moyenne et un maxpooling (Avg / Max ) de toutes les couches sans embeddings.</br>
   - Il a également effectué un Multi Sample Dropout (MSD): cette technique accélère l'entrainement et permet une meilleure généralisation pour les réseaux de neurones.
   - AdamW: un optimiseur adaptatif avec utilisation d'une échelle de taux d'apprentissage pour moduler l'évolution du taux d'apprentissage de l'optimiseur en fonction du temps [(plus de détails ici)](https://arxiv.org/pdf/1711.05101.pdf).</br>
   - Une loss personnalisée : Jaccard-based Soft Labels.</br>
   - Le meilleur modèle unique : RoBERTa-base-squad2, 5 fold CV stratified : 0,715</br>   
   **Multi Sample Dropout (MSD):** C'est l'une des techniques qu'ils ont utilisées et que je trouve si intéressante. En fait, il applique un dropout plusieurs fois avec différents masques et ensuite il calcule la moyenne des résultats</br>
  Le dropout initial crée un sous-ensemble choisi au hasard (appelé dropout sample) à partir des données d'entrée de chaque itération d'entrainement, tandis que le MSD crée plusieurs échantillon de dropout. La loss est calculée pour chaque échantillon, puis la moyenne des losses des échantillons est calculée pour obtenir la Loss finale [(plus de détails ici)](https://arxiv.org/pdf/1905.09788.pdf).</br>
  ![alt text](https://github.com/Amine-OMRI/tweet-sentiment-extraction-kaggle-compete-1st-place-detailed-solution/blob/main/Multi-Sample-Dropout.png?raw=true)</br>
    Une autre technique qui a été utilisée comme Optimiser c'est :</br>
  **SWA :** la technique SWA (Stochastic Weight Averaging) récemment proposée, et sa nouvelle implémentation dans torchcontrib. La SWA est une procédure simple qui améliore la généralisation du deep learning sur la Descente de Gradient Stochastique (SGD) sans coût supplémentaire, et peut être utilisée en remplacement de tout autre optimiseur dans PyTorch. Le SWA a une large gamme d'applications et de fonctionnalités.</br>
  Il a été démontré que SWA améliore considérablement la généralisation des tâches de vision par ordinateur, y compris les VGG, les ResNets, les Wide ResNets et les DenseNets sur ImageNet et les CIFAR benchmarks.</br>
  En bref, le SWA effectue une moyenne égale des poids traversés par le SGD avec un programme d'apprentissage modifié.</br>

   **Custom loss Jaccard-based Soft Labels:** Étant donné que la Cross Entropy n'optimise pas directement l'indice de Jaccard, Heartkilla a essayé différentes fonctions de Loss pour pénaliser davantage les prédictions lointaines que les prédictions proches. SoftIOU utilisé dans la segmentation n'a pas aidé, il a donc trouvé une Loss personnalisée en calculant l'indice de Jaccard au niveau du token. Il a ensuite utilisé ces nouveaux labels cibles et a optimisé la divergence. Alpha c'est un paramètre permettant d'équilibrer l'étiquetage habituel basé sur la Cross Entropy et l'indice de Jaccard.
![alt text](https://www.googleapis.com/download/storage/v1/b/kaggle-user-content/o/inbox%2F2000545%2F9341bede28263bcf0e9bb259ac790338%2FScreen%20Shot%202020-05-30%20at%2017.31.22.png?generation=1592405028556842&alt=media)</br>
  Il a également remarqué que les probabilités dans ce cas changent assez rapidement, alors il décidé de corriger un peu le résultat en ajoutant un carré.
  ![alt text](https://www.googleapis.com/download/storage/v1/b/kaggle-user-content/o/inbox%2F2000545%2F4d1975e293c33c077fd45e6b81d1aa63%2FScreen%20Shot%202020-05-30%20at%2017.29.17.png?generation=1592405079812280&alt=media)</br>
  Cela a parfaitement fonctionné pour trois de ses modèles, à l'exception du DistilRoBERTa qui utilisait la précédente version sans le carré. Finalement, cette Loss a augmenté tous les modèles d'environ 0,003.
  Voici un graphique des probabilités target pour une phrase de 30 tokens avec start_idx=5 et end_idx=25, alpha=0,3.</br>
   ![alt text](https://www.googleapis.com/download/storage/v1/b/kaggle-user-content/o/inbox%2F2000545%2Fd746070e62bc05d74f7543785da6df70%2Fplot.jpg?generation=1592405194100691&alt=media)</br>
   
   **Les modèles de [Theo](https://www.kaggle.com/theoviel):**</br>
   ● Transformateurs</br>
      ○ BERT-base-uncased (CV 0.710)</br>
      ○ BERT-large-uncased-wwm (CV 0.710)</br>
      ○ DistilBERT (CV 0.705)</br>
      ○ ALBERT-large-v2 (CV 0.711)</br>
   ● Architecture</br>
      ○ MSD sur la concaténation des 8 derniers états cachés</br>
   ● Entrainement</br>
      ○ Adoucir la cross-entropy catégorielle</br>
      ![alt text](https://github.com/Amine-OMRI/tweet-sentiment-extraction-kaggle-compete-1st-place-detailed-solution/blob/main/Smoothed-categorical-cross-entropy.png?raw=true)</br>
      ○ [Taux d'apprentissage discriminatoire](https://arxiv.org/pdf/1801.06146.pdf)</br>
      ![alt text](https://github.com/Amine-OMRI/tweet-sentiment-extraction-kaggle-compete-1st-place-detailed-solution/blob/main/Discriminative-learning-rate.png?raw=true)</br>
      ○ **Sequence bucketing** pour accélérer l'entrainement : L'idée est d'effectuer une mise en bucket (bucketing) du corpus d'entraînement, où chaque bucket représente une plage de longueurs d'énonciation et chaque échantillon d'entraînement est attribué au bucket qui correspond à sa longueur.Ensuite, un batch est construit en tirant des séquences à partir d'un bucket choisi au hasard. Le concept de bucketing atténue d'une certaine manière le problème des zero-padding si des plages de longueur appropriées peuvent être définies, tout en permettant un certain niveau de caractère aléatoire au moins lorsque des séquences sont sélectionnées dans un batch.  Toutefois, les buckets doivent être très grands pour assurer une variabilité suffisamment importante au sein des batches. D'un autre côté, la fabrication de buckets trop grands augmentera le temps d'entrainement en raison de calculs non pertinents sur des zero-padding séquences. Le réglage correct de ces hyperparamètres est donc d'une importance fondamentale pour un entrainement rapide et robuste des modèles acoustiques.</br>
   
   **Les modèles de [Cl_ev (Anton)](https://www.kaggle.com/cl2ev1):**</br>
   ● Transformateurs</br>
      ○ RoBERTa-base (CV 0.715)</br> 
      ○ BERTweet: Un modèle linguistique pré-entrainé sur des [Tweets  en anglais](https://arxiv.org/pdf/2005.10200.pdf)</br>
   ● Architecture: Pareil que ceux de Théo</br>
   ● Entrainement</br>
      ○ Smoothed categorical cross-entropy</br>
      ○ Discriminative learning rate</br>
      ○ Fichier custom merges.txt pour RoBERTa</br>
   
   **Les modèles de [Hikkiiii](https://www.kaggle.com/wochidadonggua):**</br>
    ● Transformateurs</br>
      ○ 5fold-roberta-base-squad2(0.712CV) </br> 
      ○ 5fold-roberta-large-squad2(0.714CV) </br>
   ● Architecture: 
      ○ Ajoutez le sentiment à la fin du texte</br>
      ○ CNN + Couche linéaire sur la concaténation des derniers **3 hidden states**</br>
   ● Entrainement</br>
      ○ Smoothed categorical cross-entropy</br>
      ○ Discriminative learning rate</br>
      ○ Fichier custom merges.txt pour RoBERTa</br>
      
===> Étant donné que les transformateurs sont à niveau token, ils ne peuvent pas capturer le bruit.</br>
===> Solution : stacking</br>
      ○ Convertir les probabilités des tokens des transformateurs au niveau des caractères en attribuant à chaque caractère la probabilité de son token</br>
      ○ Alimenter les probabilités OOF (out of fold) au niveau des caractères en un NN au niveaux des caractères en utilisant le Staking</br>
   
   **Le Stacking**: est un ensemble machine learning algorithm.  Il existe de nombreuses façons d'assembler des modèles, les modèles les plus connus étant Bagging ou le Boosting. Le Bagging permet de regrouper plusieurs modèles similaires avec une variance élevée et d'en faire la moyenne pour diminuer la variance. Le Boosting permet de construire plusieurs modèles incrémentiels pour diminuer le biais, tout en gardant une faible variance.</br>
   Le Stacking (parfois appelé  Stacked Generalizatio) est un paradigme différent. Le but de l'empilement est d'explorer un espace de modèles différents pour le même problème. L'idée est que vous pouvez attaquer un problème d'apprentissage avec différents types de modèles qui sont capables d'apprendre une partie du problème, mais pas tout l'espace du problème. Ainsi, vous pouvez construire plusieurs apprenants différents et vous les utilisez pour construire une prédiction intermédiaire, une prédiction pour chaque modèle appris. Ensuite, vous ajoutez un nouveau modèle qui apprend à partir des prédictions intermédiaires  de la même target.</br>
  **NN utilisant le Stacking**</br>
  ![alt text](https://github.com/Amine-OMRI/tweet-sentiment-extraction-kaggle-compete-1st-place-detailed-solution/blob/main/Stacking.png?raw=true)</br>
  
  ### Les modèles du deuxième niveau</br>
  **Char-level NN:RNN**</br>
  ![alt text](https://github.com/Amine-OMRI/tweet-sentiment-extraction-kaggle-compete-1st-place-detailed-solution/blob/main/Char-level-NN-RNN.png?raw=true)</br>
  **Char-level NN:CNN**</br>
  
  ![alt text](https://github.com/Amine-OMRI/tweet-sentiment-extraction-kaggle-compete-1st-place-detailed-solution/blob/main/Char-level-NN-CNN.png?raw=true)</br>
  **Char-level NN:WaveNet**</br>
  ![alt text](https://github.com/Amine-OMRI/tweet-sentiment-extraction-kaggle-compete-1st-place-detailed-solution/blob/main/Char-level-NN-WaveNet.png?raw=true)</br>
   ### Soumissions (Submissions) </br>
  **Premières soumissions**</br>
  ![alt text](https://github.com/Amine-OMRI/tweet-sentiment-extraction-kaggle-compete-1st-place-detailed-solution/blob/main/1st-submission.png?raw=true)</br>
  **Deuxièmes soumissions**</br>
  ![alt text](https://github.com/Amine-OMRI/tweet-sentiment-extraction-kaggle-compete-1st-place-detailed-solution/blob/main/2nd-submission.png?raw=true)</br>
  
  ### Pseudo-labeling (étiquetage)
  Ils ont utilisé un de leurs échantillons de CV 0.7354 pour pseudo-étiqueter les données de test publiques. Ils ont suivi la même [approche](https://www.kaggle.com/c/google-quest-challenge/discussion/129840)et ont créé des   pseudo-étiquettes “leakless”. Ils ont ensuite utilisé un seuil de 0,35 pour couper les échantillons de faible confiance. Le score de confiance a été déterminé comme suit : (start_probas.max() + end_probas.max()) / 2. Ils ne sont pas sûrs que cela aide vraiment à améliorer le score final dans son ensemble, car ils n'ont fait que 9 soumissions avec l'inférence complète.</br>
  
  ## Pour plus de détails sur leur solution
Ils ont fait un discours sur leur solution lors du meetup ODS Paris: [YouTube link](https://www.youtube.com/watch?v=S7soN-y5WMg)<br />
Leur repo sur github : [SlideShare link](https://github.com/heartkilla/kaggle_tweet)
