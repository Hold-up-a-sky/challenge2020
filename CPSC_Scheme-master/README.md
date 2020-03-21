# challenge2020工程说明

## 参考博客
项目主体来源：https://blog.csdn.net/qq_15746879
一个不成熟的开源小方案：关于2018中国生理信号挑战赛（CPSC-2018）(1)-(4)

## Environment：
工程里的库：biosppy，需要自己安装<br>
keras==2.2.4<br>
tensorflow-gpu==1.9.0<br>

## 工程文件说明：
心电数据可从博客中提到的百度云网盘中下载，或者到physioNet challenge2020官网上下载，再通过官网上的读取文件进行读取<br>
CPSC_config.py 说明参数的配置，以及工程中需要用到的数据存放路径<br>
CPSC_model.py 设计模型结构和HRV特征提取<br>
CPSC_train_signal_lead.py 训练生成单个导联的模型，模型结构参见以上博客<br>
CPSC_train_multi_leads.py 训练生成12导联对应的模型，并存放在模型路径中<br>
CPSC_utils.py 数据预处理，包括平衡数据集，滤波，切割分段<br>
CPSC_combine_leads.py 将各个导联模型输出的概率结合<br>
CPSC_hybrid.py 将各个模型输出和特征融合，采用XGboost进行分类<br>
stacking_test.py 将各个模型输出和特征融合，采用stacking进行分类，其中基础模型包括：RF、SVM、GB、GDBC、提升树<br>
stacking_test1.py 将各个模型输出和特征融合，采用stacking进行分类，其中基础模型包括：RF、SVM、XGboost、GDBC、提升树<br>
evaluate_12ECG_score.py 这是官网提供的评分文件，其中评分函数需要先将结果保存，我将这个函数改为直接用结果矩阵即可进行计算，不需要先进行存储<br>
模型融合方法目前XGboost最佳<br>
用Tensorflow-CPU的同学需要将文件中的os.environ改为“-1”<br>

## warning:
A CUDA device is required if you want to use the models shared in this repo.
If you don't have a CUDA device, change the "CuDNNLSTM" in CPSC_model.py to "LSTM" and train it using CPUs.But it may be very slow.
