---
title:  "Coursera - Advanced Features II - Matrix Factorizations"
categories: coursera data_science
author: "Manuel"
toc: true
toc_sticky: true
---

# Recommendations

Here's a classic example of recommendations. Suppose we have some information about user, like age, region, interest and
items like gender, year and length. Also we know ratings that users gave to some items.
These ratings can be organized in a user item matrix with row corresponding to users, and columns corresponding to items, as shown in the picture. 

![Example]({{ site.baseurl }}/assets/Matrix_fact_1.png)

If we present all attributes of user and items as matrixes, the matrix product will be very close to the matrix's ratings.
In other words, which way to find matrix's U and M, such as their product gives the matrix R.
This way, this approach is called matrix factorization or matrix composition. 

![Example 2]({{ site.baseurl }}/assets/Matrix_fact_2.png)

# Documents\words example

![Example 3]({{ site.baseurl }}/assets/Matrix_fact_3.png)

# Example of feature fusion

![Example 4]({{ site.baseurl }}/assets/Matrix_fact_4.png)

# Notes about Matrix Factorization
- Can be applied only to a subset of columns
- Can provide additional diversity
    - Good for ensembles
- It is a lossy transformation. It's efficiency depends on:
    - Particular task
    - Number of latent factors (It is a good practice choose a number of parameters between 5 and 100)

# Implementation
-  Several MF (Matrix Factorization) methods can be found in sklearn
- SVD and PCA
    - Standard tools for Matrix Factorization
- TruncatedSVD
    - Works with sparse matrices (text datasets)
-  Non negative Matrix Factorization (NMF)
    - Ensures that all latent factors are non-negative
    - Good for counts-like data
    - This methods is more useful for tree based methods
    - NMF is similar in spirit to linear models. You can use the same transformation tricks

# Gotchas
Matrix Factorization is a trainable transformation, and has its own parameters. You should use the same transformation on all parts of the dataset.

Wrong way
    pca = PCS(n_components=5)
    X_train_pca = pcs.fit_transform(X_train)
    X_test_pca = pcs.fit_transform(X_test)

Right way
    pca = PCS(n_components=5)
    pcs.fir(X_all)
    X_train_pca = pcs.transform(X_train)
    X_test_pca = pcs.transform(X_test)

# Conclusion
- Matrix composition is a very general approach to dimensional reduction and feature extraction.
- It can be used for transforming categorical feature into real ones.
- Many tricks for linear models are also suitable for matrix factorizations. 