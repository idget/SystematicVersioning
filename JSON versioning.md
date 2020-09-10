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

    Blobs will be organized by schema. Example: transaction,Barcode Noramlization
    blobls will be stored as json with a file name of the schema version. Example: v1.5.1
- NextGenShemas MVC project 

   Used for exposing blob storage

## Systematic versioning
![Image of Systematic versioning](https://media.geeksforgeeks.org/wp-content/uploads/semver.png)

#### PATCH
A patch change would be used for bug fixes
#### MINOR
A minor change would be for new features or functionality that is backwords compatible
#### MAJOR
A major change would include new required data. Anychages where the client needs to make changes would be considered a majore change.

## Nuget package implemenation
Nuget package for each type of schema
	Will include:
    - Models
    - Helper libraries
    - Schema validation
    - Access to schema file

    

Retail Next gen schema will provide endpoints to schema files. This repo will have all nuget packages installed.
Controllers will be the various schemas
Get will pull a list of schema files for that service

Sample: JSON

{
   "id": "aa14300c-3483-ea11-a94c-0004ffa078c3", // MANDATORY
   
   "businessDate": "2020-04-20", // MANDATORY
   "originalBusinessDate": null,
   "payOnPhoneEligible": "false",
   "basketTotalWithTax": "21.39",
   "transactionType": "sale", // MANDATORY sale or eod, newly added field
   "transactionDateTime": "04202020 062544", // MANDATORY, need to change the date time format
   "cashierID": "550",


Projects will include nugetpackage for version supported

## Use Cases

### Nuget package update



## Coordinating a version change