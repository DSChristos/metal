# Snorkel MeTaL (previously known as _MuTS_)

<img src="assets/logo_01.png" width="150"/>

[![Build Status](https://travis-ci.com/HazyResearch/metal.svg?branch=master)](https://travis-ci.com/HazyResearch/metal)

**_v0.1.0-alpha_** 

**NOTE:**
Expect frequent changes, not all backwards-compatible, through mid-August when v0.1.0 is solidified and bundled as a pip/conda package. It will be released with additional documentation and tutorials.

Snorkel MeTaL is a framework for using multi-task weak supervision (MTS), provided by users in the form of _labeling functions_ applied over unlabeled data, to train multi-task models.
Snorkel MeTaL can use the output of labeling functions developed and executed in [Snorkel](snorkel.stanford.edu), or take in arbitrary _label matrices_ representing weak supervision from multiple sources of unknown quality, and then use this to train auto-compiled MTL networks.

**Check out the intro tutorial: https://github.com/HazyResearch/metal/blob/master/Intro_Tutorial.ipynb**

Snorkel MeTaL uses a new matrix approximation approach to learn the accuracies of diverse sources with unknown accuracies, arbitrary dependency structures, and structured multi-task outputs.
For more detail, see the **working draft of our technical report on MeTaL: [_Training Complex Models with Multi-Task Weak Supervision_](https://ajratner.github.io/assets/papers/mts-draft.pdf)**

## Sample Usage
This sample is for a single-task problem. 
For a multi-task example, see tutorials/Multi-task.ipynb.

```
"""
Load for each split: 
L: an [n,m] scipy.sparse label matrix of noisy labels
Y: an [n] numpy.ndarray of target labels
X: an n-length iterable (e.g., a list) of end model inputs
"""

from metal.label_model import LabelModel, EndModel

# Train a label model and generate training labels
label_model = LabelModel(k)
label_model.train(L_train)
Y_train_pred = label_model.predict(L_train)

# Train a discriminative end model with the generated labels
end_model = EndModel(k, layer_out_dims=[1000,10])
end_model.train(X_train, Y_train_pred, X_dev, Y_dev)

# Evaluate performance
score = end_model.score(X_test, Y_test)
```

## Setup
[1] Install anaconda3 (https://www.anaconda.com/download/#macos)

[2] Clone repository:
```
git clone https://github.com/HazyResearch/metal.git
cd metal
```

[3] Create environment:
```
source set_env.sh
conda env create -f environment.yml
source activate metal
```

[4] Test functionality:
```
nosetests
```

[5] Run tutorial:
```
jupyter notebook 
```
Open ```tutorials/Tutorial.ipynb```  
Select Kernel > Change kernel > Python [conda env:metal]  
Restart and run all
