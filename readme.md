# [本项目代码是DSHGT论文的实现](https://arxiv.org/pdf/2306.01376.pdf)

## 程序代码说明
config/：
运行配置类，包括文件夹的设置，模型的参数等

data_process/
数据处理，包括使用joern生成cpg，将每个源代码文件拆分成function的cpg，每个cpg生成network的图结构，归一化，向量化等操作

dataset/
数据集相关类，包括自定义的CPG数据集

model/
HGT模型定义类

test/
HGT的测试类，使用ogb数据集，测试HGT的运行

get_metadata.py
获取所有的节点和边类型，作为异构图的输入

metrics.py
用于计算各种评估指标

run.py
运行程序的启动入口

train.py
启动模型训练

utils.py
各种工具类


## 运行过程说明

下载数据集对应的源代码
preprocess_source_code.py：通过joern_parse将源代码转为cpg.bin文件，然后通过joern_export将解析的cpg结构，导出到exprot.dot
split_export_dot: 将export.dot文件，通过前向后向遍历的方法，分离得到每个方法的dot文件，即 方法名.dot.
data_generator: 读取每个cpg文件，设置network图相关属性
dataset_generator: 通过symbolizer.py将源代码归一化，然后通过word_embedding.py进行embedding，划分训练集和测试集
run.py：程序运行的主入口