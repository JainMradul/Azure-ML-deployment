
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

# Architectural Diagram
![architecture](https://github.com/JainMradul/Azure-ML-deployment/blob/main/screenshots/architecture.PNG)

- [x] DataSet is loaded in AutoML run via UI and through python SDK (jupyter notebook)
- [x] Model is trained and deployed manually using UI 
- [x] Above process is automated via Pipeline and best model is deployed through ACI endpoint
- [x] API documentation is accessed via swagger and application insights are enabled to keep track of logs
- [x] End user can interact via ACI endpoint or pipeline endpoint

# Key Steps 

# 1. Upload and Register Dataset 
The first step is to upload the [Bank Marketing dataset](https://automlsamplenotebookdata.blob.core.windows.net/automl-sample-notebook-data/bankmarketing_train.csv) and register it on the ML Studio

![dataset](https://github.com/JainMradul/Azure-ML-deployment/blob/main/screenshots/dataset.PNG)


# 2. AutoML run on compute cluster

In the next step, the automated ML run is configured by setting up a compute cluster and selecting the uploaded dataset for the experiment. 
AutoML run multiple iterations to identify the best model

![AutoML](https://github.com/JainMradul/Azure-ML-deployment/blob/main/screenshots/automlcomplete.PNG)

# 3. Best performing model

The best model turned out to be Voting Ensemble, with an accuracy of 91.8%

![best model](https://github.com/JainMradul/Azure-ML-deployment/blob/main/screenshots/bestmodel.PNG)

# 4. Deploy the best model

Now we will deploy the best model as an Azure Container Instance with authentication enabled.

![model deploy](https://github.com/JainMradul/Azure-ML-deployment/blob/main/screenshots/modeldeploy.PNG)


# 5. Enable logging and view logs

Application insights are enabled for deployed model to capture logs.
The logs can be viewed by running the logs.py script.

![Logs](https://github.com/JainMradul/Azure-ML-deployment/blob/main/screenshots/logs.png)


# 6. Swagger documentation of API and endpoints

Swagger documentation is use to serve deployed model. 
1. Model endpoints can be consumed via HTTP requests 
2. We can also use endpoint.py script to consume endpoint by sending request through JSON payload

![swagger1](https://github.com/JainMradul/Azure-ML-deployment/blob/main/screenshots/swagger1.PNG)
![swagger2](https://github.com/JainMradul/Azure-ML-deployment/blob/main/screenshots/swagger2.PNG)
![swagger3](https://github.com/JainMradul/Azure-ML-deployment/blob/main/screenshots/swagger3.PNG)
![swagger4](https://github.com/JainMradul/Azure-ML-deployment/blob/main/screenshots/swager4.PNG)


# 7. Pipeline run via Jupyter notebook

Second part of this project is to operationalize ML run via pipeline using Python SDK module. 
1. Jupyter notebook runs with the same compute cluster and registered dataset as in the AutoML run. 
2. Published pipelines details can be seen in pipeline tab 

![runwidget](https://github.com/JainMradul/Azure-ML-deployment/blob/main/screenshots/runwidget.PNG)

# 8. Publish pipeline and deploy as endpoint

Once the pipeline run completes, the pipeline can be published with an endpoint to enable downstream tasks automation. 
The published pipeline status and endpoint can be viewed on the ML Studio

![pipelineendpoint](https://github.com/JainMradul/Azure-ML-deployment/blob/main/screenshots/pipelineendpoint.PNG)
![pipelineendpoint2](https://github.com/JainMradul/Azure-ML-deployment/blob/main/screenshots/pipelineendpoint2.PNG)


# Screen Recording

Youtube link : https://youtu.be/lxiZu64K8UY

# Future work

- [ ] AutoML (autoguard rails) reveals the class imbalance in data and hence this could be treated using different algo/techniques to improve data quality
- [ ] Depending upon the problem in hand, identify the best evaluation metric that maximize the model performance (Accuracy metric not necessary serves the purpose hence try different metrics as well to evaluate model)
- [ ] AutoML can help you quickly identify the best performing model, hence that model could be coded and used as the base model and further improvement could be done gradually on the top of this model.


