# ML_Operationalizing_with_Azure


### Overview
##### This is the second project for the Udacity Microsoft Azure ML Nanodegree. We use Bank Marketing dataset to create an AutoML model which is later deployed using Azure Container Instance and can be consumed by REST endpoints. A pipeline using SDK is also created, published and consumed.


### Architectural Diagram
![](https://github.com/jyotisood/ML_Operationalizing_with_Azure/blob/main/Images/Architecture.png?raw=True)

### Steps
###Authentication: 

As I worked in the Udacity Azure Account, so did not need to authenticate and skipped this step.


### Automated ML Experiment
Uploaded this dataset into Azure ML Studio using the url provided.

The compute cluster was configured with following settings:Standard_DS12_v2 for the Virtual Machine and 1 as the minimum number of nodes
create an AutoML experiment to run using the Bank Marketing Dataset which was already loaded in the Azure Workspace. Set ‘'y' as the target column.
Reduced the Exit Criterion to 1 hour and Concurrency to 5 concurrent iterations max.
Run the experiment on the cluster

The best model generated is voting ensemble model with an approximate accuracy of 91.9%
 
![](https://github.com/jyotisood/ML_Operationalizing_with_Azure/blob/main/images/best_Model.png?raw=True)


** Visualize  the metrics of the best model **
 ![](images/best_model_metrics_1.png)
 ![](images/best_model_metrics_2.png)
 
### Deploy the best model
We need to deploy the best model in order to interact with  it. 
In this step, the model (voting ensemble) was deployed using Azure Container Instance (ACI), with authentication enabled.

![](images/deploy_settings.png)


After the model is successfully deployed, we can access the model endpoints in the Endpoints section.

 
### Enable Application and Logging Insights
 
At the time of deployment Enabling Application Insights and Logs can easily be done. But for this project we use Azure Python SDK to achieve this. We enable key based authentication so that only authorized users having the key can interact with the model
 ![](images/deploy_settings.png)

We modify the script of logs.py and then by running the logs.py script, we enable Application Insights.
![](images/logs_py.png)

![](images/App_insights_2.png)
![](images/App_insights_3.png)


### Swagger 

To consume AutoML model using Swagger, we first need to download the swagger.json file provided to us.

Then we run the swagger.sh and serve.py files to be able to interact with the swagger instance running with the documentation for the HTTP API of the model.


![](images/serve.png)
![](images/swagger_bash.png)


![](images/swagger1.png)
And this is the input for the /score POST method that returns our deployed model's preditions.
![](images/swagger2.png)
These are the APIs, diplaying the methods used to interact with the model.
![](images/swagger3.png)


### Consume model endpoints

Finally, it's time to interact with the model and feed some test data to it. Scoring_uri and the primary key are the best way to do this and are used in endpoint.py script and run.
![](images/endpoint.png)
After editing scoring_uri and primary key , we run the endpoint.py script to get inference from the deployed model.


### Create and Publish an ML Pipeline

In this step, python SDK is used to create and publish the pipeline.
After uploading and editing the notebook to have the same keys, URI, all cells are run through to create a pipeline.
pipeline scheduled run details

![](images/pipeline_running_1.png)
![](images/pipeline_running_overview.png)
![](images/pipeline_running_view_in_studio.png)



pipeline has been successfully created : view in SDK
![](images/pipelines_completed.png)
![](images/pipelines_completed.png)


pipeline has been successfully created : view in Azure ML Studio
![](images/endpoint.png)
pipeline REST endpoint in active state
![](images/Pipelines-COMPLETED.png)


** Pipeline Endpoints **
The piepeline endpoints have been set to active
![](images/Pipelines-ENDPOINT ACTIVE.png)


#### Status of Run Widget
The steps and running status can be seen from sdk itself using run widgets.
![](images/Run_widgets_1.png)
![](images/Run_widgets_2.png)


### Future Suggestions
The current data was imbalanced classes, In future this problem can be looked into
Increasing the number of cross validations might help in getting better accuracy
![](images/problems.png)


