# 🚗 KNN渠道风险价值评估

🔍 利用KNN机器学习算法，智能评估汽车金融合作渠道的风险与价值，助力销售团队精准决策！

📖 项目简介
本项目通过K-最近邻(KNN)算法，分析汽车金融渠道的​​历史销量​​、​​逾期率​​、​​经营状态​​等20+维度数据，构建渠道价值-风险矩阵，实现：

🏆 ​​渠道分级​​：自动识别"高价值-低风险"黄金渠道
⚠️ ​​风险预警​​：提前发现潜在风险渠道
📊 ​​智能看板​​：可视化呈现渠道健康度热力图

📌 要求：R ≥ 4.0 | 📁 数据格式：Excel(.xlsx) | 💻 测试环境：RStudio 2023.03
# 安装依赖包
install.packages(c("tidyverse", "caret", "DMwR", "ggplot2", "ROSE"))

# 运行代码
rmarkdown::render("KNN_Channel_Analysis.Rmd")


# 📈 关键成果
1. K值优化曲线
确定​​K=2​​时达到93.7%预测准确率
![image](https://github.com/user-attachments/assets/59672bf3-e1f5-48e1-a21c-6e525b83dc7f)




2. 混淆矩阵热力图
![image](https://github.com/user-attachments/assets/e2f5d491-8aa5-4aba-b4cc-0a4b3e7ae290)

![image](https://github.com/user-attachments/assets/ad232cc5-4915-495e-a0fd-3ff33e7771b2)



# 🔬 技术亮点
📂 数据预处理
🧹 智能处理缺失值（自动填充+正则化）
⚖️ SMOTE过采样解决类别不平衡问题
📐 特征工程构建复合指标：

风险评分 = 逾期率*0.6 + 经营状态*0.4
价值评分 = 销量*0.5 + 活跃度*0.3 + 地域系数*0.2


# 🤖 模型构建
🎯 基于caret包实现KNN自动化训练
📉 独创双维度评估矩阵：
classify_channel <- function(risk, value) {
  case_when(
    risk < 0.3 & value > 0.7 ~ "黄金渠道",
    risk > 0.6 ~ "高风险渠道",
    TRUE ~ "普通渠道"
  )
}
# 🌟 核心价值
✅ ​​商业价值​​：使新渠道风险评估效率提升60%
✅ ​​技术突破​​：在以下方面展现卓越能力：

# 复杂业务数据建模能力（处理20+异构特征）
不平衡数据处理技巧（SMOTE调整后F1-score提升41%）
可解释性机器学习实践（SHAP值特征分析）
# 📜 证书与协议
https://img.shields.io/badge/License-Apache_2.0-blue.svg

🤝 参与贡献
欢迎提交Issue
📌 报告数据异常
💡 提议新特征
🐛 修复代码缺陷
📧 联系：shevril@gmail.com 


