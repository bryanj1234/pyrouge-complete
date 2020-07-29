## An easier way to install pyrouge
test
This repository contains the two components you need to use pyrouge in to score text summaries by using Python.

It's verified to work on Ubuntu 20.04 LTS with Python 3.7.

It combines two previous repositories:
* The ROUGE-1.5.5 repo from [here](https://github.com/andersjo/pyrouge.git), and
* The pyrouge repo from [here](https://github.com/bheinzerling/pyrouge.git)

The installation instructions were basically taken from
[here](https://medium.com/@sagor_sarker/how-to-install-rouge-pyrouge-in-ubuntu-16-04-7f0ec1cda81b).

Note: The https://pypi.org/project/py-rouge/ package is outdated,
    so **don't** try to install pyrouge it by running `"pip install pyrouge"`.

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
        python setup.py install
        pyrouge_set_rouge_path $ROUGE_BASE
        
1. Test it

        cd $ROUGE_BASE/../../../pyrouge_python/
        python -m pyrouge.test

    If it's successful, then the last lines of the out put should be something like this:
    
        2020-07-28 22:51:19,808 [MainThread  ] [INFO ]  Processing D30005.M.100.T.G.
        2020-07-28 22:51:19,808 [MainThread  ] [INFO ]  Saved processed files to /tmp/tmplz7avgeu/model.
        2020-07-28 22:51:19,809 [MainThread  ] [INFO ]  Written ROUGE configuration to /tmp/tmp2dy_c27f/rouge_conf.xml
        2020-07-28 22:51:19,809 [MainThread  ] [INFO ]  Running ROUGE with command /home/bryan/Desktop/pyrouge_combined/pyrouge_workers/tools/ROUGE-1.5.5/ROUGE-1.5.5.pl -e /home/bryan/Desktop/pyrouge_combined/pyrouge_workers/tools/ROUGE-1.5.5/data -c 95 -2 -1 -U -r 1000 -n 4 -w 1.2 -a -m /tmp/tmp2dy_c27f/rouge_conf.xml
        ../tmp/tmprmkmdxy5/config_test.xml data/config_test.xml
        ...
        ----------------------------------------------------------------------
        Ran 11 tests in 2.397s
        
        OK
        

