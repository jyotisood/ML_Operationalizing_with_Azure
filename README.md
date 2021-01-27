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
 
<img src = https://github.com/jyotisood/ML_Operationalizing_with_Azure/blob/main/Images/best_Model.png>

** Visualize  the metrics of the best model **
 ![](https://github.com/jyotisood/ML_Operationalizing_with_Azure/blob/main/Images/best-model%20metrics_1.png)
 
 ![](https://github.com/jyotisood/ML_Operationalizing_with_Azure/blob/main/Images/best-model%20metrics_2.png)
 
### Deploy the best model
We need to deploy the best model in order to interact with  it. 
In this step, the model (voting ensemble) was deployed using Azure Container Instance (ACI), with authentication enabled so only authorized users have the key to interact with the model.

![](https://github.com/jyotisood/ML_Operationalizing_with_Azure/blob/main/Images/deploy_settings.png)

After the best model is successfully deployed, we can access the model endpoints in the Endpoints section.

![](https://github.com/jyotisood/ML_Operationalizing_with_Azure/blob/main/Images/Endpoints_best_model_deployed.png)
 
### Enable Application and Logging Insights
 
At the time of deployment Enabling Application Insights and Logs can easily be done but here we do it later by using git bash.

We modify the script of logs.py and then by running the logs.py script, we enable Application Insights.

![](https://github.com/jyotisood/ML_Operationalizing_with_Azure/blob/main/Images/logs_py.png)

See the Application Insights enabled in the Endpoints and when you click on the Application insights URL, you can get further details.

![](https://github.com/jyotisood/ML_Operationalizing_with_Azure/blob/main/Images/App_Insights_3.png)

![](https://github.com/jyotisood/ML_Operationalizing_with_Azure/blob/main/Images/App_insights_2.png)


### Swagger 

To consume AutoML model using Swagger, we first need to download the swagger.json file provided to us.

Then we run the swagger.sh and serve.py files separately in order to interact with the swagger instance running locally with the documentation for the HTTP API of the model.

![](https://github.com/jyotisood/ML_Operationalizing_with_Azure/blob/main/Images/swagger_bash.png)

![](https://github.com/jyotisood/ML_Operationalizing_with_Azure/blob/main/Images/serve.png)

On the local host, Swagger documentation for the HTTP API of our model is seen.

![](https://github.com/jyotisood/ML_Operationalizing_with_Azure/blob/main/Images/swagger1.png)

After running the script, we can see our best model's documentation instead of the default Swagger page. And this is content of API used for interacting with our deployed model.

![](https://github.com/jyotisood/ML_Operationalizing_with_Azure/blob/main/Images/swagger2.png)

![](https://github.com/jyotisood/ML_Operationalizing_with_Azure/blob/main/Images/swagger3.png)


### Consume model endpoints

Finally, now we can interact with the model and feed some test data to it. Scoring_uri and the primary key are the best way to interact and are updated in the given endpoint.py script.
After editing scoring_uri and primary key , we run the endpoint.py script and a data.json file is generated and see the response in git bash.

![](https://github.com/jyotisood/ML_Operationalizing_with_Azure/blob/main/Images/endpoint.py_and_data.json_file.png)



### Create and Publish an ML Pipeline

In this step, python SDK is used to create and publish the pipeline. 
After uploading and editing the given jupyter notebook with same cluster name, model name, all cells are run through to create a pipeline.

Pipeline running Overview

![](https://github.com/jyotisood/ML_Operationalizing_with_Azure/blob/main/Images/pipeline_running_overview.png)

![](https://github.com/jyotisood/ML_Operationalizing_with_Azure/blob/main/Images/pipeline_running_view_in_studio.png)


Pipeline has been successfully published : view in SDK

![](https://github.com/jyotisood/ML_Operationalizing_with_Azure/blob/main/Images/Endpoint_Status_%20in_SDK.png)


Pipeline has been successfully created : view in Azure ML Studio

![](https://github.com/jyotisood/ML_Operationalizing_with_Azure/blob/main/Images/Pipelines-COMPLETED.png)


Pipeline Rest Endpoints are created

![](https://github.com/jyotisood/ML_Operationalizing_with_Azure/blob/main/Images/pipelines_completed.png)


##### Pipeline Endpoints 
The piepeline endpoints are seen as active here

![](https://github.com/jyotisood/ML_Operationalizing_with_Azure/blob/main/Images/Pipelines-ENDPOINT%20ACTIVE.png)


#### Status of Run Widget
The steps and running status can be seen from sdk itself using run widgets.

![](https://github.com/jyotisood/ML_Operationalizing_with_Azure/blob/main/Images/Run_widgets_1.png)

![](https://github.com/jyotisood/ML_Operationalizing_with_Azure/blob/main/Images/Run_widgets_2.png)


### Future Suggestions
The current data was imbalanced classes, In future this problem can be looked into.
Increasing the number of cross validations might help in getting better accuracy.

![](https://github.com/jyotisood/ML_Operationalizing_with_Azure/blob/main/Images/problems.png)

#### Link to the ScreenCast

