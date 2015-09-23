## Bayesian Echo Chamber

A new Bayesian generative model for social interaction data, for uncovering influence relations from time-stamped conversation data.

> Please refer to
> 
> Fangjian Guo, Charles Blundell, Hanna Wallach and Katherine A. Heller. The Bayesian Echo Chamber: modeling social influence via linguistic accommodation. *AISTATS 2015, San Diego, CA, USA. JMLR: W&CP volume 38.*
> 
> for details of the model.

### Files

``` 
├── data								a collection of datasets
├── results								results are produced here
│   ├── 12-angry-men-analytics.Rmd		generating report from result
│   └── Makefile						compile a html report from R markdown
├── src
│   ├── bec.py							main "Bayesian echo chamber" class
│   ├── bec_sampler.py					a wrapper of the sampler of bec
│   ├── hawkes.py						an implementation of Hawkes process
│   ├── likelihoods.py					several likelihoods
│   ├── run_bec_12angrymen.py			a demo script producing result for data/12-angry-men
│   ├── slice_sampler.py				slice sampler
│   ├── talkbankXMLparse.py				parser for talkbank xml format
└── stopwords
    └── english.stop					list of stop words in English
```

### Usage

1. Run `python run_bec_12angrymen.py` would produce samples and other auxiliary files under `results/12-angry-men/`. One could customize scripts based on `run_bec_12angrymen.py` for other datasets and configurations. 
2. Run `make` under `results/ ` could produce an html report compiled from [R Markdown](http://rmarkdown.rstudio.com) file `12-angry-men-analytics.Rmd`. One could customize the `Rmd` file for analyzing other datasets. 

### Dependencies

- Python modules (tested under Python 2.7)
  - numpy, scipy
  - matplotlib
  - [nltk](http://www.nltk.org) for word stemming in `talkbankXMLparse.py`
- R libraries for generating report
  - knitr
  - ggplot2
  - coda
  - plyr
  - qgraph
  - pander

### Datasets

The conversation data is read from the [TalkBank xml](https://talkbank.org/software/) format. A conversation consists of several utterances, with each utterance described with the following files: speaker, content, start time and end time, which looks like the snippet below.

``` xml
<u who="Juror 7" uID="#7">
<w>So</w>
<w>how</w>
<w>come</w>
<w>you</w>
<w>vote</w>
<w>not</w>
<w>guilty</w>
<media start="47.4640" end="49.3820" unit="s"/>
</u>
```

Currently, we have prepared the following datasets under `data/` directory.

1. **12 Angry Men**: transcribed from the 1957 movie subtitle. 
2. **SCOTUS**: oral arguments from 50 years of the United States Supreme Court, obtained from [TalkBank](http://talkbank.org/data/Meeting/SCOTUS/).
3. **synthetic**: a synthetic example with 3 agents speaking with a vocabulary of 20, with time stamps generated from a Hawkes process and contents generated from the BEC model.

### Authors

This repo is maintained by [Richard Guo](http://richardkwo.net). We also acknowledge the contribution of [Juston Moore](https://people.cs.umass.edu/~jmoore/) to `likelihoods.py` and `slice_sampler.py`.

