# Stage de 4ème année 

Internship conducted in the ADAPT lab at DCU, Dublin, Ireland, under the supervision of Dr Annalina Caputo (https://annalina.github.io/).

## Description of the project

During my 3-month internship at the ADAPT Center at Dublin City University (DCU) in Ireland, I worked on analyzing the factors that influence student grades. The project focused on exploring and predicting final marks by using data from the university’s online Student Dashboard. This platform stores information like meeting dates and durations, how satisfied supervisors were with their students’ progress, and comments written by supervisors about the students’ work.

The first part of my work involved cleaning the non-textual data and conducting a descriptive analysis to understand which variables had the strongest impact on students’ final grades (see file `DashbordDataAnalysisPython_v8.ipynb`). After researching current NLP techniques and learning more about Transformer models, I adapted BERT to retrieve the main sentiments of supervisors’ comments to classify them as positive, negative or neutral. One of the main challenges of this internship was to apply and adapt BERT algorithm to the classification of the Dashboard text data, containing a different vocabulary from the usual datasets used to train NLP models.

To do this, I made slight modifications to the BERT architecture and employed a two-phase fine-tuning process: first on generic datasets and then on supervisor comments, which I manually labeled and augmented using techniques like back-translation and word embeddings. These adjustments ensured the model was well-suited to the unique nature of the textual data(see file ` DashbordBERT.ipynb`).

From the structured data and the sentiments extracted, I developed machine learning models to predict students' final marks. The idea was to help supervisors notice struggling students early and provide support (see file ` DashbordBERT.ipynb`).
I also created an interactive dashboard where supervisors could filter and visualize the data and results, giving them a clear, personalized view of student performance (see file ` DashbordPredictionPython_v2.ipynb`).


## Note on this project organisation 

I worked primarily on my own throughout this project, using my own free Google Colab account and computer for coding. I recognize that my file structure could have been better organized (I only made notebooks). 
This was my first experience working on such a large project, and I learned a lot about data analysis, NLP, and machine learning, as well as presenting insights through visual tools. It also taught me the importance of better structuring projects for future work.

## Directory description

Stage_4A_Dublin-/
├── README.md            
├── Projet_stage_4A/
│   ├── 1-Exploratory_Analysis/ # Analyse exploratoire des données (sauf du texte)
│   │   ├── data/ # Données pour la phase exploratoire 
│   │   │   ├── Meetings&marks_anonymized_v2.xlsx # Données anonymisées 
│   │   │   ├── dashData_from_2022-08-12_14_49_19_full_checkpoint.pkl # Sentiment of the comments computed by the best BERT method (3 labels: positive, negative, neutral). See “2-Sentiment_Analysis_with_BERT” to see how to obtain this file
│   │   │   ├── dashData_from_2022-08-18_10_50_40_full_checkpoint.pkl # Sentiment of the comments computed by the best BERT method (2 labels: positive, negative). See “2-Sentiment_Analysis_with_BERT” to see how to obtain this file
│   │   ├── results/ # Résultats obtenus par le fichier DashbordDataAnalysisPython_v8.ipynb
│   │   │   ├── dashboard.csv # Cleaned dashboard data in CSV format 
│   │   │   ├── dashboard2.pkl # Cleaned dashboard data in pickle format 
│   │   │   ├── dfProgStu.pkl # Dataframe containing student statistics
│   │   │   ├── dfProgSup.pkl # Dataframe containing supervisor statistics
│   │   │   ├── dfProgStu_s.pkl # Dataframe of student statistics to plot stacked histograms
│   │   │   ├── dfProgSup_s.pkl # Dataframe of supervisor statistics to plot stacked histograms
│   │   │   ├── dfPredC_2.pkl # Dataframe containing all information (non-textual data + BERT sentiment analysis for 2 labels - positive, negative) to predict the student's grades (see 3-Mark_Prediction)
│   │   │   ├── dfPredC_3.pkl # Dataframe containing all information (non-textual data + BERT sentiment analysis for 3 labels - positive, negative, neutral) to predict the student's grades (see 3-Mark_Prediction)
│   │   ├── DashbordDataAnalysisPython_v8.ipynb # Notebook pour le pre-processing et l’analyse de données 
│
│   ├── 2-Sentiment_Analysis_with_BERT/ # Fine-tuning de BERT pour l’analyse de sentiments sur des commentaires de professeurs 
│   │   ├── 2_DataFrame_pkl/
│   │   │   ├── 2022-08-01_17_04_14_train_0.9.pkl # Training dataset
│   │   │   ├── 2022-08-01_17_04_14_val_0.1.pkl # Validation dataset 
│   │   ├── 4_ProbsValSet_pkl/
│   │   │   ├── 2022-08-01_17_04_14_probsVal.pkl # BERT model probabilities on the validation set
│   │   ├── 6_ProbsDashbord_pkl/
│   │   │   ├── dashData_from_2022-08-18_10_50_40_full_checkpoint.pkl # Predicted labels given by the best BERT model
│   │   │   ├── dashProbs_from_2022-08-18_10_50_40_full_checkpoint.pkl # Predicted probabilities given by the best BERT model
│   │   ├── 7_Augmented_pkl/ # Augmentation du dataset manuellement labellisé
│   │   │   ├── 200_embeddings.pkl # Dataset augmenté avec embeddings
│   │   │   ├── 200_eng-de.pkl # Dataset augmenté avec English-German back-translation 
│   │   │   ├── 200_eng-fr.pkl # Dataset augmenté avec English-French back-translation 
│   │   │   ├── 200_eng-zh.pkl # Dataset augmenté avec English-Chinese back-translation 
│   │   ├── data/
│   │   │   ├── annotations/ # Annotations manuelles des commentaires de superviseurs
│   │   │   ├── Meetings&marks_anonymized_v2.xlsx # Données anonymisées 
│   │   │   ├── dashbordLabel.xlsx # Données du dashboard pour exécuter BERT 
│   │   │   ├── miniLabel.xlsx # Données du dashboard pour effectuer la sélection de modèle
│   │   │   ├── testLabel.xlsx # Données du dashboard pour tester la performance du modèle 
│   │   ├── result/ # Excels contenant les résultats obtenus pour plusieurs tests de BERT sur différents datasets
│   │   │   ├── BERT_eval_miniLabel.xlsx # Résultats des tests de BERT sur le validation set pour la sélection de modèle
│   │   │   ├── BERT_runs_2.xlsx # Résultats des tests de BERT sur le training set
│   │   │   ├── BERT_test_testLabel.xlsx # Résultats des tests du meilleur modèle BERT sur le test set
│   │   ├── DashbordBERT.ipynb # Analyse de sentiments avec BERT
│   │   ├── DashbordBasicNLP.ipynb # Analyse de sentiments avec des méthodes de NLP non-supervisées pour servir de baseline
│
│   ├── 3-Mark_Prediction/ # Prédiction de la note obtenue par les élèves 
│   │   ├── data/
│   │   │   ├── dfPredC_2.pkl # Dataframe containing all information (non-textual data + BERT sentiment analysis for 2 labels - positive, negative) to predict the student's grades
│   │   │   ├── dfPredC_3.pkl # Dataframe containing all information (non-textual data + BERT sentiment analysis for 3 labels - positive, negative, neutral) to predict the student's grades
│   │   ├── result/
│   │   │   ├── ResultatsPrediction.docx # Résultats des prédictions 
│   │   ├── DashbordPredictionPython_v2.ipynb # Prédiction des notes des élèves en utilisant les données non textuelles + l’analyse de sentiments 
│
├── Redaction_stage_4A/
│   ├── Fiche_Synthèse/ # Paragraphe court décrivant le projet 
│   ├── 2021-22-RapportStage4A-Lila-Roig.pdf # Rapport de stage
│   ├── Overleaf-2021-22-RapportStage4A-Lila-Roig.zip # Latex du rapport de stage


