# Deploying-a-Sentiment-Analysis-Model
Use AWS SageMaker to deploy a model for web app


## Summary 
-	Completed a machine learning full workflow: explore and process data – modeling – deployment for a web app
- Built an RNN model to determine the sentiment of a IMDV movie review using Amazon's SageMaker service. 
- Deploy the model and construct a web app that allow communication between user's data prediction with accuracy of 82%. 



## Steps

- Install SageMaker

### 1. Data preparation
- Download IMDB dataset
- Split into train and test datasets
- Remove html tags and stopwords in reviews using Be autifulSoup 
- Build a cache file for results
- Tokenize words in all reviews {ind:words}, then sort by the occurring frequency
- Let each review has 500 words. If not, pad with 0. 

### 2. Upload data to S3
- Save training data locally
- upload training data to S3

### 3. Build and Train the PyTorch Model
- Build RNN model using Pytorch
    - Import data, and build DataLoader
    - Train: 
        - define LSTM model
        - define loss function
        - forward + backward
- Train the model
    - Define sagemaker.pytorch predictor
    - fit model
    
### 4. Deploy model: create endpoint
- Deploy a predictor

### 5. Testing
- Test 1
    - Use the predictor to get predictions for processed testing data
    - Cal accuracy
- Test 2
    - Use the predictor to get predictions for unprocessed review
    - process the review: a sentence as input --> Tokenization --> padding 
    - prediction

### 6. Deploy the model for the web app
- Write a function of all data preprocessing
- Define a RealTimePredictor
- Deploy
- Testing
    - 250 string reviews(unprocessed data) as input
    - pass to predictor
    - Cal accuracy

### 7. Setup Lambda function
- Construct lambda function
    - give this function permission to send and recieve data from a SageMaker endpoint.

### 8. setup API gate
- API is used to create new endpoint(URL) to execute Lambda function
