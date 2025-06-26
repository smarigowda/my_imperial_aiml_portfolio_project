# **Model Card:**

# **MovieLens Content Recommendation System**

## **1.** **Model Overview**

**Name**: MovieLens Content-Based Recommendation using Decision Tree

**Author**: Santosh Marigowda

**Industry**: Media and Entertainment

**Objective**: To recommend movies users are likely to enjoy based on their historical ratings and item metadata using classification models.

**Primary Audience**: Streaming platform users, content curation teams.

## **2.** **Model Details**

- **Model Type**: Supervised Binary Classification
- **Algorithm**: Decision Tree Classifier (after comparison with KNN and Logistic Regression)
- **Features Used**:
  - Movie genre (multi-hot encoded)
  - Simplified user preference (binary labels: “Liked” or “Not Liked”)
- **Target Variable**: Binary variable indicating whether a user would like a movie (Liked if rating ≥ 4)

## **3.** **Dataset Details**

- **Name**: MovieLens 100K
- **Source**: https://grouplens.org/datasets/movielens/100k/
- **Description**: Contains 100,000 ratings from 943 users on 1,682 movies. Each movie includes binary genre tags; all users rated at least 20 movies.
- **Preprocessing**: Minimal (already cleaned); ratings binarized into “Liked” (≥4) and “Not Liked” (<4).

## **4.** **Evaluation Metrics**

| **Metric** | **KNN** | **Logistic Regression** | **Decision Tree** | **Tuned Decision Tree** |
| ---------- | ------- | ----------------------- | ----------------- | ----------------------- |
| Accuracy   | 0.52    | 0.58                    | 0.60              | 0.60                    |
| Precision  | 0.59    | 0.57                    | 0.60              | 0.60                    |
| Recall     | 0.42    | 0.56                    | 0.59              | 0.59                    |
| F1 Score   | 0.49    | 0.56                    | 0.58              | 0.59                    |

> **Best Model Chosen**: Decision Tree (with minor improvement post tuning)

## **5.** **Use Case**

- **Problem Statement**: Users face information overload when trying to choose movies.
- **Goal**: Simplify discovery by suggesting movies aligned with user tastes.
- **Real-World Application**: Integration into streaming platforms for personalized content discovery.

## **6.** **Limitations**

- **Feature Limitation**: Model only uses genre features; deeper insights could come from movie descriptions, user demographics, reviews, or timestamps.
- **Recall Bias**: Despite improved recall (0.75 for liked class), predictions for “Not Liked” content still have low recall.
- **Overfitting Risk**: Decision Trees are prone to overfitting; cross-validation or ensemble models like Random Forest could help.
- **Scalability**: May struggle as user/item volume increases; would benefit from matrix factorization or hybrid filtering.

## **7.** **Ethical Considerations**

- **Bias**: Model may favor popular genres or mainstream content over niche interests.
- **Privacy**: All data used is anonymized; however, real deployments must comply with data protection standards (GDPR).
- **Transparency**: Decision Trees provide explainability, which is beneficial in sensitive recommendation contexts.

## **8.** **Next Steps**

- Use ensemble models like **Random Forest** or **XGBoost** for improved accuracy and robustness.
- Add **user-level features** (e.g., demographics, session time).
- Explore **hybrid models** combining content- and collaborative-filtering.
- Deploy as a **recommendation microservice** on a streaming platform prototype.