This repository contains the two components you need to use pyrouge in to score text summaries by using Python.

It combines two previous repositories:
* The ROUGE-1.5.5 repo from [here](https://github.com/andersjo/pyrouge.git), and
* The pyrouge repo from [here](https://github.com/bheinzerling/pyrouge.git)

The installation instructions were taken from
[here](https://medium.com/@sagor_sarker/how-to-install-rouge-pyrouge-in-ubuntu-16-04-7f0ec1cda81b).

## Installation on Debian-based linux

1. Make sure Perl is installed.

        sudo apt-get install perl
    
1. Install libxml-dom-perl.

        sudo apt install libxml-dom-perl

1. Clone this repository (https://github.com/bryanj1234/pyrouge_combined).

        git clone https://github.com/bryanj1234/pyrouge_combined

1. Install ROUGE-1.5.5.

        cd pyrouge_combined/pyrouge_workers/
        export ROUGE_BASE="$(pwd)/tools/ROUGE-1.5.5/"
        export ROUGE_EVAL_HOME="$(pwd)/tools/ROUGE-1.5.5/data/"
        cd $ROUGE_EVAL_HOME/WordNet-2.0-Exceptions/
        ./buildExeptionDB.pl . exc WordNet-2.0.exc.db
        cd ../
        rm WordNet-2.0.exc.db
        ln -s WordNet-2.0-Exceptions/WordNet-2.0.exc.db WordNet-2.0.exc.db
        
1. Install pyrouge

        cd $ROUGE_BASE/../../../pyrouge_python/
        mkdir bin
        python setup.py install
        pyrouge_set_rouge_path $ROUGE_BASE
        
1. Test it

        cd $ROUGE_BASE/../../../pyrouge_python/
        python -m pyrouge.test

---

This repository contains code for the ACL 2017 paper *[Get To The Point: Summarization with Pointer-Generator Networks](https://arxiv.org/abs/1704.04368)*. 

## Looking for test set output?
The test set output of the models described in the paper can be found [here](https://drive.google.com/file/d/0B7pQmm-OfDv7MEtMVU5sOHc5LTg/view?usp=sharing).

## Looking for pretrained model?
A pretrained model is available here:
* [Version for Tensorflow 1.0](https://drive.google.com/file/d/0B7pQmm-OfDv7SHFadHR4RllfR1E/view?usp=sharing)
* [Version for Tensorflow 1.2.1](https://drive.google.com/file/d/0B7pQmm-OfDv7ZUhHZm9ZWEZidDg/view?usp=sharing)

(The only difference between these two is the naming of some of the variables in the checkpoint. Tensorflow 1.0 uses `lstm_cell/biases` and `lstm_cell/weights` whereas Tensorflow 1.2.1 uses `lstm_cell/bias` and `lstm_cell/kernel`).

## Looking for CNN / Daily Mail data?
Instructions are [here](https://github.com/abisee/cnn-dailymail).

## About this code
This code is based on the [TextSum code](https://github.com/tensorflow/models/tree/master/textsum) from Google Brain.

This code was developed for Tensorflow 0.12, but has been updated to run with Tensorflow 1.0.
In particular, the code in attention_decoder.py is based on [tf.contrib.legacy_seq2seq_attention_decoder](https://www.tensorflow.org/api_docs/python/tf/contrib/legacy_seq2seq/attention_decoder), which is now outdated.
Tensorflow 1.0's [new seq2seq library](https://www.tensorflow.org/api_guides/python/contrib.seq2seq#Attention) probably provides a way to do this (as well as beam search) more elegantly and efficiently in the future.

## How to run

### Get the dataset