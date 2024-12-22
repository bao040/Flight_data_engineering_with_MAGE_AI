# Flight Customer Satisfaction With Snowflake, AWS S3 and MAGE AI

### Overall Diagram 

![Description of the image](https://github.com/bao040/Flight_data_engineering_with_MAGE_AI/blob/master/flight_data_flow.png)


### Project Description: Flight Customer Satisfaction Analysis

This data engineering project focuses on analyzing and creating strongly data pipeline that can flow effectively. The dataset includes various features related to passenger demographics, flight experiences, and satisfaction levels, such as:

- **Gender**: Passenger’s gender (Female, Male)
- **Customer Type**: Loyalty status of the customer (Loyal, Disloyal)
- **Age**: Age of the passenger
- **Type of Travel**: Purpose of the flight (Personal, Business)
- **Class**: Travel class (Business, Eco, Eco Plus)
- **Flight Distance**: Distance of the flight journey
- **Service Satisfaction Levels**: Ratings for multiple services including inflight wifi, food and drink, seat comfort, boarding, baggage handling, cleanliness, etc. (Scale: 1-5, with 0 for non-applicable services)
- **Delays**: Minutes of delay during departure and arrival
- **Satisfaction**: Overall satisfaction level (Satisfied, Neutral, Dissatisfied)

### Data Flow Process for Flight Customer Satisfaction Analysis

1. **Raw Data Loading to Snowflake**:
   - The raw data, which contains various passenger-related features and their satisfaction ratings, is first loaded into **Snowflake**. Snowflake acts as a cloud-based data warehouse, providing a scalable and efficient environment for storing and querying large datasets.
   - Data is typically ingested from multiple sources (e.g., CSV files, APIs, etc.) into Snowflake using **ETL** (Extract, Transform, Load) pipelines.


![Description of the image](https://github.com/bao040/Flight_data_engineering_with_MAGE_AI/blob/master/mage_ui.png)


2. **Data Preprocessing in MAGE AI**:
   - Once the raw data is in Snowflake, it is passed to **MAGE AI**, a modern data orchestration tool that helps streamline the data transformation process.
   - In MAGE AI, several preprocessing steps are applied to clean and prepare the data for analysis and modeling:
     - **Data Cleansing**: Remove or handle missing, erroneous, or duplicate data entries.
     - **Column Selection**: Unnecessary columns (such as identifiers or irrelevant features) are dropped to reduce noise and improve model performance.
     - **Feature Engineering**: New features may be created, such as combining or transforming existing columns (e.g., creating categories for age groups or normalizing satisfaction ratings).
     - **Data Type Conversion**: Ensure all features are in the appropriate format (e.g., converting categorical data into numerical form for machine learning).

3. **Dimensional and Fact Table Creation (Data Modeling) in MAGE AI**:
   - In this step, the data is structured into **dimensional** and **fact** tables:
     - **Dimensional Tables**: These tables store descriptive information (e.g., Customer Type, Travel Class, and Services). These are often used for lookups or as reference data in queries.
     - **Fact Tables**: These tables store quantitative data, such as passenger satisfaction scores, flight distances, and delays. Fact tables typically have foreign keys referencing the corresponding dimensional tables.
   - **Data Modeling**: The tables are organized using data modeling techniques like **Star Schema** or **Snowflake Schema** to optimize query performance and ensure data integrity.

4. **Storing Processed Data in Amazon S3**:
   - After transforming and structuring the data into fact and dimensional tables, these tables are stored in **Amazon S3** for long-term storage and easy access.
   - The data in S3 is typically stored in format **CSV** to maintain efficiency and facilitate further analysis.
  
  ![Description of the image](https://github.com/bao040/Flight_data_engineering_with_MAGE_AI/blob/master/aws_s3_data_storage.png)
  

5. **Data Exploration & Visualization**:
   - During the data exploration phase, the data is analyzed using tools like **Jupyter Notebooks** or visualization libraries (e.g., **Matplotlib**, **Seaborn**) to gain insights into trends and patterns.
   - Visualizations might include:
     - Distribution of satisfaction levels across different features (e.g., Gender, Age, Travel Class)
     - Correlation matrices to identify relationships between service satisfaction and customer satisfaction
     - Flight delay analysis and its impact on satisfaction
   - These visualizations guide decision-making and inform feature selection for the machine learning models.

6. **Model Training and Evaluation**:
   - Using the processed data, machine learning models are trained to predict customer satisfaction based on the various features.
   - Two models are used for this task:
     - **RandomForestClassifier**: An ensemble learning model that uses multiple decision trees to classify customer satisfaction into categories (Satisfied, Neutral, Dissatisfied).
     - **LogisticRegression**: A simpler model that predicts the probability of customer satisfaction based on the features.
   - The models are trained using training data and evaluated on validation data to assess accuracy, precision, recall, and other metrics. Hyperparameter tuning may be applied to improve model performance.
