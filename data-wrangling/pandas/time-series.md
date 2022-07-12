# Pandas Time-Series Operations

## Normalizing a TS dataframe

```python
google = pd.read_csv('google.csv', parse_dates ['date'], index_col='date')
google.head(3)
```

```
date        price

2010-01-04  313.06
2010-01-05  311.68
2010-01-06  303.83
```

### take the frst value

```python
first_price = google.price.iloc[0]  # int-based selection
```

get a normalized DataFrame ->

```python
normalized = google.price.div(first_price).mul(100)
```

 - `.sub(..., axis=0)` : Subtract a Series from each DataFrame column by aligning indexes
