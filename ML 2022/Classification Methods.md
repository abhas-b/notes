#major 

[[Classification workflow template]]

1. [[Logistic Regression]]
2. [[Stochastic Gradient Descent]]
3. [[SVM - beta]]
4. [[Decision Trees]]
5. [[Random Forest (Bagging)]]
6. [[KNN]]
7. [[Multiclass Classification]]


* After training, we need to evaluate errors.
	* Confusion matrix can be a useful tool.
	* Confusion matrix should be normalized before proceeding further with error analysis, to adjust for the difference in number of samples per class.
	* Fill the diagonals with zeros, to retain only the errors

```
conf_mx = confusion_matrix(y_train, y_train_pred)
row_sums = conf_mx.sum(axis=1, keepdims=True)
norm_conf_mx = conf_mx / row_sums

np.fill_diagonal(norm_conf_mx, 0)
plt.matshow(norm_conf_mx, cmap=plt.cm.gray)
```