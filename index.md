# Trading Machine - Random Forest

A idéia principla é testar indicadores técnicos para a explicação de retornos da ação PETR4, para isso foi usado o modelo de Random Forest e como imputs alguns indicadores técnicos tradicionáis, como:

* RSI
* Stochastic
* ROC
* Chaikin Money Flow
* Force Index
* KAMA

Além dos retornos passados e a % de quanto um fechamento ficou da máxima e mínima do dia desde 2010


### Bibliotecas utilizadas:


```markdown
import pandas as pd
import numpy as np
import ta  ### biblioteca para analise de indicadores técnicos
from sklearn.tree import DecisionTreeClassifier
from sklearn.model_selection import train_test_split
from sklearn.metrics import accuracy_score
from sklearn.metrics import classification_report
from sklearn.preprocessing import StandardScaler
from sklearn.pipeline import Pipeline
from sklearn.model_selection import GridSearchCV
import matplotlib.pyplot as plt
```

For more details see [Basic writing and formatting syntax](https://docs.github.com/en/github/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/Jhonattanln/Decision_Tree/settings/pages). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://docs.github.com/categories/github-pages-basics/) or [contact support](https://support.github.com/contact) and we’ll help you sort it out.
