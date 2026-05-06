# StellarDecoders

基于 XGBoost 与恒星子类分组训练的恒星大气参数预测与聚类分析框架。

StellarDecoders 面向 LAMOST 恒星光谱数据，结合机器学习回归与无监督聚类方法，对恒星的：

- Effective Temperature (`Teff`)
- Surface Gravity (`log g`)
- Metallicity (`[M/H]`)

等关键大气参数进行建模与分析。

---

# Overview

不同恒星子类在：

- 光谱结构
- 物理参数分布
- 演化特征

上存在明显差异。

因此，StellarDecoders 采用：

## Subclass Group Training

即：

- 按恒星子类划分数据
- 对每一类恒星分别训练模型
- 独立进行预测与评估

以降低数据异质性带来的误差，提高模型在特定恒星类别上的拟合能力与泛化性能。

---

# Features

## Atmospheric Parameter Prediction

基于 XGBoost 的恒星大气参数预测：

- `Teff`
- `log g`
- `[M/H]`

---

## Stellar Clustering Analysis

项目同时包含基于物理参数空间的恒星聚类分析。

当前实现包括：

- DBSCAN 密度聚类
- 三维参数空间可视化
- 恒星参数分布分析

聚类特征包括：

- `teff`
- `GMAG`
- `logg`

用于研究不同恒星群体在参数空间中的结构分布。

---

# Method

## Data Preprocessing

对原始星表数据进行：

- 缺失值过滤
- 物理范围筛选
- 参数标准化

例如：

```python
df = df[(df['teff'] > 2500) & (df['teff'] < 50000)]
```

用于保证数据符合合理恒星物理范围。

---

## Standardization

采用 `StandardScaler` 进行标准化：

```python
scaler = StandardScaler()
X_scaled = scaler.fit_transform(df)
```

避免不同量纲对聚类与回归造成影响。

---

## DBSCAN Clustering

聚类部分采用：

```python
DBSCAN(eps=0.3, min_samples=300)
```

实现恒星参数空间中的密度聚类分析。

该方法能够：

- 自动识别恒星群体结构
- 检测离群点
- 避免传统 KMeans 对簇数量的依赖

---

## Visualization

项目支持：

- 二维 Teff-GMAG 聚类分布图
- 三维 Teff-GMAG-logg 参数空间可视化

用于分析：

- 恒星主序分布
- 参数空间密度结构
- 聚类边界与异常样本

---

# Dataset

主要使用：

## LAMOST Stellar Catalogues

包括：

- LAMOST LRS Catalogue of gM, dM, and sdM Stars
- LAMOST LRS Stellar Parameter Catalogue of A/F/G/K Stars

数据划分：

- 80% Training Set
- 20% Testing Set

---

# Results

实验结果表明：

- 子类分组训练能够显著提升 `log g` 预测精度
- XGBoost 相较传统 MLP 方法具有更强泛化能力
- DBSCAN 能够有效识别恒星参数空间中的结构分布
- 模型在 A/F/G/K 星型上具有良好迁移性

---

# Repository Structure

```text
StellarDecoders/
│
├── StellarDecoders.ipynb     # Main notebook
├── data/                     # Stellar catalogues
├── results/                  # Figures and outputs
├── README.md
└── requirements.txt
```

---

# Usage

## Clone Repository

```bash
git clone https://github.com/yourname/StellarDecoders.git
cd StellarDecoders
```

---

## Install Dependencies

```bash
pip install -r requirements.txt
```

---

## Run Notebook

```bash
jupyter notebook StellarDecoders.ipynb
```

---

# Example Workflow

```python
# 数据标准化
X_scaled, scaler = standardize_data(df_features)

# DBSCAN聚类
dbscan_labels = perform_clustering(X_scaled)

# 聚类可视化
plot_cluster_results(df_features, X_scaled, dbscan_labels)
```

---

# Dependencies

```text
numpy
pandas
matplotlib
scikit-learn
xgboost
jupyter
```

# Acknowledgement

- LAMOST Survey
- XGBoost
- Scikit-learn
- Stellar spectroscopy research community

---

## StellarDecoders

Decoding stellar atmospheres through subclass-aware machine learning.
