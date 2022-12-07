## Plan - test

- DONE import expenses
- compute static monthly avg home meal price = food / N where N = ( 30 * 3 - [takeaway+resto above 4 eur treshold])
- Treshold: > or <= 4 EUR
- plot takeaway and resto expenses to see where to draw the line

Further:

- compute home meal price by resizible rolling window - from quarter to 1 week
- plot a seaborn graph showing dynamics: is the price increased? by how much?








```python
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt
import numpy as np
```


```python
filepath = "./input/MoneyOK.csv"
expenses = pd.read_csv(filepath, sep="\t")
expenses.shape
```


