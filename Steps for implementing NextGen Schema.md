- Azure blob container creation 
- Key vault entry for blob connection string
- Schemas added to Azure Devops repository
- Azure Devops build pipeline creation for schemas
- Azure Devops release pipeline creation for schemas
    - Task for a beta release

        The task will need to add the file to the blob storage with a pre release version
    - Task for Prod release

- Repositories for nuget packages representing schemas
- Creation of nuget packages for each external schema
- Local repository inside Meijer's nuget package location
- Azure Devops build pipeline creation for nuget packages
- Azure Devops release pipeline creation for nuget packages
    - Deployed to Meijer nuget package repository
- Azure Web App created for both non-prod and production
    - int, cert, qa slots created.
- Azure Devops Repository for Schema Web application
- Azure Devops build pipeline creation for web app
- Azure Devops release pipeline creation for web app
