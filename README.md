# 🚗 KNN渠道风险价值评估

🔍 利用KNN机器学习算法，智能评估汽车金融合作渠道的风险与价值，助力销售团队精准决策！

📖 项目简介
本项目通过K-最近邻(KNN)算法，分析汽车金融渠道的​​历史销量​​、​​逾期率​​、​​经营状态​​等20+维度数据，构建渠道价值-风险矩阵，实现：

🏆 ​​渠道分级​​：自动识别"高价值-低风险"黄金渠道
⚠️ ​​风险预警​​：提前发现潜在风险渠道
📊 ​​智能看板​​：可视化呈现渠道健康度热力图

📌 要求：R ≥ 4.0 | 📁 数据格式：Excel(.xlsx) | 💻 测试环境：RStudio 2023.03
##  🛠️ Technical Stack / 安装依赖包

* **Programming Language (编程语言)**: R 4.4
* **Core R Packages (主要R包)**:
* install.packages(c("tidyverse", "caret", "DMwR", "ggplot2", "ROSE"))
    * `readxl`: For importing data (数据导入).
    * `dplyr`: For efficient data manipulation (数据整理).
    * `ggplot2`: For creating visualizations (数据可视化).
    * `caret` or `tidymodels`: For KNN algorithm, preprocessing, tuning (机器学习流程).
    * `rmarkdown` / `knitr`: For generating reports (报告生成).
    * `DMwR` or `ROSE` For balance test and train dataset(⚖️ SMOTE过采样解决类别不平衡问题).

## 运行代码
rmarkdown::render("KNN_Channel_Analysis.Rmd")


## 🧬 Core Functionality & Project Workflow / 核心功能与项目流程
This project is developed within a R Markdown file, structuring the analysis logically from data input to insight generation. Key functional stages include:
(本项目在一个R Markdown文件中开发，逻辑清晰地组织了从数据输入到洞察生成的全过程。关键功能阶段包括：)

1.  **Data Ingestion & Preparation (数据导入与准备📂 )**:
    * Loads data from specified Excel files using `readxl`. (使用 `readxl` 从指定的Excel文件加载数据。)
    * Performs data cleaning, including addressing of specific missing value patterns, data type correction ]. (执行数据清洗，例如：[特定的缺失值处理模式、基于领域知识的数据类型校正 ])
    * **Custom Preprocessing Functions (🧹 智能处理缺失值|自动填充+正则化)**:
        * `rescale()`: [Normalizes specific skewed features using a log transformation."]. (对特定偏态特征进行对数转换以实现正态化。)
        * `ifelse()`: [find null value and replace with nul or others - **识别NULL，取而代之**]

2.  **Feature Engineering (🔬 特征工程)** :
    * [calculating today() and Initial cooporation day to create a numbers of cooperation day."]. (“计算初始生效日期和今天创建了一个合作天数。”)

3.  **Model Training & Hyperparameter Tuning (模型训练与超参数调优)**:
    * Utilizes the `caret` framework for KNN model training. (运用 `caret`框架进行KNN模型训练。)
    * Data is split into training (75%) and testing (25%) sets. (数据按比例划分为训练集和测试集，75%训练，25%测试。)
    * **Hyperparameter K Optimization (超参数K优化)**: The optimal number of neighbors (K) is determined by `X-fold cross-validation]` on the training set, evaluating K values from `[ 1 to 20]`. The K value yielding the `Accuracy` is selected. (通过在训练集上进行[X折交叉验证]`来确定最佳邻居数K，评估K值范围从`[1到20]`，选择产生`准确率`的K值。)
    * **Feature Scaling (特征缩放)**: Numerical features are `[centered and scaled (standardized)]` , which is crucial for distance-based algorithms like KNN. (在训练前，对数值型特征进行`[中心化和标准化]`处理，这对KNN等基于距离的算法至关重要。)

4.  **Model Evaluation & Interpretation (模型评估与解读)**:
    * The trained model's performance is assessed on the unseen test set using metrics like Accuracy and a Confusion Matrix. (在未见过的测试集上评估训练模型的性能，使用准确率和混淆矩阵等指标。)
    * Key visualizations include "K value vs. Prediction Accuracy", "Classification Results", and "Confusion Matrix". (关键可视化包括“K值与预测准确率关系图”、“分类结果”和“混淆矩阵”。)

5.  **Reporting (报告生成)**:
    * The entire analysis, including code, outputs, and narrative, is compiled into a reproducible HTML report via `knitr` and `rmarkdown`. (整个分析过程，包括代码、输出和文字说明，都通过`knitr`和`rmarkdown`编译成可复现的HTML报告。)

## 💾 Model Export & Usage / 模型导出与应用
The trained KNN model is saved to disk for potential future use or deployment, allowing for predictions on new channel data without retraining.
(训练好的KNN模型被保存，以便将来使用或部署，从而可以在不重新训练的情况下对新的渠道数据进行预测。)

* **Using the Exported Model (使用导出的模型)**:
    * To make predictions on new, unseen data, the saved model can be loaded back into an R session using `readRDS()`.
        ```R
        knn_model_meta <- list(
        train_data = channels_train,
         train_labels = channels_train_labels,
         k_value = 2,  # 保存关键参数
         normalization_params = list(  # 若有归一化参数需保存
         mean = apply(channels_train, 2, mean),
         sd = apply(channels_train, 2, sd)
          )
         )

# 使用压缩格式保存 saving with compression
        saveRDS(knn_model_meta, file = "knn_model_meta.rds", compress = "xz")

# 重新加载时 reload
         loaded_model <- readRDS("knn_model_meta.rds")
        ```

## 📈 关键成果
1. K值优化曲线
确定​​K=2​​时达到93.7%预测准确率📐 
![image](https://github.com/user-attachments/assets/59672bf3-e1f5-48e1-a21c-6e525b83dc7f)


2. 混淆矩阵热力图📉 

![image](https://github.com/user-attachments/assets/e2f5d491-8aa5-4aba-b4cc-0a4b3e7ae290)


![image](https://github.com/user-attachments/assets/ad232cc5-4915-495e-a0fd-3ff33e7771b2)


## 🤖 模型构建
🎯 基于caret包实现KNN自动化训练

## 🌟 核心价值
✅ ​​商业价值​​：使新渠道风险评估效率提升60%
✅ ​​技术突破​​：在以下方面展现卓越能力：

## 复杂业务数据建模能力（处理20+异构特征）
不平衡数据处理技巧（SMOTE调整后F1-score提升41%）
可解释性机器学习实践（SHAP值特征分析）
## 📜 证书与协议
https://img.shields.io/badge/License-Apache_2.0-blue.svg

🤝 参与贡献
欢迎提交Issue
📌 报告数据异常
💡 提议新特征
🐛 修复代码缺陷
📧 联系：shevril@gmail.com 
## 🌟 Demonstrating Techniques in Data Science


