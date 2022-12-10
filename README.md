# Shakespearean-Sonnets-GPT
Authors: <br>
Isaiah Jones (isaiah.jones@u.northwestern.edu), *Northwestern University* <br>
Ruth Bagley (ruthbagley16@gmail.com), *Northwestern University* <br>
Shubhanshi Gaudani (shubhanshigaudani2024@u.northwestern.edu), *Northwestern University* <br>


**COMP SCI 496: Generative Deep Models**

Professor Bryan Pardo

## Motivation 
The goal of the project is to generate Shakespearean sonnets based on 5 keywords given to the model. Shakespearean sonnets have a specific meter and rhyme scheme that hopefully our model will learn to generate, and we will evaluate our generated sonnets based on their adherence to this structure and their similarity to the keywords provided as input.

## Prior Work 
In class, we have seen many models that generate text ‘organically’, however we were curious to see how to make this generated text such that it inherits a new form (i.e. that of a sonnet) while still retaining the initial content/subject matter. Upon further research we found many attempts at algorithmic sonnet generation, the Hafez et al. approach generates sonnets based on an inputted arbitrary subject by using an RNN and a FSA. A separate paper by Benhardt et al. builds on the same approach to determine rhymes by using both phoneme structure and the stress pattern for each word to decide the degree of rhyme. While all of these papers perform sonnet generation from topics, we are interested in transforming a text of given length into a sonnet. 

### GPoet-2:
One of the main inspirations for our work was GPoet-2, a GPT-2 based limerick generator. Also with a rhyme scheme and high structure. They enforce the rhyme scheme by fine-tuning the model with a reversed corpus, though they mention the quality in limerick takes a hit when trained this way [1].

### GPT-2 Poetry by Gwern Branwen:
Another inspiration for our work is GPT-2 Neural Network Poetry by Gwern Branwen. They trained GPT-2 on the Gutenberg Poetry Corpus containing 3 million lines of free and available poetry before generation. While his model was at generating prose, it still would require some additional finetuning for the specific task of sonnet generation. In addition, we found a fair amount of RNN-based models and transformer based models for smaller poetry tasks such as haikus and other short-formed poems [2].  

## Approach 
### Dataset 
We used Shakespearean sonnet dataset from Kaggle[3] to fine tune the pre-trained model. The sonnet dataset is a text file containing Shakespeare’s 154 sonnets and can be found in `Sonnets.txt` . We refined the dataset to include 5 key words that capture the main essence of the sonnet. The 5 words were selected manually from the sonnet, and later we also tried using a TFIDF based approach to extract these words but found the manual approach to be better in terms of the results obtained. The refined dataset can be found in `Sonnets with keywords.txt`
So an example from the dataset is:  <br>
 <br>
*Keywords*: 
weary, travel, zealous, imaginary, mind

*Sonnet*:
Weary with toil, I haste me to my bed, <br>
The dear repose for limbs with travel tired;  <br>
But then begins a journey in my head <br>
To work my mind, when body's work's expired: <br>
For then my thoughts--from far where I abide-- <br>
Intend a zealous pilgrimage to thee, <br>
And keep my drooping eyelids open wide, <br>
Looking on darkness which the blind do see: <br>
Save that my soul's imaginary sight <br>
Presents thy shadow to my sightless view, <br>
Which, like a jewel hung in ghastly night, <br>
Makes black night beauteous, and her old face new. <br>
Lo! thus, by day my limbs, by night my mind, <br>
For thee, and for myself, no quiet find. <br>

### GPT-2
The OpenAI GPT-2 in the past has exhibited abilities of writing very coherent essays with enriched vocabulary that goes beyond what we anticipated large language models are able to produce. The GPT-2 has an architechture similar to the decoder-only transformer [4]. The GPT2 was, however, a very large, transformer-based language model trained on a massive dataset, and we leverage its pre-trained model in order to fine-tune it on our much smaller dataset. 

### Fine-tuning Process 
In order to fine-tune the model, we: 
1. Cloned the GPT-2 Medium (345M parameters) model 
2. Unfroze the last 6 layers of the model 
3. Retrained using the Transformers library 

In terms of the tokenizer, we used the existing tokenizer by GPT-2. The overall code for fnetuning the GPT-2 can be found in the file `GPT_2_finetuning_for_sonnets.ipynb` 

### Experiments 
#### 1. Varying the number of unfrozen layers:
We varied the number of unfrozen layers from 4-8. For both 4 and 8 the model produced gibberish text, whereas for 5, 6 and 7 the model produced standard english. For the 7 layer variation, text had large chunks of generated text directly lifted from the initial sonnets while the 5 layer variation often had youtube links and sports commentary. Therefore, our final model has 6 unfreezed layers. The specific loss variation can be seen in the below graph:

<img src="/unfeezed-layers-experiment.png" width="400">

#### 2. Varying the number of epochs (Depending on the resulting training loss and validation loss values):
We varied the number of epochs from 7 until 40. We found that the validation loss was consisstently the lowest between 12 to 14 epochs after which it increased indicating overfitting to the data. Our final model was therefore trained for 13 epochs. 

#### 3. Varying the learning rate: 
We discovered that our model was very sensitive to learning rate. The current learning rate of the model is 5e-3, when we tried to decrease or increase the power or scalar value for the exponential, the model either did not produce any output or produced gibberish/random numbers and symbols. We therefore narrowed it down to using 5e-3. 

#### 4. Varying the type of GPT-2 Model:
The GPT2 model is available in 4 sizes: GPT2-small, GPT2-medium, GPT2-large, GPT2-extralarge. We realised that even Colab Pro runs out of memory for both the GPT2-large and GPT2-extralarge models, however GPT2-medium was supported and therefore we ended up using it. However overall in terms of results there wasn't a great difference in terms of results between GPT2-small and GPT2-medium. Our initial experiments were with GPT2-medium. 

### Evaluation Metric
We created a 'sonnet score' evaluation metric for sonnet structure, which uses Poesy[5] to judge length, meter, and rhyme of the poem and compare to Shakespearean sonnet standards (which are 14 lines, 10 syllables per line in iambic pentameter, and an abab cdcd efef gg rhyme scheme). The score varies from 0 to 1, with 1 being perfect. The rhyme detection is not always perfectly accurate, but usually it's quite close, making our sonnet score a reasonably reliable metric. The poem evaluation is found `in sonnetScore.ipynb`

## Results 

Overall, we feel quite satisfied with the quality of work generated by our model. With our work, we demonstrate our ability to use GPT-2 for our specific usecase and have it generate outputs that are similar enough to what we desire. Although our model was unable to exactly capture the complex structure and rhyme scheme of a Shakespearean sonnet, our model clearly demonstrates a level of structural learning. Through our hyperparameter search, we were also able to limit the amount of straight recall done by the model so that it is purely generating new bodies of work.

### Our Generated Sonnets
Here are two sonnets generated by our model:

*Sonnet 1*.<br>
'Tis better policy (of perfect truth being made) <br>
never kept old excuse newsworn stands least blushing stand! <br>
Therefore desire is daily renewed <br>
beseem thine evermore enlarged loving quest <br>
increase her storey doomless phoenix <br>
ere long date near which she would convert <br>
else mistakingly appear'd deadowed or diecast away <br>
twain by fortune do sing hymns at heaven gateways <br>
where late sweetest creatures live <br>
sang song players possessed did common forsake <br>
their faces become sourest spies deservalled<br>
informer scouchered simplicity strangle', <br>
maketh bad what they bring forth now <br>
must bear all wrong directed thereby reign.<br>
<br>
Sonnet Score: 0.731
<br>
<br>
*Sonnet 2*.<br>
When thou shalt be disposed to set me light <br>
And place my merit in the eye of scorn. <br>
I will not praise that purpose <br>
not once vassalized mine own desert; <br>
but when thy love hath cast his utmost sum <br>
past paying rent: dost pay it as if <br>
Not paid before was no need then took from thee <br>
this kindness gift confoundingly <br>
make defence for myself against confounding age's <br>
cruel knife and crooked sword-barren siege bars <br>
so shall he fight eternal war with Time decays?<br>
<br>
Sonnet Score: 0.454
<br>
Additional examples are in `generated_examples.txt`

## Comparison to other models

### GPT-3
In a one-shot setting, and provided with the keywords "love, fame, excitement, angst, cheese", two GPT-3 models produced the following sonnets.

*text-davinci-003*<br>
To seek sweet pleasure and exciting show, <br>
Where anguish and despair their darts bestow, <br>
The cheese of life is all to him a woe; <br>
E'en though he strive with all his power and might <br>
To win the laurel and his soul's delight, <br>
Yet still the same old story is in sight, <br>
That love and fame bring with them endless plight. <br>
And so, in vain, his efforts will not cease, <br>
For love and fame have brought him naught but grief; <br>
The cheese of life is still an utter tease, <br>
And all his striving brings him naught but grief.<br>
<br>
Sonnet score: 0.878<br>
<br>
<br>
*text-davinci-002*<br>
Love is like a rose, <br>
Fame is like a bee, <br>
Excitement is like a cat, <br>
Angst is like a cheese, <br>
But only you can make them what they are.<br>
<br>
Sonnet score: 0.332
<br>

### ChatGPT
In a zero-shot setting with no keywords, ChatGPT produced the following two sonnets. The first is original, but the second is an exact copy of Shakespeare, with one repeated line which reduced the sonnet score quite a bit.

*Sonnet 1*<br>
With beauteous eyes and hair of shining gold,<br>
Thou art the fairest maid that e'er I've seen.<br>
In thy sweet voice, a thousand tales are told,<br>
And every glance doth speak of beauty keen.<br>
<br>
Thy cheeks, like roses, bloom with youthful glow,<br>
And in thy lips, a subtle, red delight.<br>
Thy graceful form doth move with gentle flow,<br>
A vision fair to see, both day and night.<br>
<br>
But beauty fades, and youth doth pass away,<br>
And though thou art a goddess in mine eyes,<br>
Thou must, like all before thee, fade to gray,<br>
And with thy passing, all our joys will die.<br>
<br>
So let us cherish every moment spent,<br>
For time doth steal away what it hath lent.<br>
<br>
Sonnet score: 0.998<br>
<br>
<br>
*Sonnet 2*<br>
In fair Verona, where we lay our scene,<br>
Two households, both alike in dignity,<br>
In fair Verona, where we lay our scene,<br>
From ancient grudge break to new mutiny,<br>
<br>
Where civil blood makes civil hands unclean.<br>
From forth the fatal loins of these two foes<br>
A pair of star-cross'd lovers take their life;<br>
Whose misadventured piteous overthrows<br>
Do with their death bury their parents' strife.<br>
<br>
The fearful passage of their death-mark'd love,<br>
And the continuance of their parents' rage,<br>
Which, but their children's end, naught could remove,<br>
Is now the two hours' traffic of our stage;<br>
<br>
The which if you with patient ears attend,<br>
What here shall miss, our toil shall strive to mend.<br>
<br>
Sonnet Score: 0.817<br>
<br>


## References 
[1]. https://arxiv.org/pdf/2205.08847.pdf <br>
[2]. https://www.gwern.net/GPT-2 <br>
[3]. https://www.kaggle.com/datasets/blacksheep2105/shakespearean-sonnets <br>
[4]. https://jalammar.github.io/illustrated-gpt2/ <br>
[5]. https://github.com/quadrismegistus/poesy <br>
