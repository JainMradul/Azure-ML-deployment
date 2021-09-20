
# Operationalizing Machine Learning

In this project, the UCI Bank Marketing dataset is used to predict whether the bank's clients will open a term deposit with them or not. So, this is a binary classification problem which requires predicting 'yes' or 'no'

Dataset consist of 40 columns and ~33k rows

Broadly classifying, independent variables consist of customers demographics,employment status,qualification, education and marital status information.

Here is a list of all the columns available in dataset:

>      'age', 'marital', 'default', 'housing', 'loan', 'month', 'day_of_week',
>      'duration', 'campaign', 'pdays', 'previous', 'poutcome', 'emp.var.rate',
>      'cons.price.idx', 'cons.conf.idx', 'euribor3m', 'nr.employed',
>      'job_admin.', 'job_blue-collar', 'job_entrepreneur', 'job_housemaid',
>      'job_management', 'job_retired', 'job_self-employed', 'job_services',
>      'job_student', 'job_technician', 'job_unemployed', 'job_unknown',
>      'contact_cellular', 'contact_telephone', 'education_basic.4y',
>      'education_basic.6y', 'education_basic.9y', 'education_high.school',
>      'education_illiterate', 'education_professional.course',
>      'education_university.degree', 'education_unknown', 'y' 

Broadly 2 approaches are used to operationalize: 

1. AutoML run through UI 
2. Pipeline run through python SDK

The model with the highest accuracy is deployed as an endpoint using Azure Container Instance (ACI). Through the ACI, the REST endpoint with authentication is used to access the model via API documentation enabled by Swagger.

## Architectural Diagram
![architecture](https://github.com/JainMradul/Azure-ML-deployment/blob/main/screenshots/architecture.PNG)

- [x] DataSet is loaded in AutoML run via UI and through python SDK (jupyter notebook)
- [x] Model is trained and deployed manually using UI 
- [x] Above process is automated via Pipeline and best model is deployed through ACI endpoint
- [x] API documentation is accessed via swagger and application insights are enabled to keep track of logs
- [x] End user can interact via ACI endpoint or pipeline endpoint

## Key Steps 

## 1. Upload and Register Dataset 
The first step is to upload the [Bank Marketing dataset](https://automlsamplenotebookdata.blob.core.windows.net/automl-sample-notebook-data/bankmarketing_train.csv) and register it on the ML Studio

![dataset](Screenshots/dataset.png)


## 2. AutoML run on compute cluster

In the next step, the automated ML run is initiated by configuring a compute cluster and selecting the uploaded dataset for the experiment. The completed experiment goes through some iterations and outputs a best model.

![run](Screenshots/automl-complete.png)

## 3. Best performing model

The best model is a collection of classifiers - Voting Ensemble - with an accuracy of nearly 92%.

![model](Screenshots/best-model.png)

## 4. Deploy the best model

We now proceed to deploy the best model as an Azure Container Instance with authentication enabled.

![deploy](Screenshots/deploy1.png)


## 5. Enable logging and view logs

The deployed model is updated to enable logging of application insights. The logs can be viewed by running the logs.py script.

![logs](Screenshots/deploy2.png)
![logging](Screenshots/logs.png)


## 6. Swagger documentation of API and endpoints

The deployed model API documentation is served up on Swagger. The model endpoints can be consumed via HTTP requests and a JSON input payload by running the endpoint.py script.

![swagger1](Screenshots/swagger1.png)
![swagger2](Screenshots/swagger2.png)
![swagger3](Screenshots/swagger3.png)

![API](Screenshots/endpoint.png)


## 7. Pipeline run via Jupyter notebook

This is the second part of operationalising where the experiment is run via pipeline powered by the Python SDK. A Jupyter notebook runs with the same compute cluster attached as in the AutoML run and the same dataset as before. The details can be viewed via the RunDetails widget and the dataset shows up as an AutoML module in the pipeline. 

![pipeline](Screenshots/pipeline.png)

![rundetails](Screenshots/rundetails.png)

![automl](Screenshots/pipeline-run.png)


## 10. Publish pipeline and deploy as endpoint

Once the pipeline run completes, the pipeline can be published with an endpoint to enable automation of the task if it is needed again. The published pipeline status and endpoint can be viewed on the ML Studio as well as a scheduled run with the said pipeline

![1](Screenshots/pipeline-endpoint.png)
![2](Screenshots/pub-pipeline.png)
![3](Screenshots/pipeline-run-complete.png)



## Screen Recording


Link to screencast: 

# Suggestions on improving the project

The dataset shows a class imbalance during the run so that can be addressed by balanced data collection, since a model performs only as well as its data. Metrics other than accuracy can also be used to improve the model performance.
