# BGRU-BLSTM-GloVe-fastText-NLP

## Objective
Predict a binary NLP sentiment classification for the IMDB dataset with 50,000 reviews with an evenly distributed target values **[1:Positive & 2:Negative]** using a Bidirectional **Gated Recurrent Unit** and Bidirectional **Long-Short-Term Memory**. Feature Engineer the reviews by cleaning, removing stop-words, tokenizing before obtaining a vector representation for each token using **GloVe pre-trained word embeddings**. Measure GRU performance with **accuracy score** since the target values are evenly distributed. Bi-GRU outperformed Bi-LSTM with 90.99% and 86.11%, respectively. 

## Bidirectional RNN 
Bidirectional Recurrent Neural Network's architecture adds a hidden layer that passes information in a backward direction. This allows information to be dependent not only the previous input but also the future values. The forward and backward hidden states are concatenated to obtain the hidden state and input it to the output layer
![](https://www.researchgate.net/publication/311430194/figure/fig1/AS:436131947913217@1480993367891/BiDirectional-RNN-architecture-for-detecting-clickbaits.png)


## Output 
**Bi-Directional GRU with fastText Embeddings**
```
Epoch:18/20, Train Accuracy: 93.65%, Eval Accuracy: 89.82%, Eval Precision: 0.8792
Epoch:19/20, Train Accuracy: 94.07%, Eval Accuracy: 89.87%, Eval Precision: 0.9028
```
**Bi-Directional GRU with GloVe Embeddings**
```
Epoch:19/20, Train Accuracy: 93.74%, Eval Accuracy: 89.87%, Eval Precision: 0.8989
Epoch:20/20, Train Accuracy: 94.96%, Eval Accuracy: 90.99%, Eval Precision: 0.8970
```
**Bi-Directional LSTM with fastText Embeddings**
```
Epoch:19/20, Train Accuracy: 87.29%, Eval Accuracy: 85.12%, Eval Precision: 0.8539
Epoch:20/20, Train Accuracy: 88.11%, Eval Accuracy: 85.26%, Eval Precision: 0.8688
```
**Bi-Directional LSTM with GloVe Embeddings**
```
Epoch:19/20, Train Accuracy: 88.95%, Eval Accuracy: 86.30%, Eval Precision: 0.8864
Epoch:20/20, Train Accuracy: 89.11%, Eval Accuracy: 86.11%, Eval Precision: 0.8933
```
## Repository File Structure
    ├── src          
    │   ├── train.py             # Training Bidirectional GRU and evaluating metric (accuracy & precision) 
    │   ├── bigru_model.py       # Bidirectional Gated Recurrent Unit (GRU) architecture, inherits nn.Module
    │   ├── bilstm_model.py      # Bidirectional Long-Short Term Memory (LSTM) architecture, inherits nn.Module
    │   ├── engine.py            # Class Engine for Training, Evaluation, and Loss function 
    │   ├── dataset.py           # Custom Dataset that return a paris of [input, label] as tensors
    │   ├── embeddings.py        # GloVe Embeddings and fastText Embeddings
    │   ├── data.py              # Cleaning dataset by removing stopwords and special characters, labeled target values
    │   └── config.py            # Define path as global variable
    ├── inputs
    │   ├── clean_train.csv      # Cleaned Data and Featured Engineered with re
    │   └── train.csv            # Kaggle IMDB Dataset 
    ├── models
    │   └── imdb_model.bin       # GRU parameters saved into model.bin 
    ├── static
    │   └── style.css            #  
    ├── templates
    │   └── index.html           # 
    ├── requierments.txt         # Packages used for project
    └── README.md

## Model's Architecture
```
BIGRU(
  (embedding): Embedding(180446, 100)
  (gru): BIGRU(100, 128, num_layers=2, batch_first=True, dropout=0.2, bidirectional=True)
  (out): Linear(in_features=512, out_features=1, bias=True)
  (sigmoid): Sigmoid()
)



BILSTM(
  (embedding): Embedding(180446, 100)
  (lstm): BILSTM(100, 128, num_layers=2, batch_first=True, dropout=0.2, bidirectional=True)
  (out): Linear(in_features=512, out_features=1, bias=True)
  (sigmoid): Sigmoid()
)
```  

## GPU's Menu Accelerator
```
Sat Aug 14 00:31:06 2021       
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 470.42.01    Driver Version: 460.32.03    CUDA Version: 11.2     |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|                               |                      |               MIG M. |
|===============================+======================+======================|
|   0  Tesla P100-PCIE...  Off  | 00000000:00:04.0 Off |                    0 |
| N/A   39C    P0    33W / 250W |   2047MiB / 16280MiB |      0%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+
```
