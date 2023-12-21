# CovidTestingApp_MigrateOnPrem_To_HybridCloud

Business Problem:

The luxury hotel chain currently faces challenges with its existing COVID testing web application, which is hosted on traditional on-premise servers. The limitations of this infrastructure impact scalability, resource utilization, and the ability to adapt to varying demands efficiently.

Project Objective:

Migrate a Covid Testing real web application of a luxury hotel chain to a Scalable Hybrid Cloud environment.

## Table of Contents

- [Project Overview](#project-overview)
- [Installation](#installation)
- [Usage](#usage)
- [Data](#data)
- [Workflow](#workflow)
- [Results](#results)
- [More ideas](#More-ideas)
- [Dependencies](#dependencies)
- [License](#license)
- [Contact](#contact)
- [References](#references)

## Project Overview

The goal of this project is to migrate a real-time web application and its database to a Hybrid cloud environment of GCP and AWS. To achieve this, we
* Use the IaaC tool Terraform to set up Google cloud and AWS infrastructure.
* Use the PaaS tool Docker to deploy the web application to Google Cloud in the container. 
* Use the container orchestration tool Kubernetes to run manage and scale containers built in the previous step in Google Cloud.
* Use RDBS Cloud SQL in Google Cloud as a DB for the web app.
* Use the S3 AWS bucket to store, migrate, and sync the database for the web app.

## Workflow Gist

- Create a user on AWS with IAM Rules that allow full access to the AWS S3 bucket and keep the access Key for this user.
- Set up the environment on GCP and AWS using [set AWS credentials] (https://github.com/krunalgedia/CovidTestingApp_MigrateOnPrem_To_HybridCloud/blob/main/mission1/en/aws_set_credentials.sh) and [set GCP credentials] (https://github.com/krunalgedia/CovidTestingApp_MigrateOnPrem_To_HybridCloud/blob/main/mission1/en/aws_set_credentials.sh).
- Using Terraform, deploy
    
| ![Image](https://github.com/krunalgedia/CovidTestingApp_MigrateOnPrem_To_HybridCloud/blob/main/images_app/mission1/S3%20bucket.png) | AWS S3 bucket with ACL set to private |
|-----------------------------|------------------|
| ![Image](https://github.com/krunalgedia/CovidTestingApp_MigrateOnPrem_To_HybridCloud/blob/main/images_app/mission1/sql%20database%20instance.png) | Cloud SQL database instance   |
| ![Image](https://github.com/krunalgedia/CovidTestingApp_MigrateOnPrem_To_HybridCloud/blob/main/images_app/mission1/gke%20instance.png) | Cloud GKE cluster on autopilot mode.   |

  - The final terraform status should be
    ![Image](https://github.com/krunalgedia/CovidTestingApp_MigrateOnPrem_To_HybridCloud/blob/main/images_app/mission1/CLI%20terraform%20state.png)

* Configure the Cloud SQL instance and assign private IP within the default VPC.
  
* Build docker image of the web application can push to Google Container Registry (GCR) for deployment.

* Ensure that the deployment yaml file has correct keys for S3 and SQL set up in the env of the container.

* Deploy the docker container from GCR to Google Kubernetes Engine (GKE). Following are some specs of the running instance:
| ![Image](https://github.com/krunalgedia/CovidTestingApp_MigrateOnPrem_To_HybridCloud/blob/main/images_app/mission2/gke%20workload%20or%20deployment.png) | GKE Workload |
|-----------------------------|------------------|
| ![Image](https://github.com/krunalgedia/CovidTestingApp_MigrateOnPrem_To_HybridCloud/blob/main/images_app/mission2/gke%20service%20and%20ingress.png) | GKE Service and Ingress  |

* Check the website using GKE Ingress endpoint IP
![Image](https://github.com/krunalgedia/CovidTestingApp_MigrateOnPrem_To_HybridCloud/blob/main/images_app/mission2/website%20on%20gke.png)

* Create a user on Cloud SQL Instance, connect to database using the user credential and migrate database to the cloud app.
* Make a folder on AWS with testing reports corresponding to the database, and sync the S3 folder to migarte the files to the cloud app.
![Image](https://github.com/krunalgedia/CovidTestingApp_MigrateOnPrem_To_HybridCloud/blob/main/images_app/mission3/updated%20database%20with%20data%20and%20pdf%20migrated%20on%20website.png)


