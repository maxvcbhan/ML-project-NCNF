# Neural Collaborative Filtering (Fork)

This repository is **forked** from the original project: [Neural Collaborative Filtering by He Xiangnan et al.](https://github.com/hexiangnan/neural_collaborative_filtering). It implements neural collaborative filtering methods for recommendation systems, combining matrix factorization and multi-layer perceptrons.
## 🌟 Summary of Improvement

This section highlights the key improvements made in the project:

- **Enhanced Functionality**: Introduced new configurations for `num_factors`, `num_neg`, and `topK` to extend the hyperparameter space for experiments and update keras's code to support python3 and keras version 3
- **Support for Additional Datasets**: Added integration with the GitHub Archive dataset, enabling analysis of open-source software activities.
- **Layer Comparison**: Enabled experiments to compare model performance with and without additional activity layers, providing deeper insights into model architecture design.
- **Improved Documentation**: Updated `README.md` and other resources to better explain the workflow, dataset usage, and experiment results.
- **Streamlined Grid Search**: Optimized grid search processes for faster and more efficient hyperparameter tuning across multiple datasets.

By incorporating these improvements, the project provides a more comprehensive and flexible framework for running experiments in neural collaborative filtering.
## 📊 Presentation
![alt text](https://github.com/maxvcbhan/ML-project-NCNF/blob/4c6a6303ba030116be2a8c94191ba1e613c759a7/pic/Cover.png)
![alt text](https://github.com/maxvcbhan/ML-project-NCNF/blob/e246af551bb3db3b84216a6886cc59e750a4b5a7/pic/page1.png)
![alt text](https://github.com/maxvcbhan/ML-project-NCNF/blob/26ef6a7d2d3f2779bc1c75054ead4a7d8dbe67b6/pic/page2.png)
![alt text](https://github.com/maxvcbhan/ML-project-NCNF/blob/c2fb6a3189db1aed0ef47358960d8aac83305ad3/pic/page3.png)
![alt text](https://github.com/maxvcbhan/ML-project-NCNF/blob/1a2489d5b60193dc78ecf92160e19bfd590b6389/pic/fig3.png)
![alt text](https://github.com/maxvcbhan/ML-project-NCNF/blob/master/pic/ResultRunTable.png)
![alt text](https://github.com/maxvcbhan/ML-project-NCNF/blob/f425f0bb2d38dcc13a7b59dbacb399aa33991650/pic/page4.png)
![alt text](https://github.com/maxvcbhan/ML-project-NCNF/blob/a9a84f3d801c3175e1f95fc7987273c0cd434243/pic/References.png)
***

## 🚀 How to Run the Experiments

The following sections describe how to execute the experiments for different configurations and datasets.

### 🔍 **Grid Search with MovieLens Dataset**

Run a grid search with the following configuration:
- **Hyperparameters**:
  - `num_factors`: [8]
  - `num_neg`: [10]
  - `topK`: [10]
- **Dataset**: MovieLens (ml-1m)

```bash
python NeuMF-gridsearch.py --dataset=ml-1m --batch_size=20480 --epochs=50
```

### 📌 **Grid Search with Pinterest Dataset**

Run a grid search with the following configuration:
- **Hyperparameters**:
  - `num_factors`: [8, 16, 32, 64]
  - `num_neg`: [1, 5, 10]
  - `topK`: [1, 5, 10]
- **Dataset**: Pinterest (pinterest)

```bash
python NeuMF-gridsearch-pinterest.py --dataset=ml-1m --batch_size=20480 --epochs=50
```
 ### 🌐 Grid Search with GitHub Archive Dataset (No Activity Layer)

Run a grid search with the following configuration:

**Hyperparameters**:
- `num_factors`: [8, 16, 32, 64]
- `num_neg`: [1, 5, 10]
- `topK`: [1, 5, 10]

**Dataset**: GitHub Archive (No Activity Layer)

```bash
python NeuMF-gridsearch-gh.py --dataset=gh-archive --batch_size=20480 --epochs=50
```

 ### 🌐 Grid Search with GitHub Archive Dataset (With Activity Layer)

Run a grid search with the following configuration:

**Hyperparameters**:
- `num_factors`: [8, 16, 32, 64]
- `num_neg`: [1, 5, 10]
- `topK`: [1, 5, 10]

**Dataset**: GitHub Archive (With Activity Layer)

```bash
python NeuMF-gridsearch-gh-add-layers.py --dataset=gh-archive --batch_size=20480 --epochs=50
```


## Details from authors
This is our implementation for the paper:

Xiangnan He, Lizi Liao, Hanwang Zhang, Liqiang Nie, Xia Hu and Tat-Seng Chua (2017). [Neural Collaborative Filtering.](http://dl.acm.org/citation.cfm?id=3052569) In Proceedings of WWW '17, Perth, Australia, April 03-07, 2017.

Three collaborative filtering models: Generalized Matrix Factorization (GMF), Multi-Layer Perceptron (MLP), and Neural Matrix Factorization (NeuMF). To target the models for implicit feedback and ranking task, we optimize them using log loss with negative sampling.

**Please cite our WWW'17 paper if you use our codes. Thanks!**

Author: Dr. Xiangnan He (http://www.comp.nus.edu.sg/~xiangnan/)

## Environment Settings
We use Keras with Theano as the backend.
- Keras version:  '1.0.7'
- Theano version: '0.8.0'

## Example to run the codes.
The instruction of commands has been clearly stated in the codes (see the  parse_args function).

Run GMF:
```
python GMF.py --dataset ml-1m --epochs 20 --batch_size 256 --num_factors 8 --regs [0,0] --num_neg 4 --lr 0.001 --learner adam --verbose 1 --out 1
```

Run MLP:
```
python MLP.py --dataset ml-1m --epochs 20 --batch_size 256 --layers [64,32,16,8] --reg_layers [0,0,0,0] --num_neg 4 --lr 0.001 --learner adam --verbose 1 --out 1
```

Run NeuMF (without pre-training):
```
python NeuMF.py --dataset ml-1m --epochs 20 --batch_size 256 --num_factors 8 --layers [64,32,16,8] --reg_mf 0 --reg_layers [0,0,0,0] --num_neg 4 --lr 0.001 --learner adam --verbose 1 --out 1
```

Run NeuMF (with pre-training):
```
python NeuMF.py --dataset ml-1m --epochs 20 --batch_size 256 --num_factors 8 --layers [64,32,16,8] --num_neg 4 --lr 0.001 --learner adam --verbose 1 --out 1 --mf_pretrain Pretrain/ml-1m_GMF_8_1501651698.h5 --mlp_pretrain Pretrain/ml-1m_MLP_[64,32,16,8]_1501652038.h5
```

Note on tuning NeuMF: our experience is that for small predictive factors, running NeuMF without pre-training can achieve better performance than GMF and MLP. For large predictive factors, pre-training NeuMF can yield better performance (may need tune regularization for GMF and MLP).

## Docker Quickstart
Docker quickstart guide can be used for evaluating models quickly.

Install Docker Engine
- [Ubuntu Installation](https://docs.docker.com/engine/installation/linux/ubuntu/)
- [Mac OSX Installation](https://docs.docker.com/docker-for-mac/install/)
- [Windows Installation](https://docs.docker.com/docker-for-windows/install/)

Build a keras-theano docker image
```
docker build --no-cache=true -t ncf-keras-theano .
```

### Example to run the codes with Docker.
Run the docker image with a volume (Run GMF):
```
docker run --volume=$(pwd):/home ncf-keras-theano python GMF.py --dataset ml-1m --epochs 20 --batch_size 256 --num_factors 8 --regs [0,0] --num_neg 4 --lr 0.001 --learner adam --verbose 1 --out 1
```

Run the docker image with a volume (Run MLP):
```
docker run --volume=$(pwd):/home ncf-keras-theano python MLP.py --dataset ml-1m --epochs 20 --batch_size 256 --layers [64,32,16,8] --reg_layers [0,0,0,0] --num_neg 4 --lr 0.001 --learner adam --verbose 1 --out 1
```

Run the docker image with a volume (Run NeuMF -without pre-training):
```
docker run --volume=$(pwd):/home ncf-keras-theano python NeuMF.py --dataset ml-1m --epochs 20 --batch_size 256 --num_factors 8 --layers [64,32,16,8] --reg_mf 0 --reg_layers [0,0,0,0] --num_neg 4 --lr 0.001 --learner adam --verbose 1 --out 1
```

Run the docker image with a volume (Run NeuMF -with pre-training):
```
docker run --volume=$(pwd):/home ncf-keras-theano python NeuMF.py --dataset ml-1m --epochs 20 --batch_size 256 --num_factors 8 --layers [64,32,16,8] --num_neg 4 --lr 0.001 --learner adam --verbose 1 --out 1 --mf_pretrain Pretrain/ml-1m_GMF_8_1501651698.h5 --mlp_pretrain Pretrain/ml-1m_MLP_[64,32,16,8]_1501652038.h5
```
* **Note**: If you are using `zsh` and get an error like `zsh: no matches found: [64,32,16,8]`, should use `single quotation marks` for array parameters like `--layers '[64,32,16,8]'`.

### Dataset
We provide two processed datasets: MovieLens 1 Million (ml-1m) and Pinterest (pinterest-20).

train.rating:
- Train file.
- Each Line is a training instance: userID\t itemID\t rating\t timestamp (if have)

test.rating:
- Test file (positive instances).
- Each Line is a testing instance: userID\t itemID\t rating\t timestamp (if have)

test.negative
- Test file (negative instances).
- Each line corresponds to the line of test.rating, containing 99 negative samples.
- Each line is in the format: (userID,itemID)\t negativeItemID1\t negativeItemID2 ...

Last Update Date: December 23, 2018
