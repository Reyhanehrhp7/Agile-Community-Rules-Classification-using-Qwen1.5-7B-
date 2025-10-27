Part A:

I fine-tuned Qwen1.5-7B using the Hugging Face Transformers framework with the QLoRA approach and an added classification head for binary text classification.
The model was trained to classify whether a comment’s body text “complies” with or “violates” a given rule. 
I prepared the data in a conversational format compatible with Axolotl and trained it for three epochs.

Throughout training, the training loss dropped from 22.2 to 2.19 over three epochs, while the validation loss stabilized around 0.66. Accuracy improved from 0.61 to 0.78, and the F1 score rose from 0.45 to 0.79, showing clear and consistent learning. 
The validation evaluation resulted in an F1 of 0.76, while the test set achieved an F1 of 0.74, confirming that the model generalized well without significant overfitting.

Eval loss:0.755

https://wandb.ai/reyhaneh-rhp7-university-of-texas-at-dallas/huggingface/runs/8fpuzewe

Part B:

I fine-tuned Qwen1.5-7B agian using its language modeling head instead of a classification head—treating the classification task as a text generation problem.
 The model was trained to generate one of two tokens: “complies” or “violates.” To make this possible, I modified the dataset by converting all 0s to “complies” and 1s to “violates.” Each training example was formatted as a prompt: Classify the TEXT by selecting label from the following list: ['complies', 'violates'].
### TEXT: {text} ### LABEL:

The training loss decreased from 0.33 to 0.15, and the validation loss stabilized around 0.21, while the mean token accuracy remained high (≈0.90).
 This indicates that the model effectively learned to generate the correct label token given the text input. On the validation set, performance was consistent, but on the test set, the loss increased, suggesting some domain or prompt sensitivity.

Eval loss: 0.2033674120903015

Syncing run Jigsaw_PartB_training_Language_Head to Weights & Biases (docs)
View project at https://wandb.ai/reyhaneh-rhp7-university-of-texas-at-dallas/Jigsaw_PartB_training_Language_Head
View run at https://wandb.ai/reyhaneh-rhp7-university-of-texas-at-dallas/Jigsaw_PartB_training_Language_Head/runs/jiz99kil


Part C:

I used the same model architecture—Qwen1.5-7B but instead of adding a classification head, I fine-tuned it using the language modeling head within Axolotl. 
Each training example was then reformatted into an instruction-style prompt using a structured template. The prompt guided the model to behave as a rule compliance analyst, showing subreddit context, the rule, positive and negative examples, and finally the target comment for classification.
During training, the model achieved a training loss of 1.82 and a validation loss of 1.78, indicating stable learning and effective adaptation to the instruction-following task. 

View run PartC_Training_Instruction_Model at: https://wandb.ai/reyhaneh-rhp7-university-of-texas-at-dallas/PartC_Training_Instruction_Model/runs/kyjvp1lh
View project at: https://wandb.ai/reyhaneh-rhp7-university-of-texas-at-dallas/PartC_Training_Instruction_Model
Synced 5 W&B file(s), 0 media file(s), 0 artifact file(s) and 0 other file(s)