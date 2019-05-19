# FBB2019 reproduction project
*Belyaeva July, Bushmakin Ilya, Pushkarev Sergei*
## Intro
This project contains models and some test code for reproduction of some parts of article [1].

## Methods
This repository contains:
1) Chainer CNN from original article [1].
2) PyTorch CNN with the same architecture, but training code uses Cosine Annealing With Warm Restarts from article [2] to adjust 
 learning rate and achieve lower loss and higher accuracy
3) Clustering:
    1) Max pseudoclique clustering of CNN predictions
    2) Spectral clustering of DAFS matrices
4) Visualisation and analysis code

## Results
1) The original code from the article has a little documentation. Instructions from README
is not effective:
    1) `dafs` can not be installed from provided source without `make clean` due to 
        broken links to BOOST
    2) `dafscnn` in *MakeNcRNAMatrix has to be replaced with `dafs`
    3) Provided bash script can not build dataset. It works only for 60 sequence datasets,
        and even so, it produces only first two files instead of 60.
    4) *prepareData.py* was written to replace original bash script and integrate functions of
        *AssembleMatrix.py*
    5) Original *RNApairClassify.py* can not be used for cross-validation with -v < 10 passed
        due to mysterious line `val = 9` before the cycle. It is a patch to perform only the last part of
        cross-validation. This strange decision is also the reason of 'data vanishing', the 9/10 of the test dataset
        do not participate in training or validation of the CNN.
    6) We could not understand what is Unknown Family mode. All we know:
        > In addition to the 10-fold cross-validation experiment, as a 
        more difficult task and for the more practical purpose of finding
        new ncRNA families, the ncRNA families for generating the training
        data were chosen to be different from the ones for the test data.
        This experiment, called unknown-family validation, may evaluate
        the capacity of our one-dimensional CNN method for accurate 
        clustering of ncRNA sequences of unknown families that do not
        exist in the training data.
    7) On some datasets DataLoader produces empty datasets for some reason.
2) NO DOCSTRINGS and almost no comments on the details of the script 
    (metrics unmentioned, code for comparison not provided)
## References
1) Genta Aoki, Yasubumi Sakakibara, 
Convolutional neural networks for classification of alignments of non-coding 
RNA sequences, Bioinformatics, Volume 34, Issue 13, 01 July 2018, 
Pages i237–i244, https://doi.org/10.1093/bioinformatics/bty228
2) Loshchilov, Ilya, and Frank Hutter. 
"Sgdr: Stochastic gradient descent with warm restarts."
 arXiv preprint arXiv:1608.03983 (2016).
 
   