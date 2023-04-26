
- [1. Clarifying requirements](#1-clarifying-requirements)
  - [business objective](#business-objective)
  - [features the system needs to support](#features-the-system-needs-to-support)
  - [data](#data)
  - [constraints](#constraints)
  - [scale of the system](#scale-of-the-system)
  - [performance](#performance)
- [2. Framing the problem as an ML task](#2-framing-the-problem-as-an-ml-task)
  - [Defining the ML objective](#defining-the-ml-objective)
  - [Specifying the system's input and output](#specifying-the-systems-input-and-output)
  - [Choosing the right ML category](#choosing-the-right-ml-category)
    - [Common ML categories](#common-ml-categories)
- [3. Data preparation](#3-data-preparation)
  - [Data engineering](#data-engineering)
    - [Data source](#data-source)
    - [Data storage (database)](#data-storage-database)
    - [Extract, transform, and load (ETL)](#extract-transform-and-load-etl)
    - [Data types in ML](#data-types-in-ml)
  - [Feature engineering](#feature-engineering)
    - [Operations](#operations)
      - [Missing values](#missing-values)
      - [Feature Scaling](#feature-scaling)
      - [Discretization](#discretization)
      - [Encoding categorical features](#encoding-categorical-features)
        - [integer encoding](#integer-encoding)
        - [one-hot encoding](#one-hot-encoding)
      - [embedding learning](#embedding-learning)
- [4. Model development](#4-model-development)
  - [Model selection](#model-selection)
    - [Establish a simple baseline](#establish-a-simple-baseline)
    - [Experiment with simple models](#experiment-with-simple-models)
    - [Switch to more complex models](#switch-to-more-complex-models)
    - [Use an ensemble of models if more accurate predictions are needed](#use-an-ensemble-of-models-if-more-accurate-predictions-are-needed)
  - [Model training](#model-training)
    - [Constructing dataset](#constructing-dataset)
    - [Choosing the loss function](#choosing-the-loss-function)
    - [Training from scratch vs. fine-tuning](#training-from-scratch-vs-fine-tuning)
    - [Distributed training](#distributed-training)
- [5. Evaluation](#5-evaluation)
  - [offline evaluation](#offline-evaluation)
  - [online evaluation](#online-evaluation)
- [6. Deployment and serving](#6-deployment-and-serving)
  - [Cloud vs. on-device deployment](#cloud-vs-on-device-deployment)
  - [Model compression](#model-compression)
  - [Testing in production](#testing-in-production)
    - [Shadow deployment](#shadow-deployment)
    - [A/B testing](#ab-testing)
  - [Prediction pipeline](#prediction-pipeline)
    - [batch prediction](#batch-prediction)
    - [online prediction](#online-prediction)
- [7. Monitoring and infrastructure](#7-monitoring-and-infrastructure)
## 1. Clarifying requirements

Ensure everyone is on the same page.


### business objective

e.g., create a system to recommend vacation rentals (increase the bookings/ increase the revenue)

### features the system needs to support

e.g., a video recommendation system (want to know if users can like or dislike recommended videos) -> used to label training data

### data

- data sources?
- data size?
- data labeled?

### constraints

- available computer power 
- cloud-based/ local-based

### scale of the system

- number of users
- number of items that are needed to deal

### performance

- prediction speed
- real-time/ off-line solution

## 2. Framing the problem as an ML task

Determine if ML is necessary for solving a given problem first.

### Defining the ML objective

- Translate the business objective into a well-defined ML objective. (some examples on Page 4)

### Specifying the system's input and output

- specify input and output for each model
- might be multiple ways to specify each model's input-output

### Choosing the right ML category

#### Common ML categories

![ML categories](./img/c1-ml-categories.png)

## 3. Data preparation

### Data engineering

#### Data source

- who collect the data
- is data clean?
- trusted data source?
- user-generated or system-generated data

#### Data storage (database)

- SQL (relational)
- NoSQL

#### Extract, transform, and load (ETL)

- extract: extract data from different data sources
- transform: cleansed, mapped, transformed into specific format to meet operational needs
- load: loaded into target destination

#### Data types in ML

![data-types](./img/c1-datatypes.png)

### Feature engineering

- Select and extract predictive features from raw data
- Transform predictive features into a format usable by the model

#### Operations

Refer to Page 10

##### Missing values

- Deletion
- Imputation
  - fill with default
  - fill with mean, median, or mode

##### Feature Scaling

Scaling features to have a standard range and distribution

- Normalization (min-max scaling) [do not change data distribution]
- Standardization (z-score normalization)
- Log scaling [mitigate the skewness of a feature/ converge faster during optimization]

##### Discretization

Converting a continuous feature into a categorical feature.

##### Encoding categorical features

###### integer encoding

- assign an integer value to each unique category value
- useful if  ordinal relationship exists between categorical features

###### one-hot encoding

- create a binary feature for each unique value

##### embedding learning

- learning an N-dimensional vector for each unique value that the categorical feature may take
- useful when the number of unique values is very large (one-hot may lead to large vector sizes)

## 4. Model development

### Model selection

- logistic regression
- linear regression
- decision trees
- gradient boosted decision trees and random forests
- support vector machines
- Naive Bayes
- factorization machines
- neural networks

Some aspects to consider:

- amount of data the model needs to train
- training speed
- hyperparameters
- continual learning possibility
- compute requirement (CPU, GPU)
- model's interpretability

#### Establish a simple baseline

#### Experiment with simple models

#### Switch to more complex models

#### Use an ensemble of models if more accurate predictions are needed

### Model training

#### Constructing dataset

1. collect raw data
   - refers to [data preparation](#3-data-preparation)
   
2. identify features and labels
   - refers to [feature engineering](#feature-engineering)
   - labeling
     - hand labeling: human-involved
     - nature labeling
   
3. select a sampling strategy
   - reduce the amount of data in the system
   - convenience sampling, snowball sampling, stratified sampling, reservoir sampling, importance sampling.
   
4. split the data
   - divide data into training/ evaluation/ test data
   
5. address class imbalance (if any)
   - majority class: a class makes up a larger proportion of the dataset
   - minority class: model may not have enough data to learn the class 
   
   **Resampling training data**: adjust the ratio between different classes, making data more balanced
   
   e.g., over-sample the minority class/ undersample the majority class
   
   **Altering the loss function**: make it more robust against class imbalance, giving more weight to data points from the minority class.
   
   - a higher weight in the loss function: penalizes the model more when it makes a wrong prediction about a minority class
   
   e.g., *class-balanced loss* & *focal loss*

#### Choosing the loss function

- may need to make minor changes to the loss function to make it specific to the problem

#### Training from scratch vs. fine-tuning

- fine-tuning: continuing to train the model on new data by making small changes to its learned parameters

#### Distributed training

- train the model by dividing the work among multiple worker nodes
- operate in parallel in order to speed up model training
  - data parallelism
  - model parallelism

## 5. Evaluation

### offline evaluation

- evaluating the performance of ML models during the model development phase
  - make predictions using the evaluation dataset
  - use offline metrics to measure how close the predictions are to the ground-truth values

### online evaluation

- evaluating the performance of ML models in production after deployment
- usually tied to business objectives

## 6. Deployment and serving

### Cloud vs. on-device deployment

- refer to Page 22 Table 1.6

### Model compression

- the process of making a model smaller
- reduce inference latency and model size

1. knowledge distillation

   train a small model (student) to mimic a larger model (teacher)

2. Pruning

   find the least useful parameters and set them to zero -> sparser models, stored more efficiently

3. Quantization

   - model parameters are often represented with 32-bit floating numbers
   - use fewer bits to represent the parameters
   - can happen during training or post-training

### Testing in production

#### Shadow deployment

- deploy the new model in parallel with the existing model
- each incoming request is routed to both models
  - only the existing model's prediction is served to the user

- minimize the risk of unreliable predictions until the newly developed model has been thoroughly tested
- costly (doubles the number of predictions)

#### A/B testing

- deploy the new model in parallel with the existing model
- a portion of the traffic is routed to the newly deployed model, the remaining requests are routed to the existing model
  - the traffic routed to each model should be random
  - should be run on a sufficient number of data points in order for the results to be legitimate

### Prediction pipeline

Refers to Page 24

- make a choice between online prediction and batch prediction

#### batch prediction

- model predicts periodically 
- predictions are pre-computed, no need to worry about inference latency

#### online prediction

- predictions are generated and returned as soon as requests arrive

## 7. Monitoring and infrastructure

- process of tracking, measuring, logging different metrics
