# The Machine Learning Process



![image-20250331001219459](/Users/patrickedwardtapayan/Library/Application Support/typora-user-images/image-20250331001219459.png)

## Data Preprocessing: Importance of Training-Test Split in ML Model Evaluation

> [!note]
>
> splitting **training set** and **testing set**
>
> we train 80% of data - and test it on 20% of the remaning data
>
> 80% = training set
>
> 20% = testing set

![Screenshot 2025-04-02 at 00-06-56 Course Machine Learning A-Z AI Python & R ChatGPT Prize 2025 Udemy](/Users/patrickedwardtapayan/Downloads/Screenshot 2025-04-02 at 00-06-56 Course Machine Learning A-Z AI Python & R ChatGPT Prize 2025 Udemy.png)

---

## Feature Scaling In Machine Learning: Normalization vs Standardization Explained

> [!note]
>
> Feature Scaling : is always applied to columns 

### Why Feature Scaling Matters

Machine learning algorithms often depend on distances (e.g., Euclidean distance in clustering or KNN) or optimization methods sensitive to scale (e.g., gradient descent). Features measured on different scales or magnitudes can lead to:

- **Dominance:** Features with larger numeric ranges disproportionately influence the algorithm.
- **Slower convergence:** Gradient-based algorithms like neural networks or linear regression can take significantly longer to converge without feature scaling.
- **Reduced accuracy:** Algorithms relying on distance metrics (KNN, clustering methods) may yield incorrect or biased predictions.

Feature scaling addresses these issues by adjusting features into a uniform scale.



