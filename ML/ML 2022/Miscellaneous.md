#ml [[ML Concepts]]

* A high learning rate leads to fast adaptive system.
* A low learning rate makes a system more robust to noise/outliers.
* This is particularly more critical in online learning systems.
* Data issues:
	* Quantity
	* Quality
		* Outliers
		* Missing data
		* Redundant features
		* Irrelevent features
	* If the training set is too noisy, a complex algo will start detecting patterns in the noise instead of the data.
	* Solutions for overfitting:
		* [[Regularization]]
		* Reducing model complexity
		* Gather more training data
		* Remove redundant features
		* Dimensionality Reduction
		* De-noise data
	* Solutions for underfitting:
		* More complex model
		* Lower regularization
		* Feature engineering (add features)
	* Validation:
		* Split the training set in two parts:
			* Training set
			* Validation set
		* Train on training set, test on validation set to perform hyperparameter tuning.
		* Then re-train on full training set
		* Then test on test set
	* An alternate is cross validation
		* [[Cross Validation]]
* Try to work using pipelines. This lets you manage the system better.
	* [[Pipelining]]
* Model results can be inspected to understand errors better:
	* [[Feature Inference]]
* Final model evaluation:
	* evaluate on the final test set.
	* When point estimate is not adequate, and we want confidence interval on a test set, we can use a t-test from scipy:
		* [[Confidence interval for test set]]
		* 





[[GZIP utility function]]
