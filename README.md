## Table of contents
* [General info](#general-info)
* [Data](#data)
* [Methods](#methods)

## General info
### Goal
The goal of this project is to implement and compare the performance of different recommender system methods. The interest lies in estimating the rating that a user would give to a specific movie.

### I used:
* Python 3.6.9
* numpy 1.18.5
* matplotlib 3.2.2

### Notebooks
* **Naive_Approaches.ipynb** contains the implementation of four naive approaches that estimate the rating that a user would give to a movie.
* **Matrix_factorization.ipynb** contains the implementation of the matrix factorization algorithm.

## Data
The file ratings.dat contains the data used for this project. It consists of 1,000,209 anonymus ratings of users that joined [MovieLens](https://grouplens.org/datasets/movielens/) at the year 2000 and three columns that represent the user id, the movie id and the rating which is on a 5-star scale (whole ratings). There is a total of 6,040 users and 3,952 movies with each user having at least 20 ratings.

## Methods

### Naive approaches

Four naive approaches are implemented on this data, these are:

- R<sub>global</sub>(User,Item)=mean(all ratings)
- R<sub>item</sub>(User,Item)=mean(all ratings for item)
- R<sub>user</sub>(User,Item)=mean(all ratings for user)
- R<sub>user-item</sub>(User,Item)= &alpha;*R<sub>user</sub>(User,Item) + &beta; *R<sub>item</sub>(User,Item) + &gamma;

Where R(User,Item) stands for the estimate of the rating that an active user would give to a certain item. To assess and compare the performance of these approaches, 5-fold cross-validation is being used in order to get a more honest estimate of their training and test errors. For every approach, the Root mean squared error is being used for assessment. 

The naive approaches are characterized that way because of their simplicity. Especially the first three approaches use information from one source only, either the users or the movies (items). So, even though they work up to a certain extend they have some important limitations which are discussed further on the corresponding python notebook.

### Matrix Factorization
More details about the training proccess of this algorithm can be found in **Matrix_factorization.ipynb**.

#### **Algorithm summary**:

- For each fold (1 through 5):
    - Split the dataset to training and test set.
    - Initialize the values of U and V randomly from the standard normal distribution.
    - Loop until the RMSE on the test set has very little difference between two iterations :
        - For every sample x<sub>ij</sub> in the training data :
            - Calculate the error e<sub>ij</sub>
            - Update the i-th row of $U$ and the j-th column of V.
        - Calculate the RMSE on the training and test set.
        - if the absolute difference of the RMSE on the test set, between two iterations is less than 0.001, go to             the next iteration.

