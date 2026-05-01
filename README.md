# Darmmikrobiom & Krankheitsvorhersage

Abschlussprojekt: Klassifikation von Krankheiten anhand des Darmmikrobioms.

**Team:** Amine El Marouani, Slavica, Sahar

---

## Projektstruktur

```
Darmmikrobiom/
├── Notebook/
│   └── Data_Analysis_final.ipynb
├── Data/
│   ├── AGP/
│   │   ├── AGP_count.csv
│   │   ├── AGP_meta.csv
│   │   ├── AGP_meta_clean.csv
│   │   └── AGP_tax.csv
│   ├── MGS/
│   │   ├── sampleID.csv
│   │   └── vect_atlas.csv
│   └── Output/
│       ├── evaluation_xgboost.png
│       ├── confusion_matrix_multiclass.png
│       ├── confusion_matrix_geography.png
│       ├── shap_beeswarm.png
│       ├── shap_importance.png
│       ├── feature_importance.png
│       ├── diversity_features.png
│       └── log_transformation.png
└── Darm Gesundheit.pbix
```

---

## Datensätze

### AGP — American Gut Project (Teil 1: EDA)
| | |
|---|---|
| Proben | 698 |
| Features | ~52.000 ASVs |
| Methode | 16S-rRNA-Sequenzierung |
| Analyse | Power BI |

### MGS-Atlas (Teil 2: Machine Learning)
| | |
|---|---|
| Proben | 6.014 |
| Features | 1.990 Metagenomic Species |
| Methode | Shotgun-Metagenomik |
| Länder | 22 |
| Erkrankungen | 14 (CRC, T2D, ACVD, LC u.a.) |
| Klassenbalance | 54 % gesund / 46 % krank |

---

## ML-Pipeline

**Zielvariable:** binär — `healthy = 0`, alle Erkrankungen = `1`

**Vorverarbeitung:**
- log1p-Transformation: `np.log1p(X * 1e6)`
- Diversity-Features: Shannon, Simpson, Observed MGS, Pielou Evenness

**Modell:** XGBoost auf allen 1.990 Features

**Ergebnisse:**
| Metrik | Wert |
|---|---|
| ROC-AUC (binär) | **0,864** |

---

## Setup

```bash
source .venv313/bin/activate
jupyter lab Notebook/Data_Analysis_final.ipynb
```

**Stack:** Python 3.13 · NumPy · Pandas · Scikit-learn · XGBoost · SHAP · Power BI
