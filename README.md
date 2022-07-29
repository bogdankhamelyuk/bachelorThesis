# Recognition of commands spoken in dialect
## Introduction

This paper explores the possibility of recognising the Vorarlberg dialect of German language using modern speech recognition models. The models used were the monolingual Wav2Vec developed by Facebook and its multilingual analogue XLSR. Both models were finetuned with the collected speech samples of the dialect. The XLSR additionally pre-trained for German (XLSRDe) was also used, which was later finetuned to the dia-lect as well. The quality of the results was measured with the word error rate (WER). 

## Hypothesis 
Based on the "Using Large Self-Supervised Models for Low-Resource Speech Recognition." from of Krishna D. N. et al. and "Unsupervised Cross-lingual Representation Learning For Speech Recognition." from Alexis Conneau et al. the main hypothesis of the work is whether to prove or not the claim, that multilingual models perform better on Low-Resource languages than monlingual. Low-Resource languages in this context are the languages which are merely not represented in internet. The dialects of voralrberg can be counted to those kind of languages, since there is no pre-made datasets and no labeled data at all. It is also expected, that XLSRDe will perform better than other models, because it is already trained for the closely related langauge. 


## Goals
### Main Goal
Main goal of the work is to implement speech recognition of vorarlberg dialect using modern automatic speech recognition (ASR) models such as Wav2Vec, XLSR, and XLSRDe. 

### Sub-Goals
Since there were no datasets available, it was decided to create some datasets and make them publicly accessible. They can be still found in this repository. For speeding up collection of the audios was also decided to create simple website on django and flask frameworks. Their implementation will be described afterwards.

## Implementation  
### Collecting of Audio
Collecting of audios was made in two ways: externally and manually. In the first option there was Django-based website created and deployed using Microsoft Azure. This website consisted from two parts: survey and pages with the sentences to read.
<img width="550" alt="image" src="https://user-images.githubusercontent.com/71139952/181834105-18b8ab30-2c3b-42ef-8e2c-969d77a5121d.png">
<img width="337" alt="image" src="https://user-images.githubusercontent.com/71139952/181834121-f1855100-0efe-4ba4-8e7a-1309291d9ced.png">

The pronounced sentences were simultaneously sent to the Flask server running on Raspberry Pi. Using PiTunnel (https://www.pitunnel.com/) the local Flask server could gain URL, what has allowed to receive incoming "POST" requestes from the whole internet. 
In the manual way of audio collection speech examples were recorded from public sources, such as "Dornbirner Mundart Lexikon" and "d'Sprôôch - Lustenauer Wörterbuch". 
<img width="938" alt="image" src="https://user-images.githubusercontent.com/71139952/181826139-36676886-bba2-4aac-92a1-97ddc25b5640.png">

As audios were well organised into datasets they were used for fine-tuning of the models. Implementatiщт of the fine-tuning was taken from HuggingFace tutorial: Fine-tuning XLS-R for Multi-Lingual ASR with 🤗 Transformers. Similarly a GoogleColab Pro was used. So the ASR Models were downloaded from Hugging Face and used in GoogleColab environment. As the training (fine-tuning) was completed the fine-tuned models were uploaded to the Hugging Face Hub, where they are still stored.

<img width="880" alt="image" src="https://user-images.githubusercontent.com/71139952/181835582-8b9d2b8c-ae8b-4e90-a96b-7a353e87b3f6.png">

## Results
Results show that by the increasing number of audios the quality of recognition also increases (the less Word Error Rate (WER) - the better). 

<img width="812" alt="image" src="https://user-images.githubusercontent.com/71139952/181838726-ed7c5727-0ce9-4e0d-9d2c-d00e6faca1c0.png">

It also can be seen, that XLSRDe performs mostly worser than other models. So by the dataset consisting solely from Lustenau expressions XLSRDe had WER equal to 1.208 , which was the worst result, in comparison to other models. There were, though, other datasets such as "Dataset-21DL" and "Dataset-DL", where XLSRDe was the best one. 

Looking more precisly on the reasons of such behavior it may be assumed, that best performance of XLSRDe is achieved, when datasets have more than 700 outspoken words (without repetitions). 

<img width="809" alt="image" src="https://user-images.githubusercontent.com/71139952/181838762-0ce0af35-fb49-4fe6-bb40-93e35e88a3ec.png">

As as a summary, the general performance may be judged from the graph underneath. It is clearly seen that XLSR achieves averagely the better WER and its value distribution is also the smallest one, in comparison to other models. 
<img width="718" alt="image" src="https://user-images.githubusercontent.com/71139952/181839312-b00b2a65-bf76-401b-8ed2-3f9c9f9b8c88.png">

