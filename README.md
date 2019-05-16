# House-Pricing-Estimation

## Team Members
#### Project lead: Saurabh Annadate
#### QA lead: [Tanya Tandon](https://github.com/TanyaTandon) 


## Index
<!-- toc -->

- [Project Charter](#project-charter)
- [Project Plan](#project-plan)
- [Repo structure](#repo-structure)
- [Running the application](#running-the-application)
  * [1. Set up environment](#1-set-up-environment)
  * [2. Download the data](#2-download-the-data)
  * [3. Initialize the database](#3-initialize-the-database)
- [Exploratory Data Analysis](#exploratory-data-analysis)

## Project Charter

### Vision
Real estate agencies require accurate estimation of the price of a property to decide whether it is undervalued or not before making an investment decision. House pricing decisions are often subjective and can lead to bad investment decisions. Our vision is to develop a platform which would help estimate the price of a property based on certain property characteristics to help drive investment decisions, increase profits and reduce costs.


### Mission
The mission is to build an algorithm which would help accurately predict the price of a property based on certain characteristics like property type, no. of floors, age etc. and develop a user interface to administer the solution so that real estate agents can use it to estimate the price of a property.

### Success Criteria

**Model Criterion**: Our model is successful if the R-square evaluation metric exceeds 60%. 

**Desired Business Outcomes**: A Key Performance Indicator of the success of the app would be continual increase in it's adoption to drive business decisions by the various Real Estate agencies. This would be a good indicator of the model's accuracy performance as well. The intention is to deploy the app at a particular location, and based on the performance expand to other areas.    

## Project Plan

### Theme: Develop and deploy a platform that helps estimate the valuation of a property based on certain characteristics. 

1. __EPIC 1: Model Building and Optimization__
    * Story 1 : Data Visualization
    * Story 2 : Data Cleaning and missing value imputation
    * Story 3 : Feature Generation
    * Story 4 : Testing different model architectures and parameter tuning
    * Story 5 : Model performance tests to check the model run times
   
2. __EPIC 2: Model Deployment Pipeline Development__
    * Story 1 : Environment Setup : requirement.txt files
    * Story 2 : Set up S3 instance
    * Story 3 : Initialize RDS database
    * Story 4 : Deploy model using Flask
    * Story 5 : Development of unit tests and integrated tests
    * Story 6 : Setup usage logs
    * Story 7 : Solution reproducibility tests
    
3. __EPIC 3: User Interface Development__
    * Story 1 : Develop a basic form to input data and output results
    * Story 2 : Add styling/colors to make the interface more visually appealing  

### Backlog

Sprint Sizing Legend:

* 0 points - quick chore
* 1 point ~ 1 hour (small)
* 2 points ~ 1/2 day (medium)
* 4 points ~ 1 day (large)
* 8 points - big and needs to be broken down more when it comes to execution (okay as placeholder for future work though)
------------------
* EPIC 2 : Story 2 : Set up a S3 instance (1) : Sprint 1 (Completed)
* EPIC 2 : Story 3 : Initialize RDS database(1) : Sprint 1 (Completed)
* EPIC 1 : Story 1 : Exploratory Data Analysis (2) : Sprint 1 (Completed)
* EPIC 1 : Story 2 : Data Cleaning and missing value imputation (2) : Sprint 1 (Completed)
* EPIC 2 : Story 1 : Environment Setup : requirement.txt files (1) : Sprint 1 (Completed)
* EPIC 1 : Story 3 : Feature Generation (2) : Sprint 2
* EPIC 1 : Story 4 : Testing different model architectures and parameter tuning (8) : Sprint 2
* EPIC 1 : Story 5 : Model performance tests (2) : Sprint 2
* EPIC 2 : Story 4 : Deploy model using Flask (2) : Sprint 2
* EPIC 2 : Story 5 : Development of unit tests and integrated tests (4) : Sprint 2
* EPIC 3 : Story 1 : Develop a basic form to input data and output results (2) : Sprint 2
* EPIC 2 : Story 6 : Setup usage logs (2) : Sprint 2
* EPIC 2 : Story 7 : Solution reproducibility tests (4) : Sprint 2

### IceBox 
* EPIC 3 : Story 2 : Add styling/colors to make the interface more visually appealing

## Repo structure 

```
├── README.md                         <- You are here
│
├── app
│   ├── static/                       <- CSS, JS files that remain static 
│   ├── templates/                    <- HTML (or other code) that is templated and changes based on a set of inputs
│   ├── models.py                     <- Creates the data model for the database connected to the Flask app 
│
├── config                            <- Directory for yaml configuration files for model training, scoring, etc
│   ├── logging.conf                  <- Configuration files for python loggers
│   ├── config.py                     <- Contains all other configurations
│
├── data                              <- Folder that contains data used or generated. Only the external/ and sample/ subdirectories are tracked by git. 
│   ├── raw/                          <- Place to put raw data used for training the model 
│   ├── usage_log/                    <- Contains sqlite database usage_log.db which tracks all usage statistics
│
├── deliverables                      <- Contains all deliverables.
│
├── docs                              <- A default Sphinx project; see sphinx-doc.org for details.
│
├── figures                           <- Generated graphics and figures to be used in reporting.
│
├── models                            <- Trained model objects (TMOs), model predictions, and/or model summaries
│   ├── archive                       <- No longer current models. This directory is included in the .gitignore and is not tracked by git
│
├── notebooks
│   ├── develop                       <- Current notebooks being used in development.
│   ├── deliver                       <- Notebooks shared with others. 
│   ├── archive                       <- Develop notebooks no longer being used. 
│
├── src                               <- Source data for the project 
│   ├── archive/                      <- No longer current scripts.
│   ├── helpers/                      <- Helper scripts used in main src files 
│   ├── sql/                          <- SQL source code
│   ├── load_data.py                  <- Script for downloading data from the input source 
│   ├── log_usage_data.py             <- Script for building the usage log database and injesting data in it
│
├── test                              <- Files necessary for running model tests 
│
├── run.py                            <- Simplifies the execution of one or more of the src scripts 
│
├── requirements.txt                  <- Python package dependencies 
```

## Running the application

Ths application can be run on both local system as well as on AWS. Steps on how to deploy the app for both settings is given below.

### 1. Set up environment 

The `requirements.txt` file contains the packages required to run the model code. An environment can be set up in two ways. 

#### With `virtualenv`

```bash
pip install virtualenv

virtualenv housePrices

source housePrices/bin/activate

pip install -r requirements.txt

```
#### With `conda`

```bash
conda create -n housePrices python=3.7.3
conda activate housePrices
pip install -r requirements.txt

```

### 2. Download the data

Original Data Source: [Kaggle](https://www.kaggle.com/c/house-prices-advanced-regression-techniques)

For the ease of downloading, the raw data has been downloaded and placed in a public s3 bucket: **s3://housing-prices-data** 

#### Local
Run the following command in bash:
```bash
python run.py fetch
```
Running this code will download the raw data from the s3 bucket and will put it in **/Data/raw/**


#### AWS
Run the following command in bash:
```bash
python run.py fetch --where=AWS --bucket=<destination_bucket_name>
```
Running this code will download the raw data from the s3 bucket and will put it in **<destination_bucket_name>/raw/**

### 3. Initialize the database

#### Local
Run the following command in bash:
```bash
python run.py create_db
```
Running this code will create a sqlite database to log the app usage at: **/Data/usage_log/msia423.db**


#### AWS

There are two ways that a database can be initialized in AWS.

##### - Take configurations from the environment:

This requires the following environment variables to be set in advance of running the code:
* MYSQL_USER : *Username to access the RDS instance*
* MYSQL_PASSWORD : *Password to access the RDS instance*
* MYSQL_HOST : *RDS instance endpoinr*
* MYSQL_PORT : *Port number to access the instance*
* MYSQL_DB : *Name of the database*

After the environment variables have been set, run the following command in bash:
```bash
python run.py create_db --where=AWS
```
Running this code will create the database specified in the given RDS instance 


##### - User input:

This does not require you to set the environment variables in advance. Run the following command in bash:
```
python run.py create_db --where=AWS --manual=yes
```
The prompt will ask you to enter the details for establishing the connection to the RDS instance, post which the database will be created. 

## Exploratory Data Analysis

[Link to the EDA notebook](deliverables/EDA/Exploratory_Data_Analysis.md) 
















