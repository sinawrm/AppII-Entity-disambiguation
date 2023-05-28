# AppII-Entity-disambiguation
Application II: Entity disambiguation with Information Extraction (I.E), Information Retrieval (I.R), and Question Answering (Q.A.)

We build an app able to answer 3 questions (date of birth, nationality, occupation) of people who has a biography page in Wikipedia[1] once it reads them in some text. The app recognizes the name of the person, extracts the necessary documents from a collection of Wikipedia texts, retrieves the specific information needed and answers the questions. 

## 1. Data collection
Using ChatGPT[2]  we have created a random set of 20 popular figures of diverse backgrounds. We have generated 60 paragraphs. The paragraphs did not include the info that would be asked but provided general context to recognize the person in question. 
We simulate Wikipedia collection by extracting 200 articles that  each article consists of the first 2 or 3 paragraphs

## 2.A Name Entity Recognition
We use spaCy[3] to extract the first named entity with “PERSON” Label from the 60 paragraphs generated in (1).

## 2.B Information Retrieval
Using Whoosh[4] search engine library, we index the 200 articles and apply BM25 retrieval function[5], we use the paragraph as the query that we want to match and we select the retrieved Wikipedia file with the highest score.

## 3. Question Answering
We use BERT model that is fine-tuned on SQuAD dataset[6]. We craft three queries that is enriched with the extracted name from (2.A) to answer the three questions using the retrieved document (2.B). We select the text span with the highest start and end scores.

## 4. Evaluation
We retrieved gold information (date of birth, nationality, and occupation) through querying Wikidata[7] base endpoint using a handcrafted SPARQL query to retrieve the information for the people in the dataset.

## References
[1] https://www.wikipedia.org/

[2] https://openai.com/blog/chatgpt

[3] https://spacy.io/

[4] https://github.com/mchaput/whoosh

[5] https://huggingface.co/spaces/tcvieira/bm25-information-retrieval

[6] https://huggingface.co/bert-large-uncased-whole-word-masking-finetuned-squad

[7] https://www.wikidata.org/wiki/Wikidata:Main_Page
