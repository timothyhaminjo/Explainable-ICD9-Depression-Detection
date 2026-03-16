# Explainable-ICD9-Depression-Detection

This project develops an explainable natural language processing (NLP) model to detect depression-related signals from clinical discharge summaries.

Clinical coding systems such as ICD-9 are widely used for documenting diagnoses, but manual coding can be time-consuming and inconsistent. This project explores whether machine learning and clinical language models can assist in identifying depression from unstructured clinical notes while maintaining transparency in the model’s predictions.

The system fine-tunes a clinical language model on ICU discharge summaries from the MIMIC-III dataset and integrates SHAP explanations to highlight which parts of the text contributed most to each prediction.


# Dataset 
## MIMIC-III Clinical Database
This project uses discharge summaries from the MIMIC-III dataset, a publicly available critical care database containing de-identified electronic health records. Only the discharge summaries were used for analysis. 

## Target Label 
Depression was identified using the ICD-9 diagnosis code, 311. I used the binary classification, where 1 signifies detection and 0 signifies no detection. 

# Methods
## Preprocessing 
Clinical notes were cleaned and prepared for modeling using the following steps:

- Extract discharge summaries
- Remove duplicate records
- Convert text to lowercase
- Remove irrelevant tokens
- Tokenize text for transformer models

## Model Architecture 
The project fine-tunes BioDischargeBERT, a transformer model pre-trained on clinical discharge summaries.

Model pipeline was as the following:

Clinical Notes
      ↓
Tokenization
      ↓
BioDischargeBERT
      ↓
Binary Classification Layer
      ↓
Depression Prediction

## Explainability 
To improve transparency, SHAP (SHapley Additive exPlanations) was used to interpret model predictions.

SHAP highlights words in the clinical note that contributed to the prediction.

Example interpretation:
"history of depression" → strong positive signal
"no psychiatric history" → negative signal

This allows clinicians and researchers to understand why the model made a prediction. 

## Model Performance 

Model performance was evaluated using standard classification metrics. AUROC: 0.87, Accuracy: 0.79, Precision: 0.76, Recall: 0.83, and F1 Score: 0.79

# Streamlit Demo 
A Streamlit web application was developed to make the model interactive.

Users can input a clinical note and receive:

- Depression prediction
- Probability score
- SHAP explanation highlighting influential text

The limitation was the processing speed. After inputing the text, it would sometimes take minutes before the results show up. Reducing the processing speed is a future direction of research. 

# Key Takeaways 
This project demonstrates:

- Application of clinical language models for mental health signal detection
- Integration of explainable AI techniques in healthcare NLP
- Development of an interactive interface for model interpretation

The goal is not to replace clinical coding but to explore how AI can support more consistent identification of mental health conditions from clinical documentation.


