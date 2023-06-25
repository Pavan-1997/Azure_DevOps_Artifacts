# Azure DevOps Artifacts

In this project I have set up an Azure pipeline where the source code is fetched from Azure Repos and have multiple tasks.

The pipeline is executed on an agent where I have made use of an EC2 Ubuntu machine to run the jobs.

Service connections are created when required during the project.

In the end, the build output of Maven is pushed to Azure Artifacts

All the commands are documented in the CMD.txt file

Below is an image of a job with its tasks where an artifact is generated:

![azure-artifacts](https://github.com/Pavan-1997/Azure_DevOps_Artifacts/assets/32020205/42f54d5d-eeed-4e3e-90dc-df48e0d421a4)

Below is an image of the artifact pushed:

![artifact](https://github.com/Pavan-1997/Azure_DevOps_Artifacts/assets/32020205/267e5d13-aeb4-4ba9-b703-2b1af68363a5)
