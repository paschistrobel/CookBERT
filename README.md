# CookBERT: A domain adapted BERT model for the cooking domain
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

## Performance
### Text classification
<table>
    <thead>
        <tr>
            <th>Model</th>
            <th>Condition</th>
            <th>Precision</th>
            <th>Recall</th>
            <th>F-Measure</th>
            <th>95%-CI</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td rowspan=2>BERTbase</td>
            <td rowspan=1>no context</td>
            <td rowspan=1>47.94%</td>
            <td rowspan=1>48.68%</td>
            <td rowspan=1>46.15%</td>
            <td rowspan=1>[41.15%;51.16%]</td>
        </tr>
        <tr>
            <td>1 prev turn</td>
            <td>46.29%</td>
            <td>49.84%</td>
            <td>45.38%</td>
            <td>[40.06%;50.70%]</td>
        </tr>
        <tr>
            <td rowspan=2>CookBERT</td>
            <td rowspan=1>no context</td>
            <td rowspan=1><b>48.58%</b></td>
            <td rowspan=1><b>55.65%</b></td>
            <td rowspan=1><b>50.72%</b></td>
            <td rowspan=1>[45.54%;55.90%]</td>
        </tr>
        <tr>
            <td>1 prev turn</td>
            <td><b>52.26%</b></td>
            <td><b>59.30%</b></td>
            <td><b>54.05%</b></td>
            <td>[48.93%;59.16%]</td>
        </tr>
        <tr>
            <td rowspan=2>FoodBERT</td>
            <td rowspan=1>no context</td>
            <td rowspan=1>42.41%</td>
            <td rowspan=1>49.81%</td>
            <td rowspan=1>44.32%</td>
            <td rowspan=1>[38.92%;49.73%]</td>
        </tr>
        <tr>
            <td>1 prev turn</td>
            <td>36.89%</td>
            <td>44.49%</td>
            <td>38.09%</td>
            <td>[32.64%;43.55%]</td>
        </tr>
    </tbody>
</table>

### Named entity recognition
<table>
    <thead>
        <tr>
            <th>Model</th>
            <th>Tagging-Task</th>
            <th>Precision</th>
            <th>Recall</th>
            <th>F-Measure</th>
            <th>95%-CI</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td rowspan=5>BERTbase</td>
            <td rowspan=1>Food-classification</td>
            <td rowspan=1>90.68%</td>
            <td rowspan=1>96.06%</td>
            <td rowspan=1>93.29%</td>
            <td rowspan=1>[92,87%;93.71%]</td>
        </tr>
        <tr>
            <td>FoodOn</td>
            <td>65.24%</td>
            <td>73.10%</td>
            <td>68.94%</td>
            <td>[67.04%;70.83%]</td>
        </tr>
         <tr>
            <td>Hansard-parent</td>
            <td>80.35%</td>
            <td>88.68%</td>
            <td>84.31%</td>
            <td>[83.54%;85.08%]</td>
        </tr>
         <tr>
            <td>Hansard-closest</td>
            <td>70.79%</td>
            <td>79.98%</td>
            <td>75.10%</td>
            <td>[73.87%;76.34%]</td>
        </tr>
        <tr>
            <td>SNOMED CT</td>
            <td>63.04%</td>
            <td>70.65%</td>
            <td>66.62%</td>
            <td>[64.49%;68.75%]</td>
        </tr>
         <tr>
            <td rowspan=5>CookBERT</td>
            <td rowspan=1>Food-classification</td>
            <td rowspan=1><b>92.25%</b></td>
            <td rowspan=1><b>96.52%</b></td>
            <td rowspan=1><b>94.47%</b></td>
            <td rowspan=1>[94.17%;94.76%]</td>
        </tr>
        <tr>
            <td>FoodOn</td>
            <td><b>69.75%</b></td>
            <td><b>77.51%</b></td>
            <td><b>73.42%</b></td>
            <td>[71.91%;74.93%]</td>
        </tr>
         <tr>
            <td>Hansard-parent</td>
            <td><b>82.72%</b></td>
            <td><b>89.18%</b></td>
            <td><b>85.83%</b></td>
            <td>[84.69%;86.97%]</td>
        </tr>
         <tr>
            <td>Hansard-closest</td>
            <td><b>72.21%</b></td>
            <td><b>80.41%</b></td>
            <td><b>76.08%</b></td>
            <td>[74.60%;77.56%]</td>
        </tr>
        <tr>
            <td>SNOMED CT</td>
            <td><b>68.58%</b></td>
            <td><b>75.51%</b></td>
            <td><b>71.87%</b></td>
            <td>[69.99%;73.75%]</td>
        </tr>
         <tr>
            <td rowspan=5>FoodBERT</td>
            <td rowspan=1>Food-classification</td>
            <td rowspan=1>85.28%</td>
            <td rowspan=1>94.24%</td>
            <td rowspan=1>89.53%</td>
            <td rowspan=1>[88.90%;90.17%]</td>
        </tr>
        <tr>
            <td>FoodOn</td>
            <td>58.73%</td>
            <td>61.03%</td>
            <td>59.85%</td>
            <td>[56.56%;63.13%]</td>
        </tr>
         <tr>
            <td>Hansard-parent</td>
            <td>68.41%</td>
            <td>80.62%</td>
            <td>74.01%</td>
            <td>[72.13%;75.90%]</td>
        </tr>
         <tr>
            <td>Hansard-closest</td>
            <td>59.55%</td>
            <td>67.52%</td>
            <td>63.28%</td>
            <td>[60.43%;66.13%]</td>
        </tr>
        <tr>
            <td>SNOMED CT</td>
            <td>53.63%</td>
            <td>51.84%</td>
            <td>52.67%</td>
            <td>[49.17%;56.17%]</td>
        </tr>
    </tbody>
</table>


### Question answering
|Model|Exact match|F-measure|95%-CI|
| --- | --- | --- | ---|
|BERTbase| **14.06%**| **32.39%**| [31.25%;33.54%]|
|CookBERT| 12.51% |30.64%| [29.50%;31.78%]|
|FoodBERT|10.81%| 27.51%| [26.51%;28.50%]|

## Training specs

