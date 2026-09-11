# 技术细节补全指南

> 拒绝黑箱表述，每个模型落地到具体参数、步骤、依据。本文档提供C题常用方法的技术细节规范表述模板。

---

## 通用原则

不说"用XX方法做了XX"，而要说清楚：
1. **为什么选这个方法**（选型理由）
2. **具体怎么设置的**（参数全部明确）
3. **用什么工具实现的**（库/软件/版本）
4. **结果怎么评估的**（评价指标）

> 参照标准：读者看完你写的技术细节，能复现你的结果。

---

## 一、评价类方法

### 1.1 熵权法 + TOPSIS

**完整表述模板：**

> 本文采用熵权法确定各指标的客观权重，其基本原理是根据指标数据的离散程度赋权，差异越大的指标包含的信息量越多，权重越大。具体步骤如下：
> （1）构建评价矩阵 $X = (x_{ij})_{m \times n}$，其中 $m$ 为评价对象数，$n$ 为评价指标数；
> （2）指标正向化：对成本型指标取倒数，对适度型指标转化为正向指标；
> （3）标准化处理：$p_{ij} = x_{ij} / \sum_{i=1}^{m} x_{ij}$，消除量纲影响；
> （4）计算熵值：$e_j = -k \sum_{i=1}^{m} p_{ij} \ln p_{ij}$，其中 $k = 1/\ln m$；
> （5）计算权重：$w_j = (1 - e_j) / \sum_{j=1}^{n} (1 - e_j)$。
>
> 在此基础上，采用TOPSIS方法进行综合评价。该方法通过计算各评价对象与正理想解和负理想解的相对贴近度进行排序，贴近度越大表示方案越优。具体步骤为：
> （1）构造加权规范化矩阵 $V = (v_{ij})_{m \times n}$，其中 $v_{ij} = w_j \cdot x_{ij}'$，$x_{ij}'$ 为标准化后的矩阵；
> （2）确定正理想解 $V^+ = \{\max v_{ij} | j \in J^+, \min v_{ij} | j \in J^-\}$ 和负理想解 $V^- = \{\min v_{ij} | j \in J^+, \max v_{ij} | j \in J^-\}$，其中 $J^+$ 为效益型指标集，$J^-$ 为成本型指标集；
> （3）计算各方案到正理想解的距离 $D_i^+ = \sqrt{\sum_{j=1}^{n} (v_{ij} - v_j^+)^2}$ 和到负理想解的距离 $D_i^- = \sqrt{\sum_{j=1}^{n} (v_{ij} - v_j^-)^2}$；
> （4）计算相对贴近度 $C_i = D_i^- / (D_i^+ + D_i^-)$，按 $C_i$ 从大到小排序。

---

## 二、回归分析类

### 2.1 多元线性回归

**完整表述模板：**

> 本文采用多元线性回归模型分析XX与XX之间的关系。模型形式为：
> $$ y = \beta_0 + \beta_1 x_1 + \beta_2 x_2 + \cdots + \beta_p x_p + \varepsilon $$
> 其中 $y$ 为因变量，$x_1, x_2, \cdots, x_p$ 为自变量，$\beta_0, \beta_1, \cdots, \beta_p$ 为待估参数，$\varepsilon$ 为随机误差项，假设 $\varepsilon \sim N(0, \sigma^2)$。
>
> 采用普通最小二乘法（OLS）估计参数，即使残差平方和最小：
> $$ \min \sum_{i=1}^{n} (y_i - \hat{y}_i)^2 $$
>
> **模型诊断：** 为验证模型适用性，进行以下检验：
> （1）**拟合优度检验**：调整 $R^2 = $ XX，表明模型解释了XX%的因变量变异；
> （2）**F检验**：$F = $ XX，$p < 0.001$，回归方程整体显著；
> （3）**t检验**：各自变量的t值与p值见表X，其中XX变量在0.05水平上显著；
> （4）**正态性检验**：对残差进行Shapiro-Wilk检验，$W = $ XX，$p = $ XX > 0.05，不拒绝正态性假设；
> （5）**多重共线性检验**：所有变量的VIF值均小于XX，不存在严重多重共线性；
> （6）**异方差检验**：Breusch-Pagan检验 $\chi^2 = $ XX，$p = $ XX > 0.05，不存在显著异方差。

### 2.2 线性混合效应模型（LMM）

**完整表述模板：**

> 考虑到数据中同一受试者有多次重复测量，存在层次结构，普通线性回归的独立性假设不成立，因此本文采用线性混合效应模型（Linear Mixed-effects Model, LMM）进行建模。该模型同时包含固定效应和随机效应，能够有效刻画个体间的异质性。
>
> 模型形式为：
> $$ \mathbf{y}_i = \mathbf{X}_i \boldsymbol{\beta} + \mathbf{Z}_i \mathbf{b}_i + \boldsymbol{\varepsilon}_i $$
> 其中 $\mathbf{y}_i$ 为第 $i$ 个受试者的观测向量，$\mathbf{X}_i$ 为固定效应设计矩阵，$\boldsymbol{\beta}$ 为固定效应参数向量，$\mathbf{Z}_i$ 为随机效应设计矩阵，$\mathbf{b}_i$ 为随机效应向量，假设 $\mathbf{b}_i \sim N(\mathbf{0}, \mathbf{D})$，$\boldsymbol{\varepsilon}_i$ 为残差向量，假设 $\boldsymbol{\varepsilon}_i \sim N(\mathbf{0}, \sigma^2 \mathbf{I})$。
>
> 本文采用限制性最大似然估计（REML）估计模型参数。随机效应结构为随机截距 + 随机斜率（以孕周为斜率变量），即允许每个受试者有不同的基线水平和变化速率。
>
> **模型比较**：为验证随机效应的必要性，采用似然比检验（Likelihood Ratio Test, LRT）比较空模型、随机截距模型和随机截距+斜率模型。结果显示（见表X），加入随机斜率后模型拟合显著改善（$\chi^2 = $ XX, $p < 0.001$），因此最终选择随机截距+斜率模型。
>
> **组内相关系数（ICC）**：通过空模型计算得到ICC = XX，表明XX%的变异来源于个体间差异，说明使用混合效应模型是必要的。

---

## 三、优化类方法

### 3.1 线性规划 / 整数规划

**完整表述模板：**

> 本文建立XX优化模型如下：
>
> **决策变量**：定义 $x_{ij}$ 为XX（明确含义、取值范围）。
>
> **目标函数**：
> $$ \max / \min \quad Z = \sum_{i=1}^{m} \sum_{j=1}^{n} c_{ij} x_{ij} $$
> 其中 $c_{ij}$ 为XX系数。
>
> **约束条件**：
> （1）XX约束：$\sum_{j=1}^{n} a_{ij} x_{ij} \leq b_i, \quad i = 1, 2, \cdots, m$
> （2）XX约束：...
> （3）非负/整数约束：$x_{ij} \geq 0$（或 $x_{ij} \in \{0, 1\}$）
>
> **求解工具**：采用Python的PuLP/Gurobi库进行求解，求解器为XXX，全局最优解在X秒内收敛。

### 3.2 遗传算法

**完整表述模板：**

> 由于本问题的决策变量为XX，目标函数具有XX特性（非线性/高维/组合优化），传统精确算法难以在有限时间内求解，因此采用遗传算法（Genetic Algorithm, GA）进行求解。遗传算法是一种模拟自然选择和遗传变异的启发式优化算法，具有全局搜索能力强、不依赖梯度信息的优势。
>
> **算法设置**：
> - 编码方式：实数编码（或二进制编码），染色体长度为XX
> - 种群规模：$N = 200$
> - 最大迭代次数：$T_{max} = 500$
> - 选择策略：锦标赛选择（锦标赛规模为5）
> - 交叉方式：均匀交叉（或算术交叉/BLEND-α交叉，α=0.5）
> - 交叉概率：$p_c = 0.8$
> - 变异方式：高斯变异（变异标准差为0.1）
> - 变异概率：$p_m = 0.05$
> - 精英保留：每代保留前5个最优个体直接进入下一代
> - 终止条件：达到最大迭代次数，或连续50代最优值无改进
>
> **实现工具**：基于Python的DEAP库（或scikit-opt库）实现，设置随机种子为42以保证结果可复现。为降低随机性影响，独立运行30次取最优解。
>
> **收敛验证**：算法迭代曲线见图X，在第XX代左右收敛，最终目标函数值为XX。

---

## 四、机器学习类

### 4.1 随机森林

**完整表述模板：**

> 本文采用随机森林（Random Forest）回归模型进行XX预测。随机森林是一种集成学习方法，通过构建多棵决策树并对其结果进行平均，有效降低了单棵决策树的过拟合风险，同时保持了较好的预测精度。
>
> **模型参数设置**：
> - 决策树数量：n_estimators = 120
> - 最大深度：max_depth = 10
> - 最小样本分裂数：min_samples_split = 5
> - 最小叶节点样本数：min_samples_leaf = 2
> - 最大特征数：max_features = "sqrt"
> - 随机种子：random_state = 42
>
> **数据集划分**：按7:3比例随机划分为训练集和测试集，采用分层抽样保证分布一致性。
>
> **优化目标**：以均方误差（MSE）为分裂准则。
>
> **评价指标**：在测试集上评估模型性能，指标包括RMSE = XX、MAE = XX、$R^2$ = XX。
>
> **实现工具**：基于Python的scikit-learn库（版本1.2.0）实现。

### 4.2 LightGBM

**完整表述模板：**

> 本文采用LightGBM梯度提升树模型进行XX分类/回归。LightGBM基于直方图算法和带深度限制的Leaf-wise叶子生长策略，具有训练速度快、内存占用低、精度高的特点。
>
> **模型参数**：
> - boosting_type: "gbdt"
> - num_leaves: 63
> - learning_rate: 0.05
> - n_estimators: 500
> - max_depth: 8
> - min_child_samples: 20
> - subsample: 0.8
> - colsample_bytree: 0.8
> - reg_alpha: 0.1
> - reg_lambda: 0.1
> - random_state: 42
>
> **类别不平衡处理**：由于数据集中XX类与XX类比例约为1:XX，存在类别不平衡问题，采用SMOTE（Synthetic Minority Oversampling Technique）方法对少数类进行过采样，采样后类别比例约为1:1。
>
> **验证策略**：采用5折交叉验证，以accuracy/F1-score/AUC为评价指标。
>
> **超参优化**：使用Optuna框架进行超参数优化，采样器为TPE（Tree-structured Parzen Estimator），共进行100次试验，采用中位数剪枝（Median Pruner）提前终止表现不佳的试验。
>
> **实现工具**：基于Python的lightgbm库（版本3.3.5）和optuna库（版本3.1.0）实现。

### 4.3 XGBoost + SHAP可解释性

**完整表述模板：**

> 为提高模型的可解释性，本文采用SHAP（SHapley Additive exPlanations）方法对XGBoost模型的预测结果进行解释。SHAP基于博弈论中的Shapley值，能够公平地分配每个特征对预测结果的贡献度。
>
> **XGBoost模型参数**：
> - n_estimators: 300
> - max_depth: 6
> - learning_rate: 0.1
> - subsample: 0.8
> - colsample_bytree: 0.8
> - reg_alpha: 0.01
> - reg_lambda: 1
> - objective: "reg:squarederror"（回归）/ "binary:logistic"（二分类）
> - random_state: 42
>
> **SHAP分析内容**：
> （1）特征重要性排序（全局）：基于SHAP值的绝对值均值排序；
> （2）SHAP摘要图：展示各特征对预测值的影响方向和大小；
> （3）SHAP力图：单个样本的特征贡献分解；
> （4）依赖图：特定特征值与SHAP值的关系。
>
> **实现工具**：xgboost库 + shap库（版本0.41.0）。

---

## 五、时间序列类

### 5.1 ARIMA

**完整表述模板：**

> 本文采用ARIMA（AutoRegressive Integrated Moving Average）模型对XX时间序列进行预测。ARIMA模型由自回归（AR）、差分（I）和移动平均（MA）三部分组成，适用于平稳时间序列的短期预测。
>
> **建模步骤**：
> （1）**平稳性检验**：采用ADF（Augmented Dickey-Fuller）检验，原序列ADF统计量 = XX，p = XX，（不）拒绝单位根假设，因此需要进行d阶差分使序列平稳；
> （2）**差分阶数确定**：经过d = XX阶差分后，序列通过ADF检验（p < 0.05），确定I = XX；
> （3）**定阶**：通过ACF图和PACF图初步确定p和q的范围，再结合AIC和BIC信息准则选择最优模型；最终确定模型为ARIMA(p, d, q) = ARIMA(XX, XX, XX)；
> （4）**参数估计**：采用极大似然估计；
> （5）**模型诊断**：对残差进行白噪声检验（Ljung-Box检验），Q统计量 = XX，p = XX > 0.05，残差为白噪声，模型提取了序列中的主要信息。
>
> **预测效果**：在测试集上的MAPE = XX%，RMSE = XX。
>
> **实现工具**：Python的statsmodels库（版本0.14.0）中的SARIMAX类实现。

---

## 六、灵敏度分析

**完整表述模板：**

> 为考察模型参数变化对结果的影响，本文选取XX和YY两个核心参数进行灵敏度分析。选取依据为：这两个参数在实际中XX，具有较大的不确定性/波动性。
>
> **分析方法**：固定其他参数不变，分别将XX参数在[-20%, +20%]范围内以5%为步长变化，计算对应的目标函数值/关键输出指标。
>
> **灵敏度系数**：采用相对变化率衡量参数敏感度：
> $$ S = \frac{\Delta Y / Y}{\Delta P / P} $$
> 其中 $S$ 为灵敏度系数，$\Delta Y / Y$ 为输出的相对变化率，$\Delta P / P$ 为参数的相对变化率。
>
> **分析结果**：（见表X/图X）
> - XX参数的灵敏度系数为XX，对结果影响XX；
> - YY参数的灵敏度系数为XX，对结果影响XX。
>
> **结论**：模型对XX参数较为敏感，实际应用中需准确测定该参数；模型对YY参数不敏感，具有较好的鲁棒性。总体而言，在参数±20%的变化范围内，结果波动不超过XX%，模型稳定性良好。

---

## 七、CVaR 风险优化

**完整表述模板：**

> 为量化不确定性下的风险，本文引入条件风险价值（Conditional Value at Risk, CVaR）作为风险度量指标。CVaR衡量的是损失超过VaR部分的条件期望，具有次可加性和凸性，是一致性风险度量。
>
> 置信水平取 $\alpha = 95\%$，表示关注最坏5%情况下的平均损失。
>
> CVaR的计算公式为：
> $$ \text{CVaR}_\alpha = \min_{\gamma} \left\{ \gamma + \frac{1}{1-\alpha} \mathbb{E}[f(x, \xi) - \gamma]^+ \right\} $$
> 其中 $f(x, \xi)$ 为损失函数，$x$ 为决策变量，$\xi$ 为随机变量，$[z]^+ = \max(z, 0)$。
>
> **场景生成**：采用蒙特卡洛模拟生成N = 1000个场景，各不确定因素服从XX分布（依据XX数据/文献估计）。
>
> **目标函数**：以期望收益最大化为目标，同时控制CVaR风险：
> $$ \max \quad \lambda \cdot \mathbb{E}[R(x, \xi)] - (1-\lambda) \cdot \text{CVaR}_\alpha(x) $$
> 其中 $\lambda$ 为风险偏好系数，本文取 $\lambda = $ XX（风险中性/风险规避）。

---

## 各方法实现库速查表

| 方法 | Python库 | 版本参考 | 导入示例 |
|------|---------|---------|---------|
| 线性规划 | pulp / scipy.optimize.linprog / gurobipy | — | `import pulp` |
| 混合效应模型 | statsmodels | 0.14.x | `import statsmodels.api as sm` |
| 遗传算法 | DEAP / scikit-opt (sko) | — | `from deap import base, creator, tools` |
| 模拟退火 | scikit-opt / 自实现 | — | `from sko.SA import SA` |
| 粒子群 | scikit-opt / 自实现 | — | `from sko.PSO import PSO` |
| 随机森林 | sklearn.ensemble | 1.x | `from sklearn.ensemble import RandomForestRegressor` |
| XGBoost | xgboost | 1.7.x | `import xgboost as xgb` |
| LightGBM | lightgbm | 3.3.x | `import lightgbm as lgb` |
| SVM | sklearn.svm | 1.x | `from sklearn.svm import SVR/SVC` |
| 聚类 | sklearn.cluster | 1.x | `from sklearn.cluster import KMeans` |
| ARIMA | statsmodels | 0.14.x | `from statsmodels.tsa.arima.model import ARIMA` |
| GPR | sklearn.gaussian_process | 1.x | `from sklearn.gaussian_process import GaussianProcessRegressor` |
| 假设检验 | scipy.stats | — | `from scipy import stats` |
| FDR控制 | statsmodels.stats.multitest | — | `from statsmodels.stats.multitest import multipletests` |
| 贝叶斯 | PyMC / pymc3 | 5.x | `import pymc as pm` |
| 深度学习 | PyTorch / TensorFlow | 2.x | `import torch` |
| SHAP | shap | 0.41.x | `import shap` |
| 超参优化 | Optuna | 3.x | `import optuna` |
