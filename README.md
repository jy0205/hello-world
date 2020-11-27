# BERT-GCN-CRF for NER
CLUENER 细粒度命名实体识别.

## Environment

* python>=3.6.4
* pytorch==1.5.1
* seqeval==0.0.12
* tqdm
* numpy==1.19.2
* jieba==0.42.1

## Model

* BERT + GCN + CRF

## Code Structure

main.py: The run file of the whole project

net_utils.py: The train,validate,test function and other untils.

data_loader.py: Used for constructing dataset and prepare BERT output.

cal_f1.py: The function to calculate F1-score.

pos_tag.py: Generating the part of speech tag.

crf.py: The CRF model definition.

transfer.py: Transfer the BIO Data to Json data.

evaluate.py: Output the final F1 score in Testset

### Our trained model

We put our trained model on folder: model_save/bert_gcn_crf/checkpoint-best,
the model checkpoint file is: pytorch_model.bin.

## Usage
### **Train**
```
# run bert-gcn-crf
sh train.sh
```

or using the following commands:

```
# train model use 4 GPUs
CUDA_VISIBLE_DEVICES=1,4,6,7 python main.py \
  --model_name=bert_gcn_crf \
  --train_model \
  --save_model \
  --crf_lr=1e-3 \
  --lr=3e-5 \
  --gcn_lr=1e-3 \
  --per_gpu_batch_size=16 \
  --model_save_dir=./model_save \
  --checkpoint_save_dir=./model_save/bert_gcn_crf/checkpoint-best \
  --epochs=5
```
### **Test**

```
# run bert-gcn-crf
sh test.sh
```
or using the following commands:

```
# test model use 1 GPU
CUDA_VISIBLE_DEVICES=0 python main.py \
  --model_name=bert_gcn_crf \
  --test_model \
  --model_save_dir=./model_save \
  --checkpoint_save_dir=./model_save/bert_gcn_crf/checkpoint-best
```

## Results
Report on the test set of CLUENER. The size of subset is as follows:

Training Set|Validation set|Test set
|:-:|:-:|:-:|
9674|1,074|1343|

(We use the above split to cross-validate and find the optimal hyper parameter. Then we merge the train and
valiadation set to train the final model by leveraging the observed optimal settings.)

**The train log is on logs/train_log.txt**

**The test log is on logs/test_log.txt**

### Comparison results

| Model     | F1 |
|:-------------:|:-----:|
| Bi-LSTM+CRF | 70.00 |
| Bert+CRF   | 78.87  |
| BERT+GCN+CRF(ours) | **80.38** |

The results for each entity (F1 score)：
| Entity          | Bi-LSTM+CRF | Bert+CRF | BERT+GCN+CRF(ours) |
|:-------------:|:-----:|:-----:|:-----:|
| Name          | 74.04 | 87.69 | **88.16** |
| Organization  | 75.96 | **79.53** | 77.34 |
| Position      | 70.16 | 79.60 | **79.73** |
| Company       | 72.27 | 77.64 | **80.37** |
| Address       | 45.50 | 63.11 | **68.28** |
| Game          | 85.27 | 85.47 | **85.67** |
| Government    | 77.25 | **84.38** | 81.75 |
| Scene         | 52.42 | 69.63 | **76.42** |
| Book          | 67.20 | 80.00 | **81.29** |
| Movie         | 78.97 | 81.69 | **85.17** |
| Overall@Macro | 70.00 | 78.87 | **80.38** |

### Abalation Studies

| GCN Layers    | F1 |
|:-------------:|:-----:|
| 1   |  79.42  |
| 2 | 79.83 |
| 3 | **80.38** |
| 4 | 79.05 |


| Model     | F1 |
|:-------------|:-----:|
| BERT+GCN+CRF   | **80.38** |
| -GCN module | 78.95 |
| -Tag embedding module | 79.86 |


## References

* **CRF**: https://github.com/CLUEbenchmark/CLUENER2020/blob/master/pytorch_version/models/crf.py
