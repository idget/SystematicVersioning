# Retail Next Gen API versioning

## References:
[Semantic Versioning 2.0.0](https://semver.org/)

[Geeks for Geeks | Introduction to Semantic Versioning](https://www.geeksforgeeks.org/introduction-semantic-versioning/)

## Components used for supporting NextGen schema versioning
- Nuget packages for each schema that is used by a client

    Nuget package for each type of schema
	Will include:
    - Models
    - Helper libraries
    - Schema validation
    - Access to schema file
- Azure blob storage

    Blobs will be organized by schema. Example: transaction,Barcode Normalization
    blobs will be stored as json with a file name of the schema version. Example: v1.5.1
- NextGenSchemas MVC project 

   Used for exposing blob storage

## Semantic versioning
![Image of Semantic versioning](https://media.geeksforgeeks.org/wp-content/uploads/semver.png)

#### PATCH
A patch change would be used for bug fixes
#### MINOR
A minor change would be for new features or functionality that is back words compatible
#### MAJOR
A major change would include new required data. Any changes where the client needs to make changes would be considered a major change.
#### PRE-RELEASE
Changes that are being tested. Versions will be have an additional version as a suffix ex. v1.0.1.1 = beta release 1

## Nuget package implementation
A Nuget package for each type of schema will needed to support model/schema changes

- **Models**

    Models will include all data for the specified schema version the Nuget package is for. The schema will be used for model verification I.E. no required field annotations
- **Helper libraries**

    Parsing functions
- **Schema validation**

    Json input can be validated against the schema
- **Access to schema file through blob storage**

    The schema blob will be downloaded on startup the Nuget package will expose the schema in a public field. A method will be included for http requests.

    when serializing to model use the schema to validate no more [required]

- **Management of deployment environment**

    The Nuget package will be environment aware. when running in pre production environments the pre-release versions of the schema will be used if the specified schema version has not been fully completed aka in prod.

## Schema Deployment

A user story is required for a schema change. The story will describe the changes needed for the change along with which fields are required and their data types. Test cases should be added which include testable JSON input. During development the dev will make their changes have the schema reviewed and then QA will review and test using test cases provided in the user story.

Steps:
1. Dev completes schema changes
1. Card is moved to PR
1. Card is QA validates various JSON input against new schema
1.  publishing schema
    1. Pipeline will take a version type variable of PATCH,MINOR,MAJOR to determine the new version
    1. Pipeline will POST to NextGenSchemas to pull the latest schema from azure and return the schema sent to it with the version incremented. The endpoint will require to specify if the version will need to be a pre release.
    1. Pipeline will deploy the schema file to blob storage with the file name of the semantic version.
    1. During prod deployment the same steps will be taken but the file version will be without the pre-release version

## Nuget package updates
A Nuget package update can be required for two scenarios.

1. Update to the functionality of the Nuget package.

    When the functionality of the Nuget package is updated the package version would be incremented while following the same rules of semantic versioning.

1. Update to the supported schema.

    **Before the Nuget package can be updated to support a new schema, the new schema must be published to Azure.**

    Changes to the models will be completed
    The schema version supported needs to be updated. (Do not include pre-release versioning. The Nuget package will determine which will be used based on the environment it is running in)
