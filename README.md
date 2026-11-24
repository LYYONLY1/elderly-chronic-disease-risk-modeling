# 老年慢病风险建模

基于 RESILIENT 研究数据的人口统计、睡眠及可穿戴设备特征，做高血压标签的回顾性分类。项目包括数据聚合、特征处理、随机森林基线和模型对比。适用于研究和教学复现。

## 本地运行

把 [RESILIENT 官方数据](https://zenodo.org/records/15045663) 下载并解压到本机的 `data/`，使 `Demographics.csv` 与 `Sleepmat_Watch_Data/` 同级。数据由 RESILIENT 研究团队发布，引用和致谢要求见 [数据维护者说明](https://github.com/tmi-lab/Resilient-Dataset)。

```sh
python -m venv .venv
# 激活 .venv 后
python -m pip install -r requirements.txt
python train_hypertension_pipeline.py --data-dir data --out-dir outputs/baseline
python compare_models.py --data-dir data --out-dir outputs/comparison
```

训练使用人口统计和按参与者聚合的设备特征，评估比较逻辑回归、随机森林、Extra Trees、梯度提升和集成模型。用户编号只用于关联和定位本地结果。高血压诊断字段只用于生成分类标签。缺失值填补和缩放在训练管线内拟合。

该任务识别数据集中的既有高血压标签，没有验证未来发病预测、临床诊断或干预效果。请把逐参与者预测及中间特征表保存在本地。公开仓库提供训练和对比源码以及官方数据入口。
