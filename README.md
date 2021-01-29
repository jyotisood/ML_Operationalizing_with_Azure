# ML_Operationalizing_with_Azure


# Table of contents
- Architectural Diagram
- Automated ML Experiment
- Deploy the best model
- Enable Application and Logging Insights
- Interact with model using Swagger
- Consume model endpoints
- Create and Publish an ML Pipeline
- Future Suggestions
- Link to the ScreenCast

## Overview ## 
This is the second project for the Udacity Microsoft Azure ML Nanodegree. We use Bank Marketing dataset to create an AutoML model which is later deployed using Azure Container Instance and can be consumed by REST endpoints. A pipeline using SDK is also created and published.


## Architectural Diagram
![](https://github.com/jyotisood/ML_Operationalizing_with_Azure/blob/main/Images/Architecture.png?raw=True)

# Steps

### Authentication: 

As I worked in the Udacity Azure Account, so did not need to authenticate and skipped this step.

## Automated ML Experiment
The Bank Marketing dataset was preloaded in the Azure ML lab. We use the AutoML feature of Azure ML studio to run on this dataset.

The compute cluster was configured with following settings: Standard_DS12_v2 for the Virtual Machine, 1 minimum node and 6 as maximum number of nodes. Concurrancy was set to 5 maximum concurrent iterations and reduced the exit criterion to 1 hour. 

'y' is set as the target column for this experiment. We run the experiment on the created compute cluster.

The best model generated from the automl run was voting ensemble model with an approximate accuracy of 91.9%
 
![image](https://github.com/jyotisood/ML_Operationalizing_with_Azure/blob/main/Images/best_Model.png)

The other metrics of the best model 'Voting Ensemble' can be seen here:-

 ![image](https://github.com/jyotisood/ML_Operationalizing_with_Azure/blob/main/Images/best-model%20metrics_1.png)
 
 ![image](https://github.com/jyotisood/ML_Operationalizing_with_Azure/blob/main/Images/best-model%20metrics_2.png)
 
## Deploy the best model

In this step, we choose the best model (voting ensemble) for deployment using Azure Container Instance (ACI) and enable the authentication so that only authorized users have the key to interact with the model.

![image](https://github.com/jyotisood/ML_Operationalizing_with_Azure/blob/main/Images/deploy_settings.png)

After the best model is successfully deployed, we can access the model endpoints in the Endpoints section of Azure ML studio.

![image](https://github.com/jyotisood/ML_Operationalizing_with_Azure/blob/main/Images/Endpoints_best_model_deployed.png)
 

## Enable Application and Logging Insights
 
In the next step, we update the code in logs.py and run it in git bash to enable the 'Application Insights' of the deployed model. 

![image](https://github.com/jyotisood/ML_Operationalizing_with_Azure/blob/main/Images/logs_py.png)

Here, we can see the 'Application Insights' enabled for our deployed model and when you click on the Application Insights URL, you can get further details:

![](https://github.com/jyotisood/ML_Operationalizing_with_Azure/blob/main/Images/App_Insights_3.png)

![](https://github.com/jyotisood/ML_Operationalizing_with_Azure/blob/main/Images/App_insights_2.png)


## Interact with model using Swagger

To consume AutoML model using Swagger, we first need to download the swagger.json file provided to us.

Then we run the swagger.sh and serve.py files separately which download the latest swagger container UI locally on port 9000.

![](https://github.com/jyotisood/ML_Operationalizing_with_Azure/blob/main/Images/swagger_bash.png)

![](https://github.com/jyotisood/ML_Operationalizing_with_Azure/blob/main/Images/serve.png)

On the localhost, Swagger UI has been launched successfully.

![](https://github.com/jyotisood/ML_Operationalizing_with_Azure/blob/main/Images/swagger1.png)

After running the scripts, we can see our deployed model's documentation instead of the default Swagger page. Here we see example input content of API that can be used for interacting with our deployed model.

![](https://github.com/jyotisood/ML_Operationalizing_with_Azure/blob/main/Images/swagger2.png)

![](https://github.com/jyotisood/ML_Operationalizing_with_Azure/blob/main/Images/swagger3.png)


## Consume model endpoints

Finally, now we can interact with the model and feed some test data to it. Scoring_uri and the primary key are updated in the endpoint.py script. It is then run in the git bash which generates the following response:

![](https://github.com/jyotisood/ML_Operationalizing_with_Azure/blob/main/Images/endpoint.py_and_data.json_file.png)


## Create and Publish an ML Pipeline

In this step, python SDK is used to create and publish a pipeline. 

After uploading and editing the jupyter notebook with our compute cluster name, model name, we run all the cells to create a pipeline.

- Pipeline running Overview

![](https://github.com/jyotisood/ML_Operationalizing_with_Azure/blob/main/Images/pipeline_running_overview.png)

![](https://github.com/jyotisood/ML_Operationalizing_with_Azure/blob/main/Images/pipeline_running_view_in_studio.png)


- Pipeline has been successfully published : view in SDK

![](https://github.com/jyotisood/ML_Operationalizing_with_Azure/blob/main/Images/Endpoint_Status_%20in_SDK.png)


- Pipeline has been successfully created : view in Azure ML Studio

![](https://github.com/jyotisood/ML_Operationalizing_with_Azure/blob/main/Images/Pipelines-COMPLETED.png)


- Pipeline Rest Endpoints are created

![](https://github.com/jyotisood/ML_Operationalizing_with_Azure/blob/main/Images/pipelines_completed.png)


-  Pipeline Endpoints 

The pipeline endpoints are seen as active here

![](https://github.com/jyotisood/ML_Operationalizing_with_Azure/blob/main/Images/Pipelines-ENDPOINT%20ACTIVE.png)


- Status of the Run Widgets in Python file:

The steps and running status can be observed from sdk itself using run widgets.

![](https://github.com/jyotisood/ML_Operationalizing_with_Azure/blob/main/Images/Run_widgets_1.png)

![](https://github.com/jyotisood/ML_Operationalizing_with_Azure/blob/main/Images/Run_widgets_2.png)


## Future Suggestions
* The current data had imbalanced classes. In future this problem can be looked into.
* Increasing the number of cross validations might help in getting better accuracy.
* We could try increasing the Exit Criterion from 1 hour to 3 hours(Default) to find 
  even more accurate models.

![](https://github.com/jyotisood/ML_Operationalizing_with_Azure/blob/main/Images/problems.png)

### Link to the ScreenCast

[Screencast](https://youtu.be/a7xYtnrVCiU)
