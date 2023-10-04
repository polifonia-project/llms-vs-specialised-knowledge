---
component-id: llms-vs-specialised-knowledge
name: LLMs VS Specialised Knowledge
description: Results of the comparative study between knowledge extracted through our Knowledge Extraction pipeline and information that can be obtained by asking off-the-shelf Large Language Models.
type: Dataset
release-date: 30/09/2023
release-number: v0.1
work-package: 
- WP4
licence: CC-BY_v4
links:
- https://github.com/polifonia-project/llms-vs-specialised-knowledge
credits:
- https://github.com/roccotrip
- https://github.com/arianna-graciotti
---


# Comparison with Large Language Models - Proof-of-Concept Study

We conducted a Proof-of-Concept study to compare:
- the information that can be obtained by querying the knowledge extracted through our Knowledge Extraction pipeline ([Polifonia Knowledge Extractor](https://github.com/polifonia-project/Polifonia-Knowledge-Extractor) and [AMR2FRED](https://github.com/polifonia-project/amr2Fred), called through the [Text2AMR2FRED APIs](http://framester.istc.cnr.it/txt-amr-fred/api/docs/) and [Text2AMR2FRED WebApp](https://arco.istc.cnr.it/txt-amr-fred/));
- the information that can be obtained by asking off-the-shelf Large Language Models, like the [free online version of ChatGPT](https://chat.openai.com/). This study was held in August 2023.

This repository contains the results of this study, reported in a [spreadsheet](https://github.com/polifonia-project/llms-vs-specialised-knowledge/blob/main/data/LLMs_vs_Text2KGs_QuestionAnswering.xlsx).


## Background

We expect Large Language Models to be potentially unreliable in
downstream tasks like Question Answering (QA) due to their sensitivity
to prompting, hallucinations and disinclination to retain long-tail
knowledge, namely knowledge that rarely appears in their training
datasets. The work stored in this repo is
driven by the hypothesis that building Knowledge Graphs (KGs) from text
through a neuro-symbolic text-to-KG pipeline can give higher control
over the knowledge extracted and, consequently, a higher quality of the
information retrieved by querying.

## Method

We framed the comparison experiment as a Question Answering task on named entities of type `person`. We compared GPT3.5's free-text answers to natural language questions, sent as prompts via the [free online version of ChatGPT](https://chat.openai.com/), to AMR graphs produced by [Text2AMR2FRED](https://arco.istc.cnr.it/txt-amr-fred/)). 

The human evaluators that carried out the experiments are University of Bologna's Foreign Languages and Literature undergraduate students who received training and carried it out as part of their bachelor's degree curricular internship.

The experiment breaks down into two macro-steps.

### Macro-step 1

1. _Question formulation, ChatGPT prompting, ChatGPT's answer collection and evaluation_
   
--> 1.a. Human evaluators selected a named entity of type `person` occurring in [Musical heritage Historical Named Entities Recognition, Classification and Linking (MHERCL)](https://github.com/polifonia-project/historical-entity-linking), a dataset of sentences extrapolated from the [Polifonia Textual Corpus](https://github.com/polifonia-project/Polifonia-Corpus) that comprises music periodicals whose publication dates range from 1823 to 1900. Therefore, the `person` named entities occurring in it are related to music and known to be active or alive in a period similar to the periodicals' publication dates range;
   
--> 1.b. Human evaluators were instructed to maintain a 50-50 gender distribution between the selected `person` named entities. As a result, half of the questions focused on men, and the other half on women historical characters. Due to the nature of the dataset, they were extrapolated from, all the selected historical characters could not belong to significantly different periods;

 
--> 1.c. Human evaluators accessed the selected `person` named entity's Wikipedia page;
 
--> 1.d. Human evaluators asked a question related to the named entity chosen at step 1.a to GPT3.5 in the free online version of ChatGPT via a single prompt containing the question. N.B.: The question had to be answerable with information retrievable in the Wikipedia page of reference, visited in step 1.c.;
 
--> 1.e. Human evaluators assessed the correctness of the answer given by ChatGPT.

### Macro-step 2

2. _Text2AMR semantic parsing evaluation_

--> 2.a The human evaluator transforms the sentence(s) from the Wikipedia page that contains the answer to the question formulated at step 1.d into an AMR graph via [Text2AMR2FRED WebApp](https://arco.istc.cnr.it/txt-amr-fred/);

--> 2.b The human evaluator assesses the semantic correctness of the AMR graph under the assumption that if the AMR graph is semantically correct (namely, the predicates recognised by the Text2AMR parser and their arguments are correct), [AMR2FRED](https://github.com/polifonia-project/amr2Fred) will translate it into an RDF/OWL KG able to provide the correct answer to a question via a SPARQL query.


## Examples

The examples reported in the tables below are intended to illustrate the content of the results [spreadsheet](https://github.com/arianna-graciotti/llms-vs-specialised-knowledge/blob/main/data/LLMs_vs_Text2KGs_QuestionAnswering.xlsx) stored in this repository.

| **Named entity's Wikipedia page**             | **Gender** | **Human Evaluator's Question**                                           | **Human Evaluator's Prompt**                                                                      | **Human Evaluator's Answer** | **Sentence \(from Wikipedia page\) containing the answer**                                                                                                                                                                                                                                                                                                                                                   | **Is ChatGPT's answer correct?** | **ChatGPT's answer**                                                                                                                                                                                                                                                                                                                                                  |
|-----------------------------------------------|------------|--------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------|------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Giovanni_Battista_Pergolesi | M          | What is the original name of Giovanni Battista Pergolesi?                | What is the original name of Giovanni Battista Pergolesi? Give a straight answer\.                | Giovanni Battista Draghi     | Giovanni Battista Draghi \(\[\.\.\.\]; 4 January 1710 – 16 or 17 March 1736\), often referred to as Giovanni Battista Pergolesi \[\.\.\.\], was an Italian Baroque composer, violinist, and organist, leading exponent of the Baroque; he is considered one of the greatest Italian musicians of the first half of the 18th century and one of the most important representatives of the Neapolitan school\. | Yes                              | The original name of Giovanni Battista Pergolesi is Giovanni Battista Draghi\.                                                                                                                                                                                                                                                                                        |
| George_Frideric_Handel      | M          | Who was the headmaster of George Frideric Handel's Gymnasium?            | Who was the headmaster of George Frideric Handel's Gymnasium? Give a straight answer\.            | Johann Praetorius            | Early in his life Handel is reported to have attended the Gymnasium in Halle, where the headmaster, Johann Praetorius, was reputed to be an ardent musician\.                                                                                                                                                                                                                                                | No                               | Johann Zacharias Grundig was the headmaster of George Frideric Handel's gymnasium in Halle, Germany\.                                                                                                                                                                                                                                                                 |
| Mary_Ann_Paton              | F          | Where did Mary Ann Paton's sister Isabella make her début as a musician? | Where did Mary Ann Paton's sister Isabella make her début as a musician? Give a straight answer\. | Covent Garden Theatre        | She and her sisters received a good musical training: they were singers also, Isabella making her début at Mary Ann's benefit at Covent Garden Theatre, 1824, as Letitia Hardy, and Eliza sing at the Haymarket Theatre in 1833\.                                                                                                                                                                            | No                               | Isabella Paton made her début as a musician at the Covent Garden Theatre in London\.                                                                                                                                                                                                                                                                                  |
| Teresina_Brambilla             | F          | How long was Teresina Brambilla's career as a musician?                  | How long was Teresina Brambilla's career as a musician? Give a straight answer\.                  | 25 years                     | Teresa "Teresina" Brambilla\[a\] \(15 April 1845 – 1 July 1921\) was an Italian soprano who sang in the major opera houses of Europe in a career spanning 25 years\.                                                                                                                                                                                                                                         | No                               | As of my last knowledge update in September 2021, there is no widely known or documented musician by the name of Teresina Brambilla in the public domain\. Therefore, I cannot provide information about the length of her musical career\. It's possible that she gained recognition after my last update or that she is not a prominent figure in the music world\. |

| **Named entity's Wikipedia page**             | **Gender** | **Human Evaluator's Question**                                           | **Human Evaluator's Answer** | **Sentence**                                                                                                                                                                                                                                                                                                                                                                                                 | **Does the AMR graph contain an answer to the question?** | **AMR subgraph containing (or not) the answer** |
|-----------------------------------------------|------------|--------------------------------------------------------------------------|------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------|---------------------------------------------------|
| Giovanni_Battista_Pergolesi | M          | What is the original name of Giovanni Battista Pergolesi?                | Giovanni Battista Draghi     | Giovanni Battista Draghi ([...]; 4 January 1710 – 16 or 17 March 1736), often referred to as Giovanni Battista Pergolesi [...], was an Italian Baroque composer, violinist, and organist, leading exponent of the Baroque; he is considered one of the greatest Italian musicians of the first half of the 18th century and one of the most important representatives of the Neapolitan school. | Yes                                                       ||
| George_Frideric_Handel      | M          | Who was the headmaster of George Frideric Handel's Gymnasium?            | Johann Praetorius            | Early in his life Handel is reported to have attended the Gymnasium in Halle, where the headmaster, Johann Praetorius, was reputed to be an ardent musician.                                                                                                                                                                                                                                                | no                                                        | |
| Mary_Ann_Paton              | F          | Where did Mary Ann Paton's sister Isabella make her début as a musician? | Covent Garden Theatre        | She and her sisters received a good musical training: they were singers also, Isabella making her début at Mary Ann's benefit at Covent Garden Theatre, 1824, as Letitia Hardy, and Eliza sing at the Haymarket Theatre in 1833.                                                                                                                                                                            | No                                                        | |
| Teresina_Brambilla             | F          | How long was Teresina Brambilla's career as a musician?                  | 25 years                     | Teresa "Teresina" Brambilla (15 April 1845 – 1 July 1921) was an Italian soprano who sang in the major opera houses of Europe in a career spanning 25 years.                                                                                                                                                                                                                                              | Yes                                                       | |

## Results

The tables below report the results of the experiment.

Looking at the results, we can see that ChatGPT tend to return wrong answers more often when prompted with questions about women. This observation might corroborate the hypotheses regarding gender bias in LLMs (as reported in recent studies such as [Marked Personas: Using Natural Language Prompts to Measure Stereotypes in Language Models](https://aclanthology.org/2023.acl-long.84) (Cheng et al., ACL 2023)) and in Knowledge Bases such as Wikipedia (as reported in recent studies such as [WikiBio: a Semantic Resource for the Intersectional Analysis of Biographical Events](https://aclanthology.org/2023.acl-long.691) (Stranisci et al., ACL 2023)).

| **Named entity's gender** | **ChatGPT's answer correct? (Yes)** | **ChatGPT's answer correct? (No)** | **Grand Total** |
|---------------------------|----------------------------------|---------------------------------|-----------------|
| F                         | 11 (22%)                         | 39 (78%)                        | 50 (100%)       |
| M                         | 24 (48%)                         | 26 (52%)                        | 50 (100%)       |
| Grand Total               | 35 (35%)                         | 65 (65%)                        | 100 (100%)      |

As this is a Proof-of-Concept study aimed at exploring the feasibility of the research approach of Text2AMR2FRED VS LLMs comparison, we opted for a smaller sample size for the experiment's macro-step 2, as AMR graphs assessment is challenging and time-consuming. Results of the experiment's macro-step 2., are reported in the table below.

Although the small sample size is a limitation of this Proof-of-Concept study, especially for the experiment's macro-step 2, it is noteworthy that answers are included in the AMR graphs without apparent major bias toward the gender of the entities involved.

| Named entity's gender | Does the AMR graph contain an answer to the question? (Yes)| Does the AMR graph contain an answer to the question? (No) | Grand Total |
|-----------------------|------------------------------------------------------------|------------------------------------------------------------|-------------|
|                       | Yes  | No |                 |
| F                     | 7 (70%)| 3 (30%)| 10 (100%) |
| M                     | 8 (80%) | 2 (20%) | 10 (100%)|
| Grand Total           | 15 (75%) | 5 (25%) | 20 (100%)|

The last table, reported below, shows a comparison between the ChatGPT answers' correctness and the AMR graphs informativeness (namely, the presence, in the graph, of the answer to the question or not). The AMR graphs are produced according to experiment's macro-step 2 methodology. The comparison was performed on a random sub-sample of 20 questions asked about 20 person named entities, extrapolated from the sample collected in Experiment's macro-step 1. 

| Named entity's gender | Does the AMR graph contain an answer to the question? (Yes)| Does the AMR graph contain an answer to the question? (No) | Is ChatGPT's answer correct? (Yes) | Is ChatGPT's answer correct? (No) | Grand Total |
|-----------------------|------------------------------------------------------------|------------------------------------------------------------|------------------------------------|-----------------------------------|-------------|
| F                     | 7 (70%)| 3 (30%)| 1 (10%) | 9 (90%) | 10 (100%) |
| M                     | 8 (80%) | 2 (20%) | 2 (20%) | 8 (80%) | 10 (100%) |
| Grand Total           | 15 (75%) | 5 (25%) | 3 (15%) | 17 (85%) | 20 (100%)|

In spite of the constraints imposed by a small sample size, the table shows that *the AMR graphs effectively capture the answers to the questions 75% of the times*, while *ChatGPT's answer is correct 15% of the times*.

### Future work

In future work, we plan to quantitatively expand the samples of the experiment whose Proof-of-Concept methods and results described and stored in this repository. We aim to expand the experiment's methodology more broadly and examine the interplay between gender and popularity bias along the lines of recent investigations (such as the one reported in [Evaluating Entity Disambiguation and the Role of Popularity in Retrieval-Based NLP](https://aclanthology.org/2021.acl-long.345) (Chen et al., ACL-IJCNLP 2021)) and push forward the research regarding LLMs struggle with long-tail knowledge (as reported in [Large Language Models Struggle to Learn Long-Tail Knowledge](https://proceedings.mlr.press/v202/kandpal23a.html) (Kandpal et al., PMLR 2023)). Also, we plan to expand the experiment's macro-step 2 by building SPARQL queries to verify the informativeness of the Text2AMR2FRED OWL-compliant RDF output KGs through structured interrogations.
