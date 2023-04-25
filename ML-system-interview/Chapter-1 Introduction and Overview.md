[toc]

# To structure answers

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

## 5. Evaluation

## 6. Deployment and serving

## 7. Monitoring and infrastructure

