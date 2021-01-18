---
title : Faire un nuage de mots
tags : NLP
etat : hiver
---

La bibliothèque python `wordcloud` donne la possibilité de créer des nuages de mots avec l'APi de [[Matplotlib]]. La [documentation](https://amueller.github.io/word_cloud/) associée a le mérite d'exister mais est très succinte.

On commence par importer la classe `Wordcloud` et initialiser un objet. C'est l'occasion de définir ses propriétés graphiques.

```python
from wordcloud import WordCloud

cloud_generator = WordCloud(background_color='white',
                            random_state=1)
````

La méthode utilisée pour la génération dépend du type de données que l'on a :

- Avec du texte simple, on utilisera `.generate(text)``
- Si l'on dispose d'un dictionnaire `{mot:fréquence}`, on peut utiliser `.generate_from_frequencies(text)`
- Si l'on dispose d'un dataframe avec une colonne correspondant aux poids des mots et les mots en index, on utilisera `.fit_words(df_weights)`. On ordonnera les lignes du dataframe si l'on veut que seuls les mots les plus "lourds" apparaissent dans le nuage.

Exemple simple :

```python
cloud_generator = WordCloud(background_color='white',
                            random_state=1)

wordcloud_image = cloud_generator.fit_words(df_ranked_words)
plt.imshow(wordcloud_image, interpolation="bilinear")
plt.show()
````

![](/assets/img/wordcloud1.png#center)

Les options graphique suivantes sont disponibles :

- `width = 500` - largeur du graphique
- `height = 200` - hauteur du graphique
- `background_color='salmon'` - couleur du fond
- `colormap = 'tab20b'` - couleur des mots[^1]
- `collocations=False` - Permet d'éviter que des doublons apparaissent
- `stopwords = STOPWORDS`- retire les *stopwords*[^2]

Exemple plus fourni :



[^1]: On importe avec `from matplotlib import cm`. [Matplotlib colormaps](https://matplotlib.org/3.2.1/tutorials/colors/colormaps.html)
[^2]: Préciser au moment de l'importation : `from wordcloud import WordCloud, STOPWORDS`