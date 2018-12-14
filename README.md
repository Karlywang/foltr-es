# Federated Online Learning to Rank with Evolution Strategies

This repo contains the code used to run experiments for the paper 'Federated Online Learning to Rank with Evolution Strategies',
WSDM 2019 [(link)](https://dl.acm.org/citation.cfm?id=3290968)


## Installation

In order to reproduce the experiments, we need to (1) setup an appropriate python environment, and (b) download the
datasets used in the paper. The steps below assume that we create a new conda environment solely for the purpose
of running this code.

First, you need to install PyTorch ([pytorch.org](pytorch.org)). Next, we will create a conda environment:

```
conda create --name federated python=3.6
source activate federated
# assuming you want to checkout the repo in the current directory
git clone https://github.com/facebookresearch/foltr-es.git && cd foltr-es
pip install -r requirements.txt
```
That's it! The next step is to download the datasets.


## Getting datasets

In the paper, two datasets are used, MQ2007 and MQ2008. They can be downloaded from the Microsoft Research
[website](https://www.microsoft.com/en-us/research/project/letor-learning-rank-information-retrieval/).

After downloading MQ2007.rar and MQ2008.rar files, they have to be unpacked within the `./data` folder.


Once the requirements are installed and the datasets are downloaded, one you can check that everything is in order by running pytest:

```
pytest -v
```
All tests should be passing.


## Reproducing results

All notebooks are in the `./notebooks` folder.

### Estimating privacy loss by simulating user click behavior

To get the results that are reported in Table 2:
```
python eps_estimate.py
```

### Hyperparameter investigation
Figures 1 - 3 are generated by the following Jupyter notebooks:

 * `antithetic.ipynb`: influence of antithetic variates on the optimization performance (Figure 1);
 * `n_interactions.ipynb`: batch size vs optimization performance (Figure 2);
 * `privacy robustness.ipynb`: privacy level vs optimization performance (Figure 3).

You can simply start a jupyter session in the root of the repo and re-run them. 

### Learning to rank experiments

The Figures 4 and 5 are generated by the notebooks `letor-2007.ipynb` and `letor-2008.ipynb`, respectively.
However, these notebooks actually use pre-calculated scores of the baselines, that are stored in 
`baselines.json`. Once you want to re-generate those, you have to:
 * download SVMRank from the author's [site](https://www.cs.cornell.edu/people/tj/svm_light/svm_rank.html) and put it in `./svmrank/`:
```
mkdir svmrank && cd svmrank
# an example for the linux64 platform; please check the site for more options
wget http://download.joachims.org/svm_rank/current/svm_rank_linux64.tar.gz
tar -xzf svm_rank_linux64.tar.gz
```
* after then you can run the script to generate the `baselines.json`:
```
python baselines.py
```

### Citation

If you find this code or the ideas in the paper useful in your research, please consider
citing the paper:

```
@inproceedings{Kharitonov2019,
    title={Federated Online Learning to Rank with Evolution Strategies},
    author={Kharitonov, Eugene},
    booktitle={WSDM},
    year={2019}
}
```


## License
foltr-es is CC-BY-NC licensed, as found in the LICENSE file.
