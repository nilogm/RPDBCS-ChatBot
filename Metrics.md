# Evaluation through Common Literature Metrics
In order to provide a complete evaluation through well-known metrics (and also adaptations), responses from the model were also evaluated using:
- Rouge-L [[1]](#1)
- Ragas' Semantic Similarity (w/ [sentence-transformers/all-mpnet-base-v2](https://huggingface.co/sentence-transformers/all-mpnet-base-v2))
- BERTScore (Recall, Precision and F1) [[2]](#2)
- Perplexity (PPL)

As the metrics above cannot directly show if the answers given are correct, an adaptation to the metric was proposed.
To do that, three wrong answers were created for each entry in the dataset.
Each wrong answer presents a variation of the correct answer, however, with incorrect information.
Examples of entries in the dataset can be seen in the table below.

 | Question | Correct Answer | Wrong Answer 1 | Wrong Answer 2 | Wrong Answer 3 |
 | - | - | - | - | - | 
 | What is it possible to change in the report's cover in RPDBCS? | A user can change the image cover and the report's confidentiality level | A user can change the image cover, the confidentiality level and can insert the author's names on the report's cover. | A user can change only the image cover. | A user can change only the confidentiality level. | 
 | How is it possible to access the learning curves in RPDBCS? | To access the learning curves screen, select the "Learning Curves" option in the "Learning" tab on the top menu bar. | Acessing the "Learning Curves" option in the "View" on the main screen. | It is necessary to search for the "Learning Curve" on the top search bar. | To acess the screen, it is necessary to select the "Learning" option in the "View" tab. | 

In order to evaluate the answers, the base metric is used to provide scores for each of the answers (correct and incorrect) of a question in the dataset
Then, the answer with the best score (for BERTScore, the highest score; for Perplexity, the lowest score) is selected as the option the assistant would deem most correct out of them.
The new types of metrics are:

- **BERTScore Multiple Choice Recall/Precision/F1**: the system-generated answer and the wrong answers are compared to the correct answer using BERTScore. The highest scoring answer is the one closest to the "Correct Answer" in the dataset. If this answer is not the assistant-generated one, the configuration set does not score.
- **Multiple Choice Perplexity**: the PPL value is calculated for the correct and incorrect answers in the dataset. The answer with the lowest PPL value is deemed the one the assistant would most likely answer. If the answer is not the "Correct Answer" from the dataset, the configuration set does not score.

Hopefully, the figures shown below can display the limitations of the metrics in this paper's problem, as results are inconclusive (as there isn't a clear best configuration set upon analysis). Therefore, the handmade analysis was preferred, even if a greedy approach had to be done.

## Experiment 1: Choosing the best model combination for the assistant
![scores_exp1](https://github.com/user-attachments/assets/760c9fb6-3ce6-4288-a9f0-117b1267d31e)

## Experiment 2: Choosing the best parametrization for the context initialization
![scores_exp1_1](https://github.com/user-attachments/assets/d32e0dd9-9e3a-4270-8b25-4187affc0fed)

## Experiment 3: Choosing the best parametrization for the search
![scores_exp1_2](https://github.com/user-attachments/assets/f7b798c5-2a7e-4165-a627-e475c2e6d223)

## Experiment 4: Analyzing the efficiency of the summary extension
![scores_exp2](https://github.com/user-attachments/assets/d0f1e3eb-c69b-46df-8725-dc56173243cf)

## Experiment 5: Final Experiment
![scores_exp3](https://github.com/user-attachments/assets/f5fddef8-05c3-48fa-b37c-ad3d437d2f9e)

# References
<a id="1">[1]</a>
Chin-Yew Lin and Franz Josef Och. 2004. Automatic Evaluation of Machine Translation Quality Using Longest Common Subsequence and Skip-Bigram Statistics. In Proceedings of the 42nd Annual Meeting of the Association for Computational Linguistics (ACL-04), pages 605–612, Barcelona, Spain.

<a id="2">[2]</a>
Tianyi Zhang and Varsha Kishore and Felix Wu and Kilian Q. Weinberger and Yoav Artzi. 2020. BERTScore: Evaluating Text Generation with BERT. 1904.09675. https://arxiv.org/abs/1904.09675
