Pipeline process consists of different parts and we will demonstrate each part as follow:
=========================================================================================

1- Orbs: Orbs part used to illustrate and configure third part tools as services and packages used to build and deploy my software .As follow Orbs used in the application>>

        1-circleci/node@4.1.0 : install Node.js and its package managers (npm, yarn) as my runtime environment.
        2-circleci/aws-cli@1.3.1 : Install and configure the AWS command-line interface with CircleCI.
        3-circleci/aws-elastic-beanstalk@2.0.1:  Deploy and scale the application and its services via AWS Elastic Beanstalk with CircleCI. 


2- Jobs: jobs part is Responsible for running a series of steps that perform commands.Here we have only one step that called (build) and it consists of the following :

        1- docker : specify docker as an executer of build job and its image.
        2- steps :

            2.1. node/install : install Node.js version "16.13.2".
            2.2. checkout     : check the source code uploaded to Githup.
            2.3. aws-cli/setup: setup AWS command-line interface.
            2.4. eb/setup     : setup AWS Elastic Beanstalk with CircleCI.
            2.5. run          :
                    name: Front-End Install
                    command: |
                    npm run udagram-frontend:install
                
                >>run script that is responible for installing  packages in dependecies part in package.json of udagram-frontend app.

            2.6. run:
                    name: Back-End Install
                    command: |
                    npm run udagram-api:install

                 >>run script that is responible for installing  packages in dependecies part in package.json of udagram-api app.

            2.7. run:
                    name: Front-End Build
                    command: |
                    npm run udagram-frontend:build

                >>run script that is responible for building  udagram-frontend static files to www folder.

            2.8. run:
                    name: Back-End Build
                    command: |
                    npm run udagram-api:build

                >>run script that is responible for building  udagram-api to  www folder and zip files to Archive.zip .

            2.9. run:
                    name: Deploy App API
                    command: |
                    npm run udagram-api:deploy 

                 >>run script in udagram-api/bin/deploy.sh that is responible for deploy Archive.zip to Elastic Beanstalk environment that is previously created  .

            2.10. run:
                    name: Deploy App Front
                    command: |
                    npm run udagram-frontend:deploy

                >>run script in udagram-frontend/bin/deploy.sh that is responible for deploy static files in www folder to AWS S3 bucket that is previously created  .

                



  
    












    
    
   