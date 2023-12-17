![BLOCK](https://github.com/Pavan-1997/Azure_DevOps_Artifacts/assets/32020205/4692ed4b-fc5c-4260-a22f-b2875c53d5ad)


1. Go to the Azure DevOps portal organization 


2. Click on + New project -> Project name - Day7_Artifacts -> Click on Create


3. Go to the Repos on the left -> Click on Import a repository -> Clone URL - `https://github.com/Pavan-1997/Azure_DevOps_Artifacts.git` -> Click on Import


4. Now go to the Azure portal -> Search and open the App Services -> Click on + Create -> Select + Web App 

    Resource Group - Create new -> day7_rg -> Click on OK
    
    Name - spavanraj97
    
    Runtime stack - Node 18 LTS
    
    Region - Canada Central
    
    Pricing Plan - Free F1
    
    Click on Review + Create

![WebApp](https://github.com/Pavan-1997/Azure_DevOps_Artifacts/assets/32020205/eded992c-9519-4cb3-aea4-30beeb8d9fb2)


5. Now click on  Go to resource -> Click on Configuration on the left -> Click on + New application setting

    Name - `WEBSITE_DYNAMIC_CACHE`
    
    Value - `0`
    
    Click on Ok
    
    Name - `WEBSITE_ENABLE_SYNC_UPDATE_SITE`
    
    Value - `never`
    
    Click on Ok
    
    Click on Save -> Click on Continue
    
    Now go back to the Overview on the left -> Click on the Default domain which should give you a default page of the NodeJS

![DEFAULT](https://github.com/Pavan-1997/Azure_DevOps_Artifacts/assets/32020205/5f527de2-9d81-4008-afd7-08f774e944c1)


6. Now go back to the Azure DevOps portal in the project created -> Click on Pipelines on the left -> Click on Create pipeline -> Select Azure Repos Git -> Select the Repo -> Click on Starter pipeline

    Copy the pipeline code in the Repo with name PROJECT2_ARTIFACTS.yml 
    
    To create a feed -> Click on Artifacts on the left -> Click on + Create Feed -> Name - day7-nike-feed -> Click on Create -> Click on the Feed Settings -> Click on the Permissions tab
    
    Delete the Day7_Artifacts Build Service with contributor role 
    
    Click on Add users or groups -> User/Group - Project Collection Build Service -> Role - Contributor -> Click on Save
    
    Click on Add users or groups -> User/Group - Day7_Artifacts Build Service -> Role - Contributor -> Click on Save
   
![feed-permission](https://github.com/Pavan-1997/Azure_DevOps_Artifacts/assets/32020205/107979f2-3806-4170-a799-9aa62f8566fa)
    
   Click on Save and Run which should generate an artifact in the Azure Artifacts

![Build](https://github.com/Pavan-1997/Azure_DevOps_Artifacts/assets/32020205/6aa1ee11-a935-4ef3-a937-48b5c1131306)

![package](https://github.com/Pavan-1997/Azure_DevOps_Artifacts/assets/32020205/ea6e3804-c071-4ea3-850c-fb65175fcd74)


7. Click on Pipelines on the left -> Click on Releases -> Click on New pipeline -> Select Azure App Service Deployment -> Stage name - Deployment 

    Click on Add an artifact -> Select Source type - Azure Artifacts -> Feed - day7-nike-feed -> Package type - npm -> View - Prerelease -> Package - nike-2-0 -> Default version - latest -> Click on Add
    
    Click on the Continuous deployment trigger -> Enable it 
    
    Now go to the Deployment -> Click on the job,task under it -> Select the Azure subscription -> Click on Authorize which should create a service connection -> App type - Web App on Linux ->  Select the App Service name that we have created during the start 
    
    Now click on Run on Agent -> Agent Pool - Select the Self runner
    
    Now click on Deploy Azure App Service -> Package or folder - $(System.DefaultWorkingDirectory)/_nike-2-0 -> Runtime Stack - 1.0 (STATICSITE|1.0) -> Post Deployment Action - (Deployment script type - Inline Script, Inline Script - `cp -rf /home/site/wwwroot/package/* /home/site/wwwroot/`)
    
    Now click on Save

![Release](https://github.com/Pavan-1997/Azure_DevOps_Artifacts/assets/32020205/1a42248d-e1ab-45dc-94fa-6af2275c2c49)

![Deploy](https://github.com/Pavan-1997/Azure_DevOps_Artifacts/assets/32020205/265ddf4a-5916-43ca-8ce0-7c98a1c3a6d7)

![NIKE](https://github.com/Pavan-1997/Azure_DevOps_Artifacts/assets/32020205/254d61ab-5280-4ce1-b463-a941c03eb932)


8. Go to the Azure Artifacts -> Select the Package -> Cick on Promote on the top -> Select a view - day7-nike-feed@Prerelease -> Click on Promote

![Release-1](https://github.com/Pavan-1997/Azure_DevOps_Artifacts/assets/32020205/ff6ccc27-643a-48d9-ad80-bc0ae9be60ef)


9. Now go back to the Azure Devops portal in the project created -> Go to the App Service created -> Click on the Advance Tools on the left -> Click on Go -> Click on SSH ->

![kudo](https://github.com/Pavan-1997/Azure_DevOps_Artifacts/assets/32020205/2e06b328-f2eb-4c48-9082-92f0b69cd346)

```
    cd site/wwwroot/
```
``` 
    ls -lrt
```

![kudo-ssh](https://github.com/Pavan-1997/Azure_DevOps_Artifacts/assets/32020205/ce4d6431-0061-4489-b212-ddf8798896c9)
