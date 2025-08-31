#pre-processing  #functions 

1. [[Regression workflow template]]
2. [[Classification workflow template]]

[[Custom Transformers]]

```
from sklearn.pipeline import Pipeline

num_pipeline = Pipeline([('imputer', SimpleImputer(strategy='median')),
					  ('custom_transformer', CustomTransformer()),
					  ('std_scaler', StandardScaler())		
						])
```

* We can have two pipelines:
	* 1 for numeric attributes
	* 1 for categorical attributes
* Then we can combine them
* We can also have multiple pipelines for individual variables as well and then combine them.


```
cat_pipeline = Pipeline([('ohe', OneHotEncoder())])
```

Pipelines can be combined using ColumnTransformer:

```
from sklearn.compose import ColumnTransformer

full_pipeline = ColumnTransformer([
									('num', num_pipeline, num_attributes),
									('cat', cat_pipeline, cat_attributes)
])

full_prepared_dataset = full_pipeline.fit_transform(training_df)
```

attributes here can be column names of indices.

 Other options:
 * Custom transformer
 * FeatureUnion class