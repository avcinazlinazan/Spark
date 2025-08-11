## K-Means Clustering Consulting Project Solution
In this project, you examined a piece of evidence from a cybersecurity investigation to determine whether two or three hackers were responsible for a series of hacking incidents. Your underlying assumption was that if there were two or three hackers, each would have approximately the same number of hacks.

### What Was Done in the Project?
###  1. Data Preparation and Feature Selection:

First, a Spark session was launched and the dataset containing the hacking incidents (hack_data_set.csv) was loaded.

The location column in the dataset was assumed to be unreliable due to VPN use and was omitted. The remaining numerical features (Session_Connection_Time, Bytes Transferred, etc.) were selected for use in the model.

These features were combined into a single vector column using VectorAssembler.

The data was scaled with StandardScaler to improve model performance and compensate for the different feature sizes.

### 2. Model Training and Comparative Analysis:

To answer the main question, two different K-Means models were trained: one with K=2 (assuming two hackers) and the other with K=3 (assuming three hackers).

Both models were trained by fitting the scaled dataset using the fit() method.

###  3.Evaluation and Interpretation of Results:

After training, the clusters (prediction column) of the data were predicted for both models using the transform() method.

The number of hacking events for each prediction value (0, 1, 2) was counted using groupBy() and count() operations.

Results for K=3: When the model divided the data into three groups, the number of hacks (e.g., 88, 79, 1) was not equal. This contradicted the assumption that hackers committed equal hacking attacks.

Results for K=2: When the model divided the data into two groups, the number of hacks (e.g., 167, 167) was almost equal. This result perfectly aligned with the assumption that the hackers committed an equal number of hacks.

What We Found in the Project and How Do We Interpret It?
The clearest conclusion from this project is that there must have been two hackers.

**Interpretation:**

**Evidence:** 
When trained with K=2, the K-Means model divided the hacking incidents into two equal groups (167 vs. 167). This supports the forensic engineer's assumption that each hacker committed an approximately equal number of hacks.

**Rejecting the Evidence:**
When the model was trained with K=3, the resulting groups differed significantly in size (e.g., 88, 79, 1). This contradicts the assumption that the number of hacks would be equal in the presence of a third hacker. When the algorithm forcibly divided the data into three groups, it showed that there was no natural balance between these groups.

**Conclusion:**
The K-Means model's predictions clearly indicate that the most logical and balanced grouping of the hacking incidents is into two clusters. This strengthens the conclusion that two hackers were behind the cyberattacks.

This project brilliantly demonstrates how a clustering algorithm can be used not only to find clusters but also to test hypotheses and draw conclusions based on them.