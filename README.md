# Predikcia odozvy zákazníkov na marketingové kampane

**Bakalárska práca** | Technická univerzita v Košiciach, Fakulta elektrotechniky a informatiky  
**Autor:** Tomáš Kerekeš  
**Školiteľ:** Ing. Anna Biceková, PhD.  
**Rok:** 2026

---

## O práci

Práca sa zaoberá predikciou odozvy zákazníkov na priame marketingové kampane pomocou metód strojového učenia. Na verejne dostupnom retailovom datasete bola realizovaná séria ôsmich experimentov pokrývajúcich štyri klasifikačné algoritmy, techniky riešenia nevyváženosti tried a optimalizáciu rozhodovacieho prahu. Primárnou optimalizačnou metrikou je **F2-skóre**, ktoré kladie dvojnásobnú váhu na úplnosť (recall) oproti presnosti (precision).

---

## Štruktúra repozitára

```
├── Experiments3.ipynb      # Hlavný notebook – všetky experimenty
├── marketing_campaign.csv  # Vstupný dataset (Kaggle)
└── README.md
```

---

## Experimenty

| # | Popis |
|---|-------|
| 1 | Baseline modely bez riešenia nevyváženosti (Logistická regresia, Rozhodovací strom) |
| 2 | Vyváženie tried pomocou `class_weight="balanced"` + StandardScaler |
| 3 | Ensemble modely – Random Forest a AdaBoost (baseline) |
| 4 | Nadvzorkovanie pomocou SMOTE |
| 5 | Nadvzorkovanie pomocou ADASYN (všetky 4 modely) |
| 6 | ROC krivky, Precision-Recall krivky, optimalizácia rozhodovacieho prahu |
| 7 | Hyperparameter tuning – Random Forest (RandomizedSearchCV) + analýza scenárov thresholdov |
| 8 | Hyperparameter tuning – všetky 4 modely, záverečné porovnanie |

---

## Použité technológie

- **Python** (conda environment)
- **pandas**, **numpy** – spracovanie dát
- **scikit-learn** – klasifikačné modely, krížová validácia, metriky
- **imbalanced-learn** – SMOTE, ADASYN
- **matplotlib**, **seaborn** – vizualizácia

---

## Inštalácia závislostí

```bash
pip install pandas numpy scikit-learn imbalanced-learn matplotlib seaborn
```

Alebo pomocou conda:

```bash
conda install pandas numpy scikit-learn matplotlib seaborn
pip install imbalanced-learn
```

---

## Spustenie

1. Stiahni alebo naklonuj repozitár
2. Uisti sa, že súbor `marketing_campaign.csv` je v rovnakom adresári ako notebook
3. Otvor `Experiments3.ipynb` v Jupyter Notebook alebo JupyterLab
4. Spusti bunky postupne od začiatku (`Run All` alebo po jednej)

> **Poznámka:** Experimenty na seba nadväzujú – premenné (napr. `X_train_res`, `y_train_res`) sa prenášajú medzi sekciami. Odporúča sa spúšťať notebook vždy od začiatku.

---

## Dataset

**marketing_campaign.csv** – verejne dostupný dataset zo stránky [Kaggle](https://www.kaggle.com/).  
Obsahuje demografické údaje, nákupné správanie a históriu odozvy zákazníkov retailovej spoločnosti.  
Cieľová premenná: `Response` (1 = zákazník reagoval na kampaň, 0 = nereagoval).  
Počet záznamov: 2 240 | Pomer tried: 70,2 % (0) vs. 29,8 % (1).

---

## Kľúčové výsledky

Najlepšie F2-skóre dosiahol **vyladený Random Forest s F2-optimálnym prahom 0.27** (F2 = 0.718, Recall = 0.851, AUC = 0.882). Pre scenáre s požiadavkou na vyššiu presnosť bol identifikovaný balanced threshold (prah 0.35) zachytávajúci 70 % reagujúcich zákazníkov pri presnosti 0.50. Z pohľadu interpretovateľnosti je alternatívou vyladená logistická regresia s najvyšším AUC (0.893).
