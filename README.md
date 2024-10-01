# Bachelorthesis_CDS_fine-tuning
Fine-tuning GPT 3.5 - Turbo for CDS generation
Python-version: 3.12.3

Disclaimer: This Repo is only to illustrate the fine-tuning approach and serves as inspiration/hollastic overview for how to fine-tune GPT 3.5- Turbo in regards to CDS.

The following illustartes the structure of the fine-tuning approach: 

![fine-tuning pipline](https://github.com/user-attachments/assets/94b87a0b-6ff4-4c92-a1bd-7c38009d5155)

The dataset, which is colleceted and labled (data102.jsonl), is illustrated as the "self-created dataset". This data is checked through "dataPrepJob.ipynb". This data then is shuffeled (data.jsonl) and splitted (70-30 and 80-20 folders). The 80-10-10 Split, including validation Dataset, is taken for the fine-tuning and getting insights in the training process (finetuning_jobs-80-20.ipynb). 

After the model is fine-tuned, test data should be devided in two parts one "For Chat Completion" and another for checking the answer ("Right Answer"). (Generation&Evaluation Pipline.ipynb) The first part then can be fed to the fine-tuned and untuned model and the results can be generated which are saved in "Base-DF-W-ft-&-UT-consumation.pkl".

This pickle file is then the basis for the evaluation. Firstly all data are cleared from any markups in form of " ''' cds .... ''' " or any code explanation that GPT genberated and only code or better said CDS is taken for the valuation. For the first part of the evlauation the CDS are put through the compiler and checked for their syntax. For the second part, which is the semantic error-rate, it is needed that metadata are being created. This metadata are created in "Building_Metadata.ipynb" manually using the [CSN-notation](https://cap.cloud.sap/docs/cds/csn) of the code, which is an internal JSON representation and deliver more insights in the CDS model. With this metadata being created then the semantic evaluation in "Generation&Evaluation Pipline.ipynb" can take place and error-rate can be calculated.  
