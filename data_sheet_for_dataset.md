# **Datasheet for Dataset:** 

# **MovieLens 100K**

## **1. Motivation**

**Why was this dataset created?**

To support academic and industry research in recommender systems and machine learning. MovieLens 100K was specifically designed to be a **clean benchmark dataset** for testing collaborative filtering, content-based filtering, and hybrid recommendation algorithms.

**Who created the dataset?**

The dataset was created and is maintained by **GroupLens Research**, a research lab at the University of Minnesota.

**Who funded the creation of the dataset?**

GroupLens is partially supported by the **National Science Foundation** and university research funding.

**Intended use case:**

- Collaborative and content-based recommendation
- Rating prediction and classification
- Educational purposes and algorithm benchmarking

## **2. Composition**

**What does each row represent?**

Each row in the u.data file represents a **single rating** by a user for a movie.

**How many instances?**

- **100,000 ratings**
- From **943 users**
- On **1,682 movies**

**What are the features?**

| **Feature** | **Description**                           |
| ----------- | ----------------------------------------- |
| user_id     | Integer ID of the user (1–943)            |
| item_id     | Integer ID of the movie (1–1682)          |
| rating      | Integer rating (1–5)                      |
| timestamp   | Unix timestamp (seconds since 01-01-1970) |

In u.item, each movie also includes:

| **Feature**        | **Description**                                              |
| ------------------ | ------------------------------------------------------------ |
| movie_title        | Title of the movie                                           |
| release_date       | Release date (as string)                                     |
| video_release_date | (Often empty)                                                |
| IMDb URL           | Link to IMDb page                                            |
| genre_*            | 19 binary flags (0 or 1) indicating genre membership (e.g., Action, Comedy) |

**Missing data:**

- video_release_date is mostly missing
- Some IMDb URL entries are broken due to time

**Label classes (for this project):**

- Converted to binary:
  - Ratings ≥ 4 → “Liked”
  - Ratings < 4 → “Not Liked”

## **3. Collection Process**

**How was the data collected?**

Ratings were collected through the **MovieLens website**, where registered users voluntarily rated movies.

**Timeframe of collection:**

Data collected over several months in **late 1990s**, specifically **September 1997**.

**Consent & user participation:**

Users voluntarily rated content and agreed to data usage terms. Personally identifiable information was removed.

## **4. Preprocessing**

**What preprocessing was done?**

- Users with <20 ratings were removed.
- Inconsistent or incomplete user demographic data was dropped.
- Genre columns were one-hot encoded.
- Ratings were binarized for classification tasks.

**Preprocessing by GroupLens:**

- Original dataset is **very clean** and research-ready.
- Minimal additional cleaning needed by user.

## **5. Uses**

**How is the dataset used in your project?**

- Used to build and evaluate **content-based movie recommendation models**.
- Focused on binary classification: “Will the user like this movie?”
- Used Decision Tree, KNN, Logistic Regression

**Real-world applications:**

- Personalized recommendation engines
- Cold-start problem experiments
- Performance benchmarking

## **6. Distribution**

**License:**

The dataset is available under the **GroupLens Terms of Use**, for **non-commercial, research purposes**.

[Full Terms](https://grouplens.org/datasets/movielens/terms-of-use/)

**URL for download:**

https://grouplens.org/datasets/movielens/100k/

## **7. Maintenance**

**Who maintains the dataset?**

GroupLens Research Lab, University of Minnesota

Website: https://grouplens.org

**Will the dataset be updated?**

The 100K version is static and will not change. Larger, regularly updated datasets (1M, 10M, 20M, etc.) are available.

**Contact for questions:**

grouplens-info@umn.edu