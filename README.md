# ID2223-LAB-2

The code for finetuning all of the different models is mostly based on the provided notebook in the lab description. We did some modifications to it in order to fit our task in the lab.

We set out to use our fine-tuned LLM to assist the user in rewriting emails on a specific mood, specifically angry/happy. We also created a UI for this task which can be found here: https://huggingface.co/spaces/The-regressors/Iris

In this lab we created 5 different fine-tuned models:
1. Llama 3.2-1B-instruct: The training parameters were the orignial ones in the provided notebook, nothing noteworthy was changed
2. Llama 3.2-1B-instruct-hyperparameter-tuned: Same setup as the orgiginal model, however as explained in "model-centric approach" below, we used different hyperparmeter settings when tuning this model
3. Llama 3.1-8B-instruct: Trained using the orignial hyperparameters, but now using a bigger model
4. Phi-3.5-instruct: Different base LLM using the orginal hyperparameters in fine-tuning
5. Llama-3.2-1B-instruct-datacentric: Orginal model using the same hyperparameters, but instead of using the provdided tome dataset we tried to fine-tune on a different dataset to better fit how we wanted to use our model.

## Below is a description and analysis of some of the results of the different models

Describe in your README.md program ways in which you can improve model performance are using

# (a) model-centric approach - e.g., tune hyperparameters, change the fine-tuning model architecture, etc
In order to improve the performance of our model, we did some hyperparameter tuning. Hyperparameters can have a big impact on the final performance, since they significantly impact training and how it is conducted. For example, lowering the learning rate might lead to less overfitting, however it risks underfitting instead, escpecially if there are not enough training steps. The learning rate schedular can also impact performance, e.g having a cosine versus linear decay. In order to try different hyperparameters, we tried a kind of random search which included changes in:

* Learning rate
* Learning rate schedular type
* Number of training steps

From our results it is hard to outline if any statistically significant improvement were made with the hyperparameter tuning. The reasons being that even though we made significant changes in the training, the models were still only trained for a portion of an epoch. This was the case since training for a whole epoch was not feasible in our time constraint given the free model used in colab to conduct the training. One of these configurations was saved as a final model.

# (b) data-centric approach - identify new data sources that enable you to train a better model that one provided in the blog post
It was difficult finding a suitable datasource that was already made that would be an obvious fit for our task. We tried finding datasets that were rewriting text, or dataset containing email conversations but to no avail. As such, we settled in trying a dataset which included conversation about mental health counseling to grasp the emotional aspect of the task we wanted our fine-tuned model to succeed in. This dataset can be found here: https://huggingface.co/datasets/Sulav/mental_health_counseling_conversations_sharegpt 


# Trying different LLMs
To find the best model for our application we tried a couple of different LLMs other than llama-3.1-1B-intrusct. Firstly we tried the bigger llama 3.1-8B-instruct. This model is significantly bigger, with a lot more parameters, as such the inference time and fine-tuning time is greater. When analyzing the results... We also tried the Phi-3.5-mini-instruct model, which is bigger than the original llama-3.1 we used. As for the results...

# Performance of the difference models
In order to evaluate the performance of the different models, we recruited help from 3 different people. These 3 people acted as evaluators. The evaluation process went as follows:
1. Each evaluator was given the same 5 emails.
2. For each model, every evaluator used our rewriting tool to rewrite each email to both angry and happy.
3. Each rewritten email was then evaluated on a 0-3 point scale following some general guidelines:
- Orginal intent
- Reasonable toneality
- Professionalism

The results can be found in a google sheet here:
To summerize, the best performing model was... and the worst...
