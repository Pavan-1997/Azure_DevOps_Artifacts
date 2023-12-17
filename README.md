# Azure DevOps Artifacts

In this project I have set up an Azure pipeline where the source code is fetched from Azure Repos and have multiple tasks.

The pipeline is executed on an agent where I have made use of an EC2 Ubuntu machine to run the jobs.

Service connections are created when required during the project.

In the end, the build output of Maven is pushed to Azure Artifacts

---

# Implementation

`We will be getting 2GB of artifact storage when using free subscriptions`

Feed - Storage Repo


1. Create a new feed

  Select Members of <Organization-name> and click on create
  
  Now you should see two feeds 


2. Click on Connect to feed

  Select Maven -> In options add -DskipTests=true
  
  Copy the first section of repo
  
  Now go to POM.XML file in the repo and add the copied repo after dependencies tag in it with both  <repositories> and <distributionManagement> tags 


3. Create a new pipeline

  Now in Agent job 1 select the Agent pool created earlier
  
  Select branch - main -> Select Maven and in Goal - deploy
  
  Add another task for authentication of Maven i.e Maven Authenticate
  
  In Maven Authenticate -> Select the Feeds 
  
  Now for credentials click on Manage -> Click on New service connection -> Click on Maven -> Select Authentication method - Authentication token ->  Give Repoditory URL from Step 2 3rd line -> Give Repoditory Id from the same - azure-artifacts -> Create a PAT and give -> Finally give name to the service connection and click on Save and queue

If getting below the error 

[ERROR] Failed to execute goal org.apache.maven.plugins:maven-deploy-plugin:2.8.2:deploy (default-deploy) on project shopping-cart: Failed to deploy artifacts: Could not transfer artifact com.reljicd:shopping-cart:jar:0.0.1-20230623.103638-1 from/to azure-artifacts (https://pkgs.dev.azure.com/sqlonlinux/WebApplication/_packaging/azure-artifacts/maven/v1): Authorization failed for https://pkgs.dev.azure.com/sqlonlinux/WebApplication/_packaging/azure-artifacts/maven/v1/com/reljicd/shopping-cart/0.0.1-SNAPSHOT/shopping-cart-0.0.1-20230623.103638-1.jar 403 Forbidden - User '7179663e-9411-42be-9111-63abeb245e03' lacks permission to complete this action. You need to have 'AddPackage'. (DevOps Activity ID: 9884FB55-E9DE-4246-848E-69797B667C8D) -> [Help 1]

Goto to Artifatcs -> Feed Settings -> 	Add Permission - WebApplication Build Service (sqlonlinux) with Contributor access and save it 
Below is an image of a job with its tasks where an artifact is generated:

![azure-artifacts](https://github.com/Pavan-1997/Azure_DevOps_Artifacts/assets/32020205/42f54d5d-eeed-4e3e-90dc-df48e0d421a4)

Below is an image of the artifact pushed:

![artifact](https://github.com/Pavan-1997/Azure_DevOps_Artifacts/assets/32020205/267e5d13-aeb4-4ba9-b703-2b1af68363a5)
