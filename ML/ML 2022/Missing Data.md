#ml [[Preprocessing]]


1. Dropping column / row
2. Imputation 
	1. Simple Imputer



### Imputation

#### Simple Imputer [[sklearn]]
```
from sklearn.imputer import SimpleImputer
imputer = SimpleImputer(missing_values=np.nan, strategy='mean')
imputer.fit_transform(X)
```



Numeric Variables:

1. Fill mean value
2. Fill median value
3. Back fill
4. Front fill

Categorical Variables:

1. Fill most frequent value
2. Back fill
3. Front fill
