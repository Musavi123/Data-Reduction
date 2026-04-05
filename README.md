# Data-Reduction

Overview

Here I explore Exploratory Data Analysis (EDA), dimensionality reduction, and feature selection techniques applied to a high-dimensional Kaggle dataset. 

The project utilizes the Airline Passenger Satisfaction dataset.

    Size: The original dataset contains 23 features and 103,904 rows.

    Features: It encompasses passenger demographics and trip details (gender, customer type, age, class, flight distance, purpose of travel) alongside satisfaction ratings for various aspects of the flying experience, such as booking procedures, cleanliness, and inflight services.

    Target Variable: The data provides insight into whether a passenger was 'satisfied' or 'neutral or dissatisfied'.

Methodology

To prepare the data and evaluate different machine learning approaches, the project was broken down into three main phases:

1. Preprocessing and EDA

    Sampling: The dataset was initially down-sampled to one-tenth of its original size to speed up processing times, specifically for later dimension reduction steps.

    Cleaning & Encoding: Missing values were handled by replacing them with the mean of their respective columns. Categorical variables were converted using label encoding, and the target variable ('satisfaction') was mapped to a binary numeric format (1 for 'satisfied', 0 for 'neutral or dissatisfied').

    Scaling: All numerical features were standardized using StandardScaler to ensure they were on the same scale.

    Visualization: The EDA process included generating count plots for the target variable, histograms and box plots to explore numerical feature distributions, and a heatmap to visualize feature correlations.

2. Dimensionality Reduction
The project employed three techniques to reduce the feature space to two dimensions (n_components=2) to explore the underlying structure of the data:

    PCA (Principal Component Analysis): Used to preserve maximum variance.

    t-SNE & UMAP: Non-linear techniques used to preserve local and global structures. (Note: The data was further down-sampled by dividing by 10 to allow these specific models to compute efficiently ).

3. Feature Selection
A Random Forest Classifier (RFC) from the scikit-learn library was used to test how feature selection impacted predictive performance. A baseline model was trained on the full preprocessed dataset without feature selection to serve as a benchmark. This was compared against:

    Filter Method: Using SelectFromModel based on importance scores from the RFC.

    Wrapper Method: Using Recursive Feature Elimination (RFE) to iteratively select relevant features.

Key Findings

    Dimensionality Reduction Results: While PCA resulted in one large cluster separated by a parabola, both t-SNE and UMAP successfully identified three clear clusters. Ultimately, UMAP provided the most defined and separated clusters.

    Baseline Accuracy: The initial RFC model achieved a high predictive accuracy of approximately 94.61% without any feature selection.

    Filter Method Trade-offs: The SelectFromModel approach reduced the required features by nearly one-third, but resulted in a slight accuracy decrease to approximately 94.42%, indicating minor information loss.

    Wrapper Method Success: RFE proved to be the most effective method. It successfully reduced the feature space by one-third while increasing the model's accuracy to approximately 94.99%. This suggests the subset selected by RFE is highly discriminative for this specific classification task
