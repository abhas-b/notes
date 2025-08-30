#pre-processing 

A custom transformer can also be added to a pipeline for swift processing of test data.

**One Hot Encoding using ColumnTransformer**:

from sklearn.compose import ColumnTransformer

ct = ColumnTransformer(transformers=[('encoder', OneHotEncoder(), [0])],
										remainder='passthrough')


We need three methods in a custom transformer:
* fit
* transform
* fit_transform -- can be obtained by using TransformerMixin class

* for enabling hyperparameter tuning, add BaseEstimator class.


```
class CombinedAttributesAdder(BaseEstimator, TransformerMixin):
		def __init__(self, add_bedrooms_per_room = True): # no *args or **kargs
			self.add_bedrooms_per_room = add_bedrooms_per_room
		def fit(self, X, y=None):
			return self # nothing else to do
		def transform(self, X):
			rooms_per_household = X[:, rooms_ix] / X[:, households_ix]
			population_per_household = X[:, population_ix] / X[:, households_ix]
			if self.add_bedrooms_per_room:
				bedrooms_per_room = X[:, bedrooms_ix] / X[:, rooms_ix]
				return np.c_[X, rooms_per_household, population_per_household,
						bedrooms_per_room]
attr_adder = CombinedAttributesAdder(add_bedrooms_per_room=False)
housing_extra_attribs = attr_adder.transform(housing.values)
```


