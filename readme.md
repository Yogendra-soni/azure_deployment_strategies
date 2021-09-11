# Issue:

While deploying Azure datafatory pipelins with the help of azure provided <br>
release pipeline, deployement task automatically diables all the triggers <br>
in the ADF. Because of which many runs of scheduled as well as event based <br>
in the ADF. Because of which many runs of scheduled as well as event based <br>
triggered  pipelines misses their runs and that causes a problem for all <br>
the process.<br><br>

# Solution:<br>
Azure data factory deployments can be done thorugh Azure CLIU commands.<br>
Below is teh link - <br>
https://github.com/MicrosoftDocs/azure-docs/blob/master/articles/data-factory/quickstart-create-data-factory-azure-cli.md<br><br>
So instead of deploying adf objects using Azure provided task, we create <br>
our own custom deployement solution, which uses josn files of adf objects <br>
to deploy them in another env with the help of azure devops CI pipelines.<br><br>

# Prerequisite:<br>
1. Azure DevOps subscription<br>
2. Azure datafactory connected to azure repository<br>
<br>

# How to use ci_deploye_azure_pipeline:-<br>
<br>
This is an yaml based pipeline.<br>
This pipline get triggered automatically when there is a chnages in ADF pipeline <br>
json file.<br>
It identifies json file chnaged during the commit and deployes them in higher env<br>
with the help of Azure CLI task and executin below command - <br>
<br>
az datafactory pipeline create-run --resource-group ADFQuickStartRG \<br>
    --name Adfv2QuickStartPipeline --factory-name ADFTutorialFactory<br>

#### Before using this ymal file below changes needs to be done maked with the help of 'marks'<br>
**Mark#1** Update with your source branch <br>
<t>it can be your cpollabration branch or your featrure branch.<br>
**Mark#2** Path of json file of ADF objects<br>
	<t>	Usally its azure_data_factory/pipeline<br>
**Mark#3** Accordingly update ADF objects path here as well<br>
**Mark#4** Devops connection for target Subscription<br>
**Mark#5** NAme of your destination ADF <br>
<br>
after modifying the yaml file connecgt it with a classic yaml based azure devops CI pipeline.<br>

<br><br>
# Disclaimer -<br>
This is an open source project, comments or contribution are most welcomed. <br>
I don't hold any responsibility for any damage/instability caused in your <br>
system while using this deployment strategy.<br>
