# Digit Recognition in GNU Octave

Eigenvalues and eigenvectors play a crucial role in solving the problem of digit recognition. This problem serves as a starting point for other similar algorithms, such as general handwriting recognition. Digit recognition (or commonly known as Digit Recognition) is used by banks for check processing, automatic reading of personal addresses, and automatic reading of completed forms. In the vast majority of cases, this problem is fundamental for individuals working in the field of machine learning.

The PCA algorithm is also used in this domain, often to reduce the dimensionality of data while preserving the most important aspects of the input received. As a result, the accuracy does not suffer significantly, but the processing time of information is significantly reduced, which is very useful when working with very large datasets.

Before discussing how recognition will be performed, let's first talk briefly about the dataset. "MNIST" is a dataset of 70,000 labeled images, containing handwritten digits collected from a multitude of people. The dataset consists of 60,000 training images and 10,000 test images. The images are grayscale and have dimensions of 28x28 pixels.

For solving the problem at hand, there are many approaches, with the most commonly used ones leveraging neural networks. To demonstrate how such a solution can look, I have prepared a Python program using Google Colab that recognizes digits with an accuracy of 98.4%, which can be found at the following link:

[Google Colab - Digit Recognition](https://colab.research.google.com/drive/1o_O4E-75-G1CFjY599E1Cd5yPcw-XO5s?usp=sharing)

However, I proposed an algorithm based on PCA which achieves an accuracy of approximately 93.3%. This method is simpler to understand and apply compared to those relying on machine learning methods.

## TASK 1:
- I used:
  - The `cast` function with parameters "double" and "uint8".
  - The `SVD` function for singular value decomposition.
  - Matrix reduction with the new dimensions.
  - Calculated the final matrix using the formula: `new_X = U * S * V'`.

## TASK 2:
- I used:
  - The `cast` function with parameters "double" and "uint8".
  - The `mean` function with dimension 2 to compute the algebraic mean of each row and subtracted it from the initial matrix to normalize it.
  - Constructed matrix Z (transpose of the initial matrix / square root of n-1).
  - The `SVD` function for singular value decomposition.
  - Calculated the pcs-dimensional principal component space: `W = V(:, 1:pcs)`.
  - Calculated the projection of the initial matrix into the principal component space: `Y = W' * photo`.
  - Calculated the final matrix.

## TASK 3:
- I used:
  - The `cast` function with parameters "double" and "uint8".
  - The `mean` function with dimension 2 to compute the algebraic mean of each row and subtracted it from the initial matrix to normalize it.
  - Constructed the covariance matrix (initial matrix * transpose of the initial matrix / n-1).
  - The `eig` function to compute the eigenvectors and eigenvalues of the covariance matrix.
  - The `sort` function applied to the diagonal of matrix S, containing eigenvalues, with the parameter 'descend' to order them in descending order and obtain an index to retain their order for application to vectors.
  - Calculated the pcs-dimensional principal component space: `W = V(:, 1:pcs)`.
  - Calculated the projection of the initial matrix into the principal component space: `Y = W' * photo`.
  - Calculated the final matrix.

## TASK 4 - VISUALE_IMAGE:
- I used:
  - The `reshape` function to transform a number line from the training matrix into a 28x28 matrix (pixel size of an image).
  - The `cast` function with the parameter "uint8".

## PREPARE_DATA:
- I used:
  - The `load` function to store the data in `d` from the table provided as an argument.
  - The `d.trainX/Y` function (X to store rows from the training image table, Y to store values from the label vector) => example: `train_mat = d.trainX(1:no_train_images, :)`.

## PREPARE_PHOTO:
- I used:
  - Inverted the image pixels knowing they can go up to 255 color values.
  - The `reshape` function to transform the image into a 1x784 line vector.

## MAGIC_WITH_PCA:
- The `MAGIC_WITH_PCA` function is similar to implementing Task 3.
- I used:
  - The `cast` function with the parameter "double".
  - The `mean` function with dimension `q` to compute the algebraic mean of each column and subtracted it from the initial matrix to normalize it.
  - Constructed the covariance matrix (transpose of the initial matrix * initial matrix / m-1).
  - The `eig` function to compute the eigenvectors and eigenvalues of the covariance matrix.
  - The `sort` function applied to the diagonal of matrix S, containing eigenvalues, with the parameter 'descend' to order them in descending order and obtain an index to retain their order for application to vectors.
  - Calculated the pcs-dimensional principal component space: `Vk = V(:, 1:pcs)`.
  - Calculated the projection of the initial matrix into the principal component space: `Y = train_mat * Vk`.
  - Calculated the final matrix.

## KNN:
- I used:
  - The `norm` function to calculate the Euclidean distance between each row of matrix Y and the test vector provided as an argument.
  - The `sort` function applied to the diagonal of matrix S, containing eigenvalues, ordering them in ascending order to obtain an index to retain their order for application to vectors.
  - The `median` function which calculates the median value of the knl vector.

## CLASSIFYIMAGE:
- I used:
  - The `cast` function with the parameter "uint8".
  - The `magic_with_pca` function.
  - The `KNN` function with k = 5.

