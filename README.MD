# Elephant Mini Project

This project is a demonstration of CI/CD concepts by creating a static web hosting S3 bucket with CloudFormation and using CodeBuild to have a form of automated testing. This was all orchestrated by CodePipeline

### Services
The following AWS services are used to create the CI/CD pipeline
- CodePipeline
- CodeBuild
- CloudFormation

### Prerequisites
- Create a S3 bucket and enable static website hosting
- Create a file named ```index.html``` and upload it to the desired GitHub repository branch

### Steps

1. The ```website.json``` file in this repository was used to create the S3 bucket in CloudFormation. The AccessControl property was set to the canned ACL PublicRead which is required for website hosting. All other CloudFormation settings were set to default
2. The CodePipeline was configured with three phases:
   - Source Phase: The action provider for this pipeline was this GitHub repository. Github webhooks was used for the change detection method to ensure the pipeline would run anytime there were changes to the repository.
   - Testing Phase: Codebuild was used to test whether the html contained the words "Automation for the People!". This was done by using ```cat index.html | grep "Automation for the People!"``` (Note: The generated buildspec.yml is available in the master branch of this repository)
   - Deploy Phase: The index.html file in this github repository was deployed to the S3 bucket initially created by the CloudFormation stack
  
![image](https://user-images.githubusercontent.com/57568144/76044909-b00a8a00-5f29-11ea-92d6-04e09b1eee89.png)
   
### Cleanup
- Ensure you delete the CloudFormation Stack and the S3 bucket to avoid incurring any additional charges. 
