
DATASCI 266: Natural Language Processing Final Project 

Empowering Interdisciplinary Research with  BERT-Based Models: A Computational Approach for Enhanced Knowledge Synthesis

Semester: Spring 2024 

Instructors: Mark Butler, Peter Grabowski

Team Members:

  => Darya Likhareva
  
  => Hamsini Sankaran
  
  => Sivakumar Thiyagarajan

 Project Organization
 
 ├── README.md          <- The top-level README describing the project aims
 
 ├── KeyModel           <- The results of our primary model SciBERT-CNN with BERT topic modeling
 
 ├── Experiments        <- The Experiments that our team conducted for multi label text classification  
 
     ├── Longformer
     ├── BERT


Introduction:

This project  introduces an advanced novel approach using SciBERT and CNNs to systematically categorize academic abstracts,body text,title from the Elsevier OA CC-BY corpus based on the subject areas of research. Our input includes abstract, body text, title and top 50 most important words from the body text column obtained using BERT topic modeling. Our target variable is subject areas of reserach comprising of the following 18 subject areas of research namely:

    1. Multidisciplinary (MULT) 
    
    2. Agriculture sciences (AGRI) 
    
    3. Environmental Science (ENVI)
    
    4. Bio-chemistry (BIOC)
    
    5. Medicine (MEDI)
    
    7. Material Science (MATE)
    
    8. Engineering (ENGI)
    
    9. Neuroscience (NEUR)
    
    10. Sociology (SOCI)

    11. Chemistry (CHEM) 
    
    12. Energy Studies (ENER) 

    13. Pharmacology (PHAR) 

    14. Immunology (IMMU) 

    15. Physics (PHYS) 

    16. Earth Sciences (EART) 

    17. Computer Science (COMP) 

    18. Chemical Engineering (CENG) 

Data Pre-Processing:

Outlined below is a comprehensive breakdown of our data processing methodology:

  1. Data Segmentation and Preparation:We divide the text data into segments of abstracts, titles, and body texts, and prepare them by trimming each to       specific word limits to ensure conciseness and relevance. For each document, we segment the text into three parts of sequents length 500 containing abstract (200 words), title (50 words), and body text (200 words) in the first segment followed by an additional 500 words from body text column in the second segment and an additional 500 words from the body text in the third segment. 
  
  2. Vectorization: We use the count vectorizer to transform the body text into a numerical format, targeting the top 50 words by frequency to capture the key thematic elements of the text.

  3.Topic Modeling: We employed a  BERT-based topic modeling technique to the body text to distill a set of topics that encapsulate the semantic content of the corpus, aiding in the dimensionality reduction and contextual understanding.We concatenated the abstract, title, and body text segments along with the extracted topic words for each document. This concatenated text becomes the input for the model. 
  
  4. Multi-Label Binarization and Tokenization: Subject area labels are encoded using MultiLabelBinarizer to prepare for multi-label classification, converting categorical labels into a binary format suitable for the model to process. The concatenated texts are tokenized using the SciBERT tokenizer, creating the necessary inputs for the model, including input IDs and attention masks.

Model Architecture:

Out of all the experiments conducted, the integration of SciBERT with a Convolutional Neural Network (CNN) and BERT topic modeling yielded the most favorable results. This combination emerged as the superior approach in our quest to boost the performance of text classification tasks. The SciBERT-CNN with BERT topic modeling approach significantly outperformed other models, cementing its position as our architecture of choice for the detailed task at hand.
![architecture](https://github.com/sivakumarthiyagarajan/266_project/assets/120620926/8aa96a61-321e-4133-bad0-2408e7aa24ed)

In the proposed system, we delineate a sophisticated architecture designed to enhance text classification efficacy through the harnessing of both SciBERT and convolutional neural network (CNN) methodologies. Our architecture utilizes SciBERT, fine-tuned on scientific literature, to capture contextual embeddings from the tokenized text. The  [CLS] token embeddings from SciBERT serve as a summary of the document's context and are fed into a CNN structure, which includes a convolutional layer followed by a max-pooling layer. This structure is specifically designed to capture and distill local contextual features from the embeddings.A dropout strategy is incorporated to prevent overfitting, ensuring that the model generalizes well to new, unseen data.The outputs from the CNN are passed through a dense layer to aid in high-level feature detection before being subjected to the final classification layer. The classification layer employs a sigmoid activation function to output probabilities for each of the target classes, enabling the model to perform multi-label classification. We further fine-tuned the SciBERT to align the model with the domain-specific characteristics of the Elsevier corpus. This process was essential to tailor the pre-trained model to the particular lexical and semantic features of the scientific text, optimizing performance for the classification task. A dropout strategy is incorporated to prevent overfitting, ensuring that the model generalizes well to new, unseen data.

The architecture diagram illustrates a multi-stage process for classifying scientific documents into subject areas. Initially, an Elsevier dataset comprising various text features like titles, abstracts, and body texts is subjected to class imbalance correction, where class weights are assigned to handle disproportionate label distribution. Then, BERT Topic Modeling is applied to the body text using a Count Vectorizer to identify the top 50 words, addressing the high-dimensional nature of text data.

For preprocessing, the text data is segmented: the abstract (limited to 200 tokens), title (50 tokens), BERT topic keywords (50 tokens), and body text (500 tokens for each segment) are tokenized. Special [CLS] tokens are prepended to signify the start of each segment, while [SEP] tokens are appended to indicate segment separations. This token structure aids SciBERT in understanding sentence boundaries and document structure within the context.

The tokenized and segmented text is then fed into a fine-tuned SciBERT model, which captures contextual embeddings, particularly using the [CLS] token embeddings as comprehensive representations of each segment.

Subsequently, the [CLS] embeddings are processed by a CNN, which consists of a convolutional layer with 64 filters of kernel size 5 to detect patterns, followed by a max-pooling layer of size 2 to reduce dimensionality and capture the most salient features. A dropout layer with a rate of 0.1 mitigates overfitting.

The processed embeddings then pass through a dense layer with 1024 units to further refine feature detection, culminating in a multi-label classification layer that outputs probabilities for each of the 18 target subject areas. The CNN's ability to extract localized patterns complements SciBERT's contextual understanding, making the system adept at handling the nuances of scientific text classification.

The architecture employs [CLS] and [SEP] token utilization to harness the full scope of SciBERT's capabilities, acknowledging the importance of these tokens in demarcating textual boundaries and summarizing content for effective processing through the CNN layers. The use of binarized target labels ensures the model is suitable for multi-label scenarios, predicting the probability of each document belonging to multiple subject areas simultaneously.

