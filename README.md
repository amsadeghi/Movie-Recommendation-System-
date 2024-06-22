**Building a Movie Recommendation System Using PySpark**
-
**Objective:**

Develop a movie recommendation system.

Utilize collaborative filtering with Alternating Least Squares (ALS).

Implement hyperparameter tuning for model optimization.
-------------------
**1. Installing PySpark library**
-
Install PySpark to enable the development of the recommendation system.

PySpark is a Python API for Spark.

**2. Importing the needed libraries**
-
**3. Initializing Spark Session**
-
The session is the entry point for DataFrame and SQL functionality.

**4. Load ratings and movies datasets from CSV files.**
-
header=True indicates that the first row is a header.

inferSchema=True automatically infers data types.

**5. Data Caching and Cleaning**
-
Cache the data for better performance as they are accessed multiple times.

Drop rows with null values to ensure data quality.

**6. Preparing Data for ALS**
-
Convert data types to integers for userId and movieId, and float for rating.

ALS requires specific data types for processing.

**7. Splitting the Data**
-
Split the ratings data into training (80%) and test (20%) sets.

A seed value ensures reproducibility.

**8. Building and Training the ALS Model**
-

ALS (Alternating Least Squares) is a popular algorithm used in collaborative filtering for building recommendation systems. It is particularly well-suited for scenarios involving large datasets of user-item interactions, such as movie ratings, product purchases, or any situation where recommendations are made based on user behavior.

*Collaborative Filtering:*
----
* ALS is a collaborative filtering technique, meaning it makes recommendations based on patterns of user-item interactions (e.g., which users rated which movies and how).
It focuses on finding latent factors that explain observed user-item interactions.

*Matrix Factorization:*
-
* The core idea behind ALS is to factorize a large user-item interaction matrix $R$ into two lower-dimensional matrices: $U$ (user factors) and $M$ (item factors).

 $R≈U⋅M^T, where: $

 * $R$ is the original user-item interaction matrix.
 * $U$ is the user-factor matrix (users x latent factors).
 * $M$ is the item-factor matrix (items x latent factors).

*Alternating Optimization:*
-
* ALS iteratively optimizes one matrix while keeping the other fixed, alternating between the two until convergence.
* First, it fixes the item matrix $M$ and solves for the user matrix $U$.
* Then, it fixes the user matrix $U$ and solves for the item matrix $M$.
* This process is repeated until the algorithm converges to a solution.

*Loss Function:*
-
* ALS minimizes the regularized least squares error:

  $∑_{(u,i)∈R}(R_{ui}−U_u⋅M_i)^2+λ(∥U∥^2+∥M∥^2)$
 * $(u,i)∈R$ are the observed user-item interactions.
 * $R_{u,i}$ is the observed rating of user $u$ for item $i$.
 * $U_u$ is the latent factor vector for user $u$.
 * $M_i$​ is the latent factor vector for item $i$.
 * $λ$ is a regularization parameter to prevent overfitting.

Configure the ALS model with specified parameters.

Train the model using the training dataset.

**9. Making Predictions**
-
Generate predictions on the test dataset. Before refining tuning on the full dataset serves the purpose of quickly assessing the initial performance of the ALS model. It's crucial for understanding the starting point of model effectiveness and provides a baseline for comparison with the refined model after hyperparameter tuning.

Display the first five predictions.

**10. Evaluating the Model**
-    
Evaluate the model using RMSE (Root Mean Square Error).

Lower RMSE indicates better model performance.

**11. Hyperparameter Tuning**
-
Build a parameter grid to search for optimal ALS hyperparameters.

Use cross-validation for robust evaluation.

**12. Initial Tuning on a Smaller Sample**
-
Perform initial hyperparameter tuning on a smaller subset of the training data.

Extract and display the best parameters.

**13. Refine Tuning on Full Dataset**
-
Conduct full hyperparameter tuning using the entire training dataset.

Evaluate the refined model's performance on the test dataset.

**14. Generating Recommendations**
-
Generate top 10 movie recommendations for a specific user.

Example shown for user_id = 123.

**15. Displaying Recommended Movie Titles**
-
Explode the recommendations column to get individual movie recommendations.

Join with the movies dataset to display movie titles and ratings.

