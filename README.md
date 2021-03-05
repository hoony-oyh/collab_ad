# Caution
1. The code might not be clean (almost no comments)
2. If you find something wrong or something to ask, reach me out! (fastest: email) 

# How to Run
1. Download the IDS 2018 dataset using AWS console  
`
aws s3 sync "s3://cse-cic-ids2018/Processed Traffic Data for ML Algorithms" [local path or s3 bucket address]
`
2. Run the notebooks in order `data_processing.ipynb` `training.ipynb` `experiment.ipynb`
    * caution: should change some variables related to path
    
# What is on each notebook
## `data_processing.ipynb`
1. preprocessing the data (feature selection & cleaning)
2. assigning identifier
3. partitioning the data to train / test data

## `training.ipynb`
1. Definition of the model
2. Split the data to train:valid=60:20
3. Get the threshold for each FPR(0, 0.05, ... , 0.95, 1.0) using the validation set
4. Save the model and threshold

## `experiment.ipynb`
1. Getting the loss from each test set
2. Experiment 1. Baseline
    * By using the saved threshold, calculate the FPR, TPR at each point
    * Plot the RoC curve
3. Experiment 2. Collaborative Detection
    * For each FPR (0, 0.05, ..., 0.95, 1.0)
        * Set the threshold for the same FPR on each model
        * Get the set of malicious **identifier** on each model
        * Do some voting process
        * Redistribute the voting result
        * Make decision on each organization
        * Calculate the FPR, TPR