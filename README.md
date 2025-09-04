<h1>Stress Prediction</h1>

This is a hands-on practice on Machine Learning to me for a dataset of student's stress.

Further information about Dataset: https://www.kaggle.com/datasets/mdsultanulislamovi/student-stress-monitoring-datasets/data

Link to the competition: https://www.kaggle.com/competitions/uit-thpt-competition-2025/overview (I don't know if this would support post-contest submission or not)

Here is the experiment through tries:

- First, I approach the dataset with quite a brute-force tactic, I try all the models, from Machine Learning to Deep Learning.
Machine Learning Models that I used:
    + Random Forest
    + CatBoost
    + XGBoost
    + SVM
    + KNN (later)
    * Each of the model is hand-tuned, as I was basically so lazy to do grid-search due to its duration.

Deep Learning:
    + I majorly use a neural network with 3 layers:
    * Each comes with a fully connected layer, and a ReLU or Tanh activation function attached right after it, and finally dropout for preventing overfitting.
    * Optimizer: Adam, learning_rate: 1e-3
    * Loss function: Cross Entropy Loss with label smoothing of 0.1

At first, I didn't make use of any preprocessing techniques, so the results within few first submissions were poor, with only approximately 0.88
After applying standard scaling, the results progressed a to 0.895, with the CatBoost with following hyperparameters:   

CatBoostClassifier(random_state = 42,iterations = 600,learning_rate = 1e-5,loss_function = 'MultiClass',verbose = False)

Interestingly, in all kinds of preprocessing techniques I used ranging from standardized to the upcoming Featured Set, there is always one submission of Machine Learning that reaches as high score as Deep Learning.

When I used PCA, I realized that there are some clusters that are separated from others, but also one specific cluster that is unpredictable as all kinds of stress appear in that zone. Hence, I specifically focus on that area where my model mostly predicts incorrectly.

The method is as following: I took all the points that my ML and DL model answered incorrectly, and repeatedly aded them to the training sets. The first tries yield pretty awful results as the DL model seems to overfit, while the ML model seems to underfit. Because, learning too much on the repeated samples could make the model overfit, so I decide that I'd only sample a smaller subset of the training set. And fortunately, the results rise marginally to 0.90909, with both Machine Learning and Deep Learning being capable of achieving this figure. It requires pretty careful finetuning and luck, to be honest. This version is saved in the Featured-Set Version of the notebook.

However, it all turned out to be useless when I recognized some hidden patterns in the dataset. I couldn't understand it but all students whose blood pressure is 1 and 2 are all labeled as 1, and 0 respectively. Therefore, I neglected all students of blood pressure of 1 or 2, I'd only evalutate those who suffered from high blood pressure of 3. I tried this approach and it really works, even a basic random forest could achieve a result 0.89 with this tactic. I went even further when I realized that, the sleep quality being 1 also significantly determines distress. And I label the rest as 0 because I couldn't find any other hidden patterns in the dataset. And the result was finally 0.913 but I think it could be better if there are any ways to extract hidden patterns in the filtered dataset but I don't know. This version is saved in the Iterative Version of the notebook.

Any suggestion is welcome. Thanks for reading this.
    
