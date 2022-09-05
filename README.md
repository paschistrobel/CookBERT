# CookBERT: A domain adapted BERT model for the cooking domain

See the official [CookBERT paper](docs/BachelorThesis.pdf).

## What is CookBERT?
CookBERT is a domain-specific [BERT](https://github.com/google-research/bert "Google's BERT implementation") model that was created via domain adaptive pretraining on the instructions of the RecipeNLG corpus, as well as enhancing BERT's default vocabulary by a total of 1229 cooking specific words. As a result, CookBERT is geared more towards the cooking domain:
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

The domain-specifity of CookBERT has proven to be superior in text classification and named entity recognition when dealing with data related to the cooking domain. 

## Performance
CookBERT was finetuned and evaluated on three different tasks, including information need classification, food entity tagging and question answering. In addition, BERTbase (uncased version) and [FoodBERT](https://github.com/ChantalMP/Exploiting-Food-Embeddings-for-Ingredient-Substitution "FoodBERT Github") were applied for the same tasks in order to be able to compare and rank CookBERT's performance.

### Text classification
Results of the classification of user information needs that arise during cooking; Based on the [Cookversational dataset](https://github.com/AlexFrummet/CookversationalSearch "CookversationalSearch Github").
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
<sub>Best performances printed in bold</sub>

### Named entity recognition
Food entity tagging using the curated version of the [FoodBase corpus](https://academic.oup.com/database/article/doi/10.1093/database/baz121/5611291 "Link to FoodBase paper"), as well as the labels provided by [Stojanov et al. (2021)](https://www.jmir.org/2021/8/e28229 "Link to paper") for five different tagging schemes.
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
<sub>Best performances printed in bold</sub>

### Question answering
Question answering in the sense of answer span extraction; Based on the cooking subset of the [DoQA dataset](https://aclanthology.org/2020.acl-main.652/ "Link to DoQA paper").
|Model|Exact match|F-measure|95%-CI|
| --- | --- | --- | ---|
|BERTbase| **14.06%**| **32.39%**| [31.25%;33.54%]|
|CookBERT| 12.51% |30.64%| [29.50%;31.78%]|
|FoodBERT|10.81%| 27.51%| [26.51%;28.50%]|

<sub>Best performances printed in bold</sub>

## Training specs
To obtain CookBERT, `BERTbase (uncased version)` was used as the starting point which was then further pretrained for `three additional epochs` on the `MLM` task on the `RecipeNLG instructions`, with `5% serving as validation data`. Training was performed with a `learning rate of 2e-5`, an effective `batch size of 32`, and a `maximum sequence length of 256`. The training took appoximately `five complete days` on a single `NVIDIA Tesla P100 GPU` provided by Google Colab Pro.

# Using CookBERT
The CookBERT pytorch model checkpoint can be downloaded from [this](https://drive.google.com/drive/folders/1l1izk2hQp2AvLe0uFywoP0z3ZccMFng-?usp=sharing) Google Drive folder. Huggingface Transformer Library enables the model to be set up easily:
```python
from transformers import (
    BertTokenizerFast,
    BertForMaskedLM,
    pipeline
)

CookBERT_tokenizer = BertTokenizerFast.from_pretrained("CookBERT-checkpoint")
CookBERT = BertForMaskedLM.from_pretrained("CookBERT-checkpoint")
CookBERT_pipeline = pipeline("fill-mask", model=MLM_CookBERT, tokenizer=MLM_CookBERT_tokenizer)

masked_text = "Cut the [MASK] into small pieces."
print("Predictions: ", CookBERT_pipeline(masked_text, top_k=5))
```

Note that the Google Drive folder only contains the CookBERT checkpoint that was trained on the MLM task. In order to apply CookBERT, the finetuning script from Huggingface can be used. 
