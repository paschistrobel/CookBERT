# CookBERT: Domain adapted BERT model for the cooking domain
## What is CookBERT?
CookBERT is based on Google's BERT (Bidirectional Encoder Representations from Transformers), which is a famous deep learning model that has received a lot of attention over the last years due to its incredible performance in a wide variety of NLP tasks (including text classification, question answering, named entity recognition and many more). However, BERT is only pretrained on textual data from the general domain (wikipedia articles and books) and it's performance is limited when encountering domain-specific data, i.e. the cooking domain. CookBERT was developed to tackle this problem. 
CookBERT ist entstanden, indem das BERT base model als Ausgangspunkt hergenommen, und via domain-adaptive pretraining weitere 3 Epochen auf die Instruktionen des kochspezifischen RecipeNLG Datensatzes trainiert wurde. Das entstande CookBERT modell ist somit speziell auf die Kochdomäne gerichtet, sichtbar in den Prädiktionen:
<table>
    <thead>
        <tr>
            <th>Input</th>
            <th>Model</th>
            <th>Top 5 predictions for [MASK] token</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td rowspan=2>"Do I have to [MASK] the apple?"</td>
            <td rowspan=1>BERTbase</td>
            <td rowspan=1>eat, take, have, touch, get</td>
        </tr>
        <tr>
            <td>CookBERT</td>
            <td>peel, slice, use, dice, chop</td>
        </tr>
        <tr>
            <td rowspan=2>“[MASK] the water.”</td>
            <td rowspan=1>BERTbase</td>
            <td rowspan=1>in, drink, under, into, on</td>
        </tr>
        <tr>
            <td>CookBERT</td>
            <td>boil, heat, add, scald, chill</td>
        </tr>
        <tr>
              <td rowspan=2>“Cut the [MASK] into small pieces.”</td>
              <td rowspan=1>BERTbase</td>
              <td rowspan=1>wood, paper, leaves, meat, bark</td>
          </tr>
          <tr>
              <td>CookBERT</td>
              <td>chicken, cheese, fruit, cabbage, sausage</td>
          </tr>
    </tbody>
</table>

Das volle Paper zu CookBERT ist [hier](docs/BachelorThesis.pdf) zu finden.
