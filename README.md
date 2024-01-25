# 模型：Solitude

本项目来源于论文发表在2022年TIFS期刊上： [Towards Private Learning on Decentralized Graphs with Local Differential Privacy](https://wanyu-lin.github.io/assets/pdf/wanyu-tifs2022.pdf). 

## 要求

代码运行要求Python>3.9，同时依赖以下环境：  
- [PyTorch](https://pytorch.org/get-started/locally/) >= 1.8.1
- [PyTorch Geometric](https://pytorch-geometric.readthedocs.io/en/latest/notes/installation.html) >= 1.7.0
- [Pandas](https://pandas.pydata.org/pandas-docs/stable/getting_started/install.html) >= 1.2.4
- [Numpy](https://numpy.org/install/) >= 1.20.2
- [Seaborn](https://seaborn.pydata.org/) >= 0.11.1  
- [wandb](https://wandb.ai/site)

## 用法

### 训练好的独立模型
如果你想独立训练并评估模型效果，可以运行以下代码：
```
python main.py -d cora -ee 8 -ex 1 -kx 4 -ky 2 --model sage --learning_rate 0.01 --weight_decay 0.001 --dropout 0.5 -s 1234 --max-epochs 500 -o ./out/cora/ee8_ex1

python main.py -d citeseer -ee 8 -ex 1 -kx 4 -ky 2 --model sage --learning_rate 0.01 --weight_decay 0.001 --dropout 0.5 -s 12345 --max-epochs 200 --orphic True -o ./out/citeseer/ee8_ex1

python main.py -d lastfm -ee 8 -ex 1 -kx 4 --model sage --learning_rate 0.01 --weight_decay 0.001 --dropout 0.5 -s 12345 --max-epochs 500 -o ./out/lastfm/ee8_ex1

dataset arguments:
  -d              <string>       name of the dataset (choices: cora, pubmed, facebook, lastfm) (default: cora)
  --data-dir      <path>         directory to store the dataset (default: ./datasets)
  --data-range    <float pair>   min and max feature value (default: (0, 1))
  --val-ratio     <float>        fraction of nodes used for validation (default: 0.25)
  --test-ratio    <float>        fraction of nodes used for test (default: 0.25)

data transformation arguments:
  -ex             <float>        privacy budget for feature perturbation (default: inf)
  -ee             <float>        privacy budget for edge perturbation (default: inf)

model arguments:
  --model         <string>       backbone GNN model (choices: gcn, sage, gat) (default: sage)
  --hidden-dim    <integer>      dimension of the hidden layers (default: 16)
  --dropout       <float>        dropout rate (between zero and one) (default: 0.0)
  -kx             <integer>      KProp step parameter for features (default: 0)
  -ky             <integer>      KProp step parameter for labels (default: 0)
  --forward       <boolean>      applies forward loss correction (default: True)

trainer arguments:
  --optimizer     <string>       optimization algorithm (choices: sgd, adam) (default: adam)
  --max-epochs    <integer>      maximum number of training epochs (default: 500)
  --learning-rate <float>        learning rate (default: 0.01)
  --weight-decay  <float>        weight decay (L2 penalty) (default: 0.0)
  --patience      <integer>      early-stopping patience window size (default: 0)
  --device        <string>       desired device for training (choices: cuda, cpu) (default: cuda)
  --orphic        <string>       use estimator to clean graph (choices: True, False) (default: False)
  --inner_epoch   <integer>      the time of using estimator in a single epoch (default: 2)
  --checkpoint_dir <string>      the path to save checkpoint

experiment arguments:
  -s              <integer>      initial random seed (default: None)
  -r              <integer>      number of times the experiment is repeated (default: 1)
  -o              <path>         directory to store the results (default: ./output)
  --log           <boolean>      enable wandb logging (default: False)
  --log-mode      <string>       wandb logging mode (choices: individual,collective) (default: individual)
  --project-name  <string>       wandb project name (default: Solitude)
  --retrain       <boolean>      whether to retrain the model (default: False)
```

每一轮运行的结果都会保存为一个CSV文件，存放在./output目录下。

## 引用

如果你使用了作者代码，请引用以下文献：
```bibtex 
@article{lin2022towards,
  title={Towards private learning on decentralized graphs with local differential privacy},
  author={Lin, Wanyu and Li, Baochun and Wang, Cong},
  journal={IEEE Transactions on Information Forensics and Security},
  volume={17},
  pages={2936--2946},
  year={2022},
  publisher={IEEE}
}
```
