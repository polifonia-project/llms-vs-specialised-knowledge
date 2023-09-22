## Comparison with Large Language Models - Pilot Study

### Background

We expect Large Language Models to be potentially unreliable in
downstream tasks like Question Answering (QA) due to their sensitivity
to prompting, hallucinations and disinclination to retain long-tail
knowledge, namely knowledge that rarely appears in their training
datasets. The work stored in this repo is
driven by the hypothesis that building Knowledge Graphs (KGs) from text
through a neuro-symbolic text-to-KG pipeline can give higher control
over the knowledge extracted and, consequently, a higher quality of the
information retrieved by querying.

### Examples

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

| **Named entity's gender** | **ChatGPT's answer correct? (Yes)** | **ChatGPT's answer correct? (No)** | **Grand Total** |
|---------------------------|----------------------------------|---------------------------------|-----------------|
| F                         | 11 (22%)                         | 39 (78%)                        | 50 (100%)       |
| M                         | 24 (48%)                         | 26 (52%)                        | 50 (100%)       |
| Grand Total               | 35 (35%)                         | 65 (65%)                        | 100 (100%)      |

| Named entity's gender | Does the AMR graph contain an answer to the question? (Yes)| Does the AMR graph contain an answer to the question? (No) |
|-----------------------|------------------------------------------------------------|------------------------------------------------------------|
|                       | Yes  | No |                 |
| F                     | 7 (70%)| 3 (30%)| 10 (100%) |
| M                     | 8 (80%) | 2 (20%) | 10 (100%)|
| Grand Total           | 15 (75%) | 5 (25%) | 20 (100%)|

| Named entity's gender | Does the AMR graph contain an answer to the question? (Yes)| Does the AMR graph contain an answer to the question? (No) | Grand Total |
|-----------------------|------------------------------------------------------------|------------------------------------------------------------|-------------|
|                       | Yes  | No |                 |
| F                     | 7 (70%)| 3 (30%)| 10 (100%) |
| M                     | 8 (80%) | 2 (20%) | 10 (100%)|
| Grand Total           | 15 (75%) | 5 (25%) | 20 (100%)|
