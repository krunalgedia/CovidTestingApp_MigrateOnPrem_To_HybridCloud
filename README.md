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
  
  - AWS S3 bucket with ACL set to private
    [Image](https://github.com/krunalgedia/CovidTestingApp_MigrateOnPrem_To_HybridCloud/blob/main/images_app/mission1/S3%20bucket.png)
    
  - Cloud SQL database instance
    [Image](https://github.com/krunalgedia/CovidTestingApp_MigrateOnPrem_To_HybridCloud/blob/main/images_app/mission1/sql%20database%20instance.png)

  - Cloud GKE cluster on autopilot mode
    [Image](https://github.com/krunalgedia/CovidTestingApp_MigrateOnPrem_To_HybridCloud/blob/main/images_app/mission1/gke%20instance.png)
    
| ![Image](https://github.com/krunalgedia/CovidTestingApp_MigrateOnPrem_To_HybridCloud/blob/main/images_app/mission1/S3%20bucket.png) | AWS S3 bucket with ACL set to private |
|-----------------------------|------------------|
| ![Image](https://github.com/krunalgedia/CovidTestingApp_MigrateOnPrem_To_HybridCloud/blob/main/images_app/mission1/sql%20database%20instance.png) | Cloud SQL database instance   |

| ![Image](https://github.com/krunalgedia/CovidTestingApp_MigrateOnPrem_To_HybridCloud/blob/main/images_app/mission1/gke%20instance.png) | Cloud GKE cluster on autopilot mode.   |


 
*    <img align="left" width="200" src="https://github.com/krunalgedia/CovidTestingApp_MigrateOnPrem_To_HybridCloud/blob/main/images_app/mission1/S3%20bucket.png" /> AWS S3 bucket with ACL set to private.
*   <img align="left" width="200" src="https://github.com/krunalgedia/CovidTestingApp_MigrateOnPrem_To_HybridCloud/blob/main/images_app/mission1/sql%20database%20instance.png" /> Cloud SQL database instance.
*   <img align="left" width="200" src="https://github.com/krunalgedia/CovidTestingApp_MigrateOnPrem_To_HybridCloud/blob/main/images_app/mission1/gke%20instance.png" /> Cloud GKE cluster on autopilot mode.
  The final Terraform state should look like <img align="right" width="200" src="https://github.com/krunalgedia/CovidTestingApp_MigrateOnPrem_To_HybridCloud/blob/main/images_app/mission1/CLI%20terraform%20state.png" />


```bash
# Example installation command
pip install -r requirements.txt

# Run Web Application
streamlit run app.py
```

## Data

The data used consists of SBB train tickets for single and extension tickets. The training set consists of just 4 SBB train tickets. All tickets are in PDF form.

## Workflow
<img align="left" width="200" src="https://www.rd.com/wp-content/uploads/2018/02/25_Hilarious-Photos-that-Will-Get-You-Through-the-Week_280228817_Doty911.jpg" />

# Headline 

Some text


0. Prepare training data by annotation using the UBIAI tool [1]. This includes drawing bounding boxes and labeling in the BIOES tagging form [2].
1. Importing data
2. Observing data
3. Loading data in appropriate form.
4. Fine-tuning LayoutML model.
5. Preparing test set processing, including OCR of prediction documents using Pytesseract and getting the bounding box for all text in the test sample.
6. Running predictions on the bounding boxes of Pytesseract.
7. Update the database with relevant NER extracted from the model prediction on the annotated test sample.

* notebooks/SBB_TrainTicketParser.ipynb contains the end-to-end code for Document parsing with database integration.
* app.py contains the streamlit app code.

## Results

We fine-tuned using Facebook/Meta's LayoutLM (which utilizes BERT as the backbone and adds two new input embeddings: 2-D position embedding and image embedding) [3]. The model was imported from the Hugging Face library [4] with end-to-end code implemented in PyTorch. We leveraged the tokenizer provided by the library itself. For the test case, we perform the OCR using Pytesseract.

With just 4 SBB train tickets we can achieve an average F1 score of 0.81.   
