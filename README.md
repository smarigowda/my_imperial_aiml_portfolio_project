# Exploring Datasets for Content Recommendation:

From my exploration, I found the following data sets which I can use for the Content Recommendation.

Dataset for recommender system

https://github.com/caserec/Datasets-for-Recommender-Systems?tab=readme-ov-file

Collaborative Filtering Recommendation System

https://www.kaggle.com/code/abdallahwagih/collaborative-filtering-recommendation-system#2.-Data-Preparation

Annimie recommendation database.

https://github.com/soham96/hyperparameter_optimisation

MoveLens

[https://movielens.org](https://movielens.org/)

**I chose to use Movie Lense dataset.**

# Research Question/ Objective:

The question I would like to answer using a ML model is to recommend content (e.g., movies, articles, songs) to users based on preferences or features. **Content-based filtering** (based on item features like genre, tags, etc.)

# Dataset Selected:

GroupLens Research has collected and made available rating data sets from the MovieLens web site ([https://movielens.org](https://movielens.org/))

I will be using this data set https://grouplens.org/datasets/movielens/ for my Portfolio Project. This data set has 100000 ratings by 943 users on 1682 items. Each user has rated at least 20 movies.  Users and items are numbered consecutively from 1.  The data is randomly ordered. The time stamps are unix seconds since 1/1/1970 UTC. The last 19 fields are the genres, a 1 indicates the movie is of that genre, a 0 indicates it is not; movies can be in several genres at once. **Features:** Movie titles, genres, user ratings

# Pre-Processing the data:

**MovieLens 100K dataset** https://grouplens.org/datasets/movielens/100k/ which I am planning to use is **very clean** and was curated specifically for ML research. This data has been cleaned up - users who had less than 20 ratings or did not have complete demographic information were removed from this data set, so I am expecting that **minimal preprocessing is needed**

# KNN Model:

# Tested with n_neighbors = 5, 8 and 10

#### Model Evaluation with n_neighbors = 5

| Metric        | Value  | Interpretation                                               |
| ------------- | ------ | ------------------------------------------------------------ |
| **Accuracy**  | 0.5210 | Only ~52% of predictions were correct. Barely better than random guessing (50%) in a binary task. |
| **Precision** | 0.5897 | ~59% of the items predicted as "liked" were actually liked. That’s decent — the model is somewhat conservative in predicting positives. |
| **Recall**    | 0.4216 | Low — the model is missing many true positives (items users actually liked). |
| **F1 Score**  | 0.4916 | Harmonic mean of precision and recall — this indicates overall balance is weak. |

#### Assessment

- **Precision is higher than recall**, which means the model is **cautious** — when it says a user will like something, it's reasonably accurate, but it **misses many good recommendations**.
- **Low accuracy and recall** suggest this model isn’t capturing enough patterns in the data.
- **Features (just genres) may not be rich enough**. Also, KNN struggles when:
  - Input features are sparse or limited
  - Data has noise
  - Classes are not well-separated in feature space



# **Decision Tree Model:**

# **Performance Summary**

| Metric    | Class 0 ("Not Liked") | Class 1 ("Liked") |
| --------- | --------------------- | ----------------- |
| Precision | 0.58                  | 0.62              |
| Recall    | 0.42                  | 0.75              |
| F1-Score  | 0.49                  | 0.68              |

### Overall:

- **Accuracy**: `0.60`
- **Macro Avg F1-Score**: `0.58`
- **Weighted Avg F1-Score**: `0.59`

------

## Interpretation

### Improvements over KNN:

- Accuracy increased from **0.52 (KNN)** → **0.60**
- F1 score for class 1 (Liked) improved significantly: **0.49 (KNN)** → **0.68**
- Higher **recall (0.75)** for liked items means it finds more of what the user would like.
- Model is better at identifying "Liked" content — very useful for recommendations.

### Limitations:

- Still weaker at predicting “Not Liked” (low recall of 0.42).
- May be **overfitting** slightly — you can check this by comparing training vs. validation/test scores.
- Could benefit from **hyperparameter tuning** (like `max_depth`, `min_samples_split`, etc.)

# Logistic Regression

### **Model Comparison (Test Set)**

| Metric        | KNN   | Decision Tree | Logistic Regression |
| ------------- | ----- | ------------- | ------------------- |
| **Accuracy**  | 0.521 | **0.60**      | 0.58                |
| **Precision** | 0.59  | **0.60**      | 0.57                |
| **Recall**    | 0.42  | **0.59**      | 0.56                |
| **F1 Score**  | 0.49  | **0.58**      | 0.56                |

### **Observations:**

- **Decision Tree** performs the best **overall**, with the highest accuracy, F1 score, and good balance across both classes.
- **Logistic Regression** is a close second. It has slightly lower F1 score but does well on **recall for class 1 (0.77)** — this could be important if you care about catching all positive recommendations.
- **KNN** performs the weakest overall, especially in recall and F1 score.

------

### **Recommendation:**

Since Decision Tree gave the **best balance of metrics**, let's proceed with **hyperparameter tuning on the Decision Tree** to see if we can improve it further.

# Hyperparameter Tuning

Let's perform **hyperparameter tuning** on the **Decision Tree Classifier** using **GridSearchCV** to optimize its performance.

We'll tune key parameters like:

- `max_depth`: controls how deep the tree can go
- `min_samples_split`: minimum samples required to split a node
- `min_samples_leaf`: minimum samples required at a leaf node
- `criterion`: function to measure the quality of a split (`gini` or `entropy`)

### **Performance Summary (Tuned Decision Tree)**

| Metric        | Before Tuning | After Tuning |
| ------------- | ------------- | ------------ |
| **Accuracy**  | 0.60          | 0.60         |
| **Precision** | 0.60          | 0.60         |
| **Recall**    | 0.59          | 0.59         |
| **F1 Score**  | 0.58          | 0.59         |

> **Result:** The improvement is minimal — only a slight bump in F1 score and macro average, suggesting the untuned tree was already near optimal or that the model's performance is limited by the data/features.

### Comparison with Other Models:

| Model             | Accuracy | F1 Score (weighted) |
| ----------------- | -------- | ------------------- |
| **KNN**           | 0.52     | 0.49                |
| **Decision Tree** | 0.60     | 0.59                |
| **Logistic Reg.** | 0.58     | 0.56                |



✅ **Best model: Decision Tree (tuned)**

# Non Technical Report

### Objective

I have built a system that helps suggest movies users are likely to enjoy, based on their past viewing and rating behavior. This system supports users in discovering relevant content without being overwhelmed by too many options.

------

### The Data

I have used the **MovieLens dataset**, which includes:

- Users
- Movies
- Ratings (from 1 to 5 stars)

To simplify, we converted the ratings into:

- "Liked" (ratings of 4 or 5)
-  "Not Liked" (ratings below 4)

This helped us focus on predicting whether a user would like a particular movie.

------

### How the Recommendation Works

We used a machine learning technique called a **Decision Tree**. Think of a decision tree as a **set of simple yes/no questions** that help determine whether a user would like a movie.

**Example:**

- Has the user liked other movies in the same genre?
- Is the average rating of the movie high?
   → Recommend the movie!

It works similarly to how a friend might recommend a movie based on your past preferences.

------

### Why Decision Tree?

I tried three different methods:

- K-Nearest Neighbors (KNN)
- Logistic Regression
- Decision Tree

Out of these, **Decision Tree gave me the best performance**, balancing **accuracy** and **clarity**.

------

### Performance Summary

On unseen test data, the decision tree correctly predicted preferences **60% of the time**. It was especially good at identifying movies users are **likely to enjoy**, with a **75% recall rate** (meaning it caught most of the movies people liked).

------

### Benefits for Users

- **Faster discovery**: Fewer bad recommendations.
- **Personalization**: Picks movies tailored to your taste.
- **Transparent**: The logic behind recommendations is understandable.

------

### Next Steps

We can make this system even better by:

- Using more data (e.g., movie descriptions, user demographics).
- Combining it with other models (like Random Forest).
- Deploying it in a real movie streaming platform.
