# SULTA_JAN_ML_PROJECT
Semestrální projekt: Predikce odchodu zákazníků (churn) telekomunikační společnosti pomocí strojového učení.

## Autor

Jan Šulta

## Dataset

Telco Customer Churn Dataset (IBM Sample Data)  
Zdroj: [Kaggle](https://www.kaggle.com/datasets/blastchar/telco-customer-churn)  
Rozsah: 7 043 zákazníků, 21 proměnných

## Struktura repozitáře
```
SULTA_JAN_ML_PROJECT/
|- README.md
|- dataprocessing.ipynb          # zpracování dat a split
|- dataprocessing.html           # HTML export notebooku
|- benchmark.ipynb               # naivní baseline a ML benchmark
|- benchmark.html                # HTML export notebooku
|- data/
|  |- Telco_Customer_Churn.csv   # originální dataset
|  |- pre-processed/             # splity po čištění, před encodingem a scalingem
|  \- processed/                 # splity po kompletní pipeline (encoding, scaling)
```

## Popis souborů

### dataprocessing.ipynb

Notebook obsahuje kompletní datovou pipeline:

1. Navázání na DÚ1 (task framing)
2. Načtení dat a základní profiling
3. Popis dat a explorativní kontrola
4. Leakage audit všech 21 proměnných
5. Čištění dat před splitem (odstranění 11 vadných řádků, konverze typů, drop customerID)
6. Stratifikovaný split 80/15/5 s reprodukovatelným seedem (random_state = 42)
7. Preprocessing pipeline (encoding, scaling — fit výhradně na train sadě)
8. Shrnutí a další kroky

### benchmark.ipynb

Notebook obsahuje dva benchmarky vyhodnocené na validační sadě:

1. **Naivní baseline** — pravidlo: Contract = Month-to-month AND tenure ≤ 12
2. **ML benchmark** — logistická regrese s class_weight="balanced"

Metriky: F1-score, ROC-AUC, PR-AUC, confusion matrix, classification report.

## Metodické poznámky

- Testovací sada nebyla použita pro ladění ani výběr modelu
- Všechny fitované transformace (OneHotEncoder, StandardScaler) byly naučeny pouze na trénovací sadě
- Deterministické kroky čištění (konverze typů, odstranění vadných řádků) provedeny před splitem
- Reprodukovatelnost zajištěna pomocí random_state = 42

## Spuštění

1. Otevřít `dataprocessing.ipynb` → Kernel → Restart & Run All
2. Otevřít `benchmark.ipynb` → Kernel → Restart & Run All

Notebooky jsou nezávislé — benchmark.ipynb načítá uložené CSV z data/pre-processed/ a data/processed/.

## Technologie

- Python 3.x
- pandas, numpy, matplotlib, seaborn
- scikit-learn (train_test_split, LogisticRegression, StandardScaler, OneHotEncoder)
