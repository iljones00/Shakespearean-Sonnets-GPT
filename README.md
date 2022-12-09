# Shakespearean-Sonnets-GPT
Authors: Isaiah Jones (), Ruth Bagley, Shubhanshi Gaudani

Contact email: 

Northwestern University 

COMP SCI 496: Generative Deep Models

Professor Bryan Pardo

## Motivation 
The goal of the project is to generate Shakespearean sonnets out of short stories. Shakespearean sonnets have a specific meter and rhyme scheme that hopefully our model will learn to generate, and we will evaluate our generated sonnets based on their adherence to this structure and their similarity to the story provided as input.

In class, we have seen many models that generate text ‘organically’, however we were curious to see how to make this generated text such that it inherits a new form (i.e. that of a sonnet) while still retaining the initial content/subject matter. Upon further research we found many attempts at algorithmic sonnet generation, the Hafez et al. approach generates sonnets based on an inputted arbitrary subject by using an RNN and a FSA. A separate paper by Benhardt et al. builds on the same approach to determine rhymes by using both phoneme structure and the stress pattern for each word to decide the degree of rhyme. While all of these papers perform sonnet generation from topics, we are interested in transforming a text of given length into a sonnet. 

## Approach 
### Dataset 
We usedShakespearean sonnet dataset (https://www.kaggle.com/datasets/blacksheep2105/shakespearean-sonnets ) to fine tune the pre-trained model. The sonnet dataset is a text file containing Shakespeare’s 154 sonnets. We refined the dataset to include 5 key words that capture the main essence of the sonnet. The 5 words were selected manually from the sonnet, and later we also tried using a TFIDF based approach to extract these words but found the manual approach to be better in terms of the results obtained. 

## Results 

Describe/show some results (how well it works in no more than a paragraph. Maybe show a picture or image or audio file of system output)
