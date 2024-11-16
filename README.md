# Stage de 4ème année 

Internship conducted in the ADAPT lab at DCU, Dublin, Ireland, under the supervision of Dr Annalina Caputo (https://annalina.github.io/).

## Description of the project

During my 3-month internship at the ADAPT Center at Dublin City University (DCU) in Ireland, I worked on analyzing the factors that influence student grades. The project focused on exploring and predicting final marks by using data from the university’s online Student Dashboard. This platform stores information like meeting dates and durations, how satisfied supervisors were with their students’ progress, and comments written by supervisors about the students’ work.

The first part of my work involved cleaning the non-textual data and conducting a descriptive analysis to understand which variables had the strongest impact on students’ final grades (see file `DashbordDataAnalysisPython_v8.ipynb`). After researching current NLP techniques and learning more about Transformer models, I adapted BERT to retrieve the main sentiments of supervisors’ comments to classify them as positive, negative or neutral. One of the main challenges of this internship was to apply and adapt BERT algorithm to the classification of the Dashboard text data, containing a different vocabulary from the usual datasets used to train NLP models.

To do this, I made slight modifications to the BERT architecture and employed a two-phase fine-tuning process: first on generic datasets and then on supervisor comments, which I manually labeled and augmented using techniques like back-translation and word embeddings. These adjustments ensured the model was well-suited to the unique nature of the textual data. (see file ` DashbordBERT.ipynb`)

From the structured data and the sentiments extracted, I developed machine learning models to predict students' final marks. The idea was to help supervisors notice struggling students early and provide support. (see file ` DashbordBERT.ipynb`)
I also created an interactive dashboard where supervisors could filter and visualize the data and results, giving them a clear, personalized view of student performance. (see file ` DashbordPredictionPython_v2.ipynb`).


## Note on this project organisation 

I worked primarily on my own throughout this project, using my own free Google Colab account and computer for coding. I recognize that my file structure could have been better organized (I only made notebooks). 
This was my first experience working on such a large project, and I learned a lot about data analysis, NLP, and machine learning, as well as presenting insights through visual tools. It also taught me the importance of better structuring projects for future work.

## Directory description


Stage_4A_Dublin-/
│
├── README.md          
│  
├── Project_Internship_4A/
│   
│   ├── 1-Exploratory_Analysis/ # Exploratory analysis of the data (excluding text)
│   │   ├── data/ # Data for the exploratory phase
│   │   │   ├── Meetings&marks_anonymized_v2.xlsx # Anonymized data 
│   │   │   ├── dashData_from_2022-08-12_14_49_19_full_checkpoint.pkl # Sentiment analysis results of comments using the best BERT method (3 labels: positive, negative, neutral). See “2-Sentiment_Analysis_with_BERT” for how to generate this file.
│   │   │   ├── dashData_from_2022-08-18_10_50_40_full_checkpoint.pkl # Sentiment analysis results of comments using the best BERT method (2 labels: positive, negative). See “2-Sentiment_Analysis_with_BERT” for how to generate this file.
│   │   ├── results/ # Results obtained by the DashbordDataAnalysisPython_v8.ipynb notebook
│   │   │   ├── dashboard.csv # Cleaned dashboard data in CSV format
│   │   │   ├── dashboard2.pkl # Cleaned dashboard data in pickle format
│   │   │   ├── dfProgStu.pkl # Dataframe containing student statistics
│   │   │   ├── dfProgSup.pkl # Dataframe containing supervisor statistics
│   │   │   ├── dfProgStu_s.pkl # Dataframe of student statistics for plotting stacked histograms
│   │   │   ├── dfProgSup_s.pkl # Dataframe of supervisor statistics for plotting stacked histograms
│   │   │   ├── dfPredC_2.pkl # Dataframe containing all information (non-textual data + BERT sentiment analysis for 2 labels - positive, negative) to predict students' grades (see 3-Mark_Prediction).
│   │   │   ├── dfPredC_3.pkl # Dataframe containing all information (non-textual data + BERT sentiment analysis for 3 labels - positive, negative, neutral) to predict students' grades (see 3-Mark_Prediction).
│   │   ├── /DashbordDataAnalysisPython_v8.ipynb # Notebook for pre-processing and data analysis
│
│   ├── 2-Sentiment_Analysis_with_BERT/ # Fine-tuning BERT for sentiment analysis on supervisor comments
│   │   ├── 2_DataFrame_pkl/
│   │   │   ├── 2022-08-01_17_04_14_train_0.9.pkl # Training dataset
│   │   │   ├── 2022-08-01_17_04_14_val_0.1.pkl # Validation dataset
│   │   ├── 4_ProbsValSet_pkl/
│   │   │   ├── 2022-08-01_17_04_14_probsVal.pkl # BERT model probabilities on the validation set
│   │   ├── 6_ProbsDashbord_pkl/
│   │   │   ├── dashData_from_2022-08-18_10_50_40_full_checkpoint.pkl # Predicted labels from the best BERT model
│   │   │   ├── dashProbs_from_2022-08-18_10_50_40_full_checkpoint.pkl # Predicted probabilities from the best BERT model
│   │   ├── 7_Augmented_pkl/ # Augmentation of manually labeled datasets
│   │   │   ├── 200_embeddings.pkl # Dataset augmented with embeddings
│   │   │   ├── 200_eng-de.pkl # Dataset augmented with English-German back-translation
│   │   │   ├── 200_eng-fr.pkl # Dataset augmented with English-French back-translation
│   │   │   ├── 200_eng-zh.pkl # Dataset augmented with English-Chinese back-translation
│   │   ├── data/
│   │   │   ├── annotations/ # Manual annotations of supervisor comments
│   │   │   ├── Meetings&marks_anonymized_v2.xlsx # Anonymized data
│   │   │   ├── dashbordLabel.xlsx # Dashboard data for running BERT
│   │   │   ├── miniLabel.xlsx # Dashboard data for model selection
│   │   │   ├── testLabel.xlsx # Dashboard data for testing model performance
│   │   ├── result/ # Excel files containing results from various BERT tests on different datasets
│   │   │   ├── BERT_eval_miniLabel.xlsx # Results from BERT tests on the validation set for model selection
│   │   │   ├── BERT_runs_2.xlsx # Results from BERT tests on the training set
│   │   │   ├── BERT_test_testLabel.xlsx # Results of the best BERT model on the test set
│   │   ├── DashbordBERT.ipynb # Sentiment analysis using BERT
│   │   ├── DashbordBasicNLP.ipynb # Sentiment analysis using unsupervised NLP methods as a baseline
│   
│   ├── 3-Mark_Prediction/ # Predicting students' grades
│   │   ├── data/
│   │   │   ├── dfPredC_2.pkl # Dataframe with all information (non-textual data + BERT sentiment analysis for 2 labels - positive, negative) to predict students' grades
│   │   │   ├── dfPredC_3.pkl # Dataframe with all information (non-textual data + BERT sentiment analysis for 3 labels - positive, negative, neutral) to predict students' grades
│   │   ├── result/
│   │   │   ├── PredictionResults.docx # Prediction results
│   │   ├── DashbordPredictionPython_v2.ipynb # Notebook for predicting student grades using non-textual data + sentiment analysis
│          
├── Internship_Writing_4A/
│   ├── Summary_Sheet/ # Short paragraph describing the project
│   ├── 2021-22-InternshipReport4A-Lila-Roig.pdf # Internship report
│   ├── Overleaf-2021-22-InternshipReport4A-Lila-Roig.zip # LaTeX source files for the internship report

