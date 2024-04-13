
Introduction:

This project  introduces an advanced novel approach using SciBERT and CNNs to systematically categorize academic abstracts,body text,title from the Elsevier OA CC-BY corpus based on the subject areas of research. Our input includes abstract, body text, title and top 50 most important words from the body text column obtained using BERT topic modeling. Our target variable is subject areas of reserach comprising of the following 18 subject areas of research namely:

    1. Multidisciplinary (MULT) 
    
    2. Agriculture sciences (AGRI) 
    
    3. Arts (ARTS)
    
    4. Bio-chemistry (BIOC)
    
    5. Decision Sciences (DECI) 
    
    6. Medicine (MEDI)
    
    7. Environmental Science (ENVI)
    
    8. Engineering (ENGI)
    
    9. Neuroscience (NEUR)
    
    10. Sociology (SOCI)

    11. Material Science (MATE)


Data Pre-Processing:

Outlined below is a comprehensive breakdown of our data processing methodology:

  1. Data Segmentation and Preparation:We divide the text data into segments of abstracts, titles, and body texts, and prepare them by trimming each to       specific word limits to ensure conciseness and relevance. For each document, we segment the text into three parts of sequents length 500 containing abstract (200 words), title (50 words), and body text (200 words) in the first segment followed by an additional 500 words from body text column in the second segment and an additional 500 words from the body text in the third segment. 
  
  2. Vectorization: We use the count vectorizer to transform the body text into a numerical format, targeting the top 50 words by frequency to capture the key thematic elements of the text.

  3.Topic Modeling: We employed a  BERT-based topic modeling technique to the body text to distill a set of topics that encapsulate the semantic content of the corpus, aiding in the dimensionality reduction and contextual understanding.We concatenated the abstract, title, and body text segments along with the extracted topic words for each document. This concatenated text becomes the input for the model. 
  
  4. Multi-Label Binarization and Tokenization: Subject area labels are encoded using MultiLabelBinarizer to prepare for multi-label classification, converting categorical labels into a binary format suitable for the model to process. The concatenated texts are tokenized using the SciBERT tokenizer, creating the necessary inputs for the model, including input IDs and attention masks.

Model Architecture:

Out of all the experiments conducted, the integration of SciBERT with a Convolutional Neural Network (CNN) and BERT topic modeling yielded the most favorable results. This combination emerged as the superior approach in our quest to boost the performance of text classification tasks. The SciBERT-CNN with BERT topic modeling approach significantly outperformed other models, cementing its position as our architecture of choice for the detailed task at hand.
![architecture](https://github.com/sivakumarthiyagarajan/266_project/assets/120620926/8aa96a61-321e-4133-bad0-2408e7aa24ed)



