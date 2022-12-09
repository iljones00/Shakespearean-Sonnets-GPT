# Shakespearean-Sonnets-GPT
Authors: Isaiah Jones (), Ruth Bagley, Shubhanshi Gaudani (shubhanshigaudani2024@u.northwestern.edu)

Contact email: 

Northwestern University 

COMP SCI 496: Generative Deep Models

Professor Bryan Pardo

## Motivation 
The goal of the project is to generate Shakespearean sonnets based on 5 keywords given to the model. Shakespearean sonnets have a specific meter and rhyme scheme that hopefully our model will learn to generate, and we will evaluate our generated sonnets based on their adherence to this structure and their similarity to the keywords provided as input.

## Prior Work 
In class, we have seen many models that generate text ‘organically’, however we were curious to see how to make this generated text such that it inherits a new form (i.e. that of a sonnet) while still retaining the initial content/subject matter. Upon further research we found many attempts at algorithmic sonnet generation, the Hafez et al. approach generates sonnets based on an inputted arbitrary subject by using an RNN and a FSA. A separate paper by Benhardt et al. builds on the same approach to determine rhymes by using both phoneme structure and the stress pattern for each word to decide the degree of rhyme. While all of these papers perform sonnet generation from topics, we are interested in transforming a text of given length into a sonnet. 

### GPoet-2:
One of the main inspirations for our work was GPoet-2, a GPT-2 based limerick generator. Also with a rhyme scheme and high structure. They enforce the rhyme scheme by fine-tuning the model with a reversed corpus, though they mention the quality in limerick takes a hit when trained this way (https://arxiv.org/pdf/2205.08847.pdf)

### GPT-2 Poetry by Gwern Branwen:
Another inspiration for our work is GPT-2 Neural Network Poetry by Gwern Branwen. They trained GPT-2 on the Gutenberg Poetry Corpus containing 3 million lines of free and available poetry before generation. While his model was at generating prose, it still would require some additional finetuning for the specific task of sonnet generation. In addition, we found a fair amount of RNN-based models and transformer based models for smaller poetry tasks such as haikus and other short-formed poems. (https://www.gwern.net/GPT-2) 

## Approach 
### Dataset 
We used Shakespearean sonnet dataset (https://www.kaggle.com/datasets/blacksheep2105/shakespearean-sonnets )to fine tune the pre-trained model. The sonnet dataset is a text file containing Shakespeare’s 154 sonnets. We refined the dataset to include 5 key words that capture the main essence of the sonnet. The 5 words were selected manually from the sonnet, and later we also tried using a TFIDF based approach to extract these words but found the manual approach to be better in terms of the results obtained. 
So an example from the dataset is: 
Keywords: 
weary, travel, zealous, imaginary, mind

Sonnet:
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

### GPT-2 and Finetuning it 


## Results 
