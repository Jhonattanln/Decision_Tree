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

### Base de dados:

A base de dados utilizada foi provida pela plataforma Economatica e comtém:

* Quantidade de negócios
* Volume
* Fechamento
* Abertura
* Mínima
* Máxima
* Médio

```markdown
df = pd.read_excel('economatica.xlsx', parse_dates=True, index_col=0, skiprows=3)
df.rename(columns={'Volume$':'Volume'}, inplace=True)
```

### Features:

A biblioteca ta foi utilizada para o cálculo dos indicadores:


```markdown
df['Retornos'] = df.Fechamento.pct_change() ## retornos
df['Kama'] = ta.momentum.KAMAIndicator(close=df.Fechamento, window=21).kama() ## indicador Kama
df['ROC'] = ta.momentum.ROCIndicator(close=df.Fechamento, window=12).roc()
df['RSI'] = ta.momentum.RSIIndicator(close=df.Fechamento, window=14).rsi()
df['Stoch'] = ta.momentum.StochasticOscillator(close=df.Fechamento, high=df.Máximo, low=df.Mínimo, 
                                                window=14, smooth_window=3).stoch()
df['Chaikin_money'] = ta.volume.ChaikinMoneyFlowIndicator(high=df.Máximo, low=df.Mínimo, close=df.Fechamento, 
                                                          volume=df.Volume, window=20).chaikin_money_flow()
df['Force_index'] = ta.volume.ForceIndexIndicator(close=df.Fechamento, volume=df.Volume, window=13).force_index() 
df['Normal'] = (df.Fechamento - df.Mínimo) / (df.Máximo - df.Mínimo) ## mede a % de quanto um dia fechou da máxima ou mínima
```

### Tratando dados

Houve a necessidade da limpeza de dados faltantes quando calculados os indicadores, como também a criação de targets para o modelo de classificação supervisionada

```markdown
df = df.dropna() ## excluindo valores nulos
X = df[[
        'Q Negs', 'Q Títs', 'Volume', 'Fechamento', 'Abertura', 'Mínimo', 
        'Máximo', 'Médio', 'Kama', 'ROC', 'RSI', 'Stoch', 'Chaikin_money', 
        'Force_index', 'Normal']] ## criando as features
y = np.where(df['Fechamento'].shift(-1) > df['Fechamento'], 1, -1) ## criando target
```

Através _train_test_split_ foi criado a base de treinamento e teste

```markdown
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, shuffle=False)
```



For more details see [Basic writing and formatting syntax](https://docs.github.com/en/github/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/Jhonattanln/Decision_Tree/settings/pages). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://docs.github.com/categories/github-pages-basics/) or [contact support](https://support.github.com/contact) and we’ll help you sort it out.
