#pre-processing #functions

Approaches:
1. generate permutations and select sets from it.
2. sklearn.model_selection.train_test_split

If the dataset is unbalanced, stratification is very important during training-test set division.

**For splitting and ensuring proper representation of any numerical variable, it can be bucketed before splitting.** We can have a seggregation based on the distribution of the column.

* We can use pd.cut / pd.qcut to stratify

`pd.cut(housing['median_income'], bins=[0, 1.5, 3, 4.5, 6, np.inf], labels=[1,2,3,4,5])`

Then we can use sklearn.model_selection.StratifiedShuffleSplit to ensure that this variable is adequately represented in test set compared to full dataset.









