Semantic Question Matching
====

A Tensorflow implementation of a BiLSTM-MaxPooling Siamese Network [1] for Paraphrase Detection on the Quora question pairs dataset [2]. The encoder can be pretrained with a Sequential Denoising Autoencoder (SDAE)
to tackle the semi-supervised setting (as in [3]).

### Requirements
The code is written in Python 3 with the following dependencies:

* Tensorflow (== 1.4)
* numpy
* pandas
* NLTK
* Gensim

### Docker
A Dockerfile with the corresponding GPU environment and jupyterlab is provided in /docker.
```bash
cd docker
nvidia-docker build -t sqm .
nvidia-docker run -it -p 8888:8888 -v <absolute_path>/:notebooks/ sqm
```

### Data
```bash
cd data
unzip data.zip -d .
./get_glove.sh
``` 

This will unzip Quora's dataset and download GloVE.6B.  
The provided split is the standard partition from [4] in the original Quora format.  
**None of question id and pair id match the original release from Quora.**

### Training
Supervised Siamese Network:
```bash
python training.py -m siamese
```
Semi-supervised SDAE-Siamese Network:
```bash
# -res is the size of the labeled seed of question pairs
python training.py -m hybrid -res 1000
```

### References

[1] A. Conneau, D. Kiela, H. Schwenk, L. Barrault, A. Bordes, [*Supervised Learning of Universal Sentence Representations from Natural Language Inference Data*](https://arxiv.org/abs/1705.02364)

[2] [Quora question pairs dataset](https://data.quora.com/First-Quora-Dataset-Release-Question-Pairs)

[3] D. Shen, Y. Zhang, R. Henao, Q. Su, L. Carin, [*Deconvolutional Latent-Variable Model for Text Sequence Matching*](https://arxiv.org/abs/1709.07109)

[4] Z. Wang, W. Hamza, R.Florian, [*Bilateral Multi-Perspective Matching for Natural Language Sentences*](https://arxiv.org/abs/1702.03814)
