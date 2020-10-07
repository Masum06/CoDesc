# CodeCorpus

A large dataset of 4.2m Java source code and parallel data of their description from code search, and code summarization studies.

This is the public release of code, and data of our paper titled "CodeCorpus: Large Code-Description Parallel Dataset", submitted to EACL, 2021.

**Table of Contents**

<!-- TOC depthFrom:1 depthTo:6 withLinks:1 updateOnSave:1 orderedList:0 -->

- [Quickstart](#quickstart)
- [Introduction](#introduction)
- [CodeCorpus Dataset](#codecorpus-dataset)
    - [CodeCorpus Dataset Creation](#codecorpus-dataset-creation)
    - [Preprocess CodeCorpus for Code Search](#preprocess-codecorpus-for-code-search)
    - [Preprocess CodeCorpus for Code Summarization](#preprocess-codecorpus-for-code-summarization)
- [Tokenizer](#tokenizer)
- [Code Search](#code-search)
- [Code Summarization](#code-summarization)
- [Licenses](#licenses)

<!-- /TOC -->


# Quickstart
  ```bash
  # clone this repository
  git clone https://github.com/code-description2020/CodeCorpus.git
  
  # change permission of scripts
  sudo chmod -R +x CodeCorpus
  cd CodeCorpus/

  # setup
  ./Setup/setup.sh
  ```

# Introduction
This is a sample intro.


# CodeCorpus Dataset
After initial setup described at [Quickstart](#quickstart), our dataset will be downloaded at `data/` folder along with preprocessed data for code search task and code summarization task. We also provide the source datasets here. Following are the links and descriptions of the dataset and preprocessed data.

1. [CodeCorpus](https://mega.nz/file/Rsx3zaqY#stMEpCe33JLAIcslPZRf6sKXcka3JW3eivgjR5DFl5U): This file contains our 4.2m dataset. The details of this dataset is given in our paper as well as in [Dataset Description](https://github.com/code-description2020/CodeCorpus/blob/master/Dataset%20Description.md) page.

2. [Original_data](https://mega.nz/file/ZpoBla5a#qeSxMXP6v-2FEI237cIVrFhuqnq5DHh88_EKuReSY3k): This file contains the source data from where we have collected and preprocessed our 4.2m dataset.

3. [CSN_preprocessed_data](https://mega.nz/file/Q4oxQCIb#CT7P5zq1WbiWOLTeafg-mFD2QZEmF1YwZmDhGZkzU90): This file contains the preprocessed data for CodeSearchNet challenge. Here test and validation sets are the preprocessed datapoints from CodeSearchNet original test and validation sets.

4. [CSN_preprocessed_data_balanced_partition](https://mega.nz/file/t543VCyA#4BLjB28yYNDT9kXBs6NWmY1ADOCMyuvqDXLg9yPhiaI): This file contains the preprocessed data for CodeSearchNet networks. Here train, test, and validation sets are from our balanced partition described in our paper

5. [NCS_preprocessed_data](https://mega.nz/file/Npo1RaBZ#ug6jJPacpjNht537PmOwxsR2MlOps0Y-LOwhx8lQ5ys): This file contains the preprocessed data for neural code summarization networks.

6. *** add bpe tokenized ncs preprocessed data here ***

*** statistics table ***

## CodeCorpus Dataset Creation
As we have already mentioned, we have provided the original data from sources to the `data/original_data/` folder. To create the 4.2m CodeCorpus dataset from original data, the following command should be used.
 ```bash
 python Dataset_Preparation/Merge_Datasets.py
 ```

## Preprocess CodeCorpus for Code Search 
The following command preprocesses CodeCorpus dataset for [CodeSearchNet](https://arxiv.org/abs/1909.09436) Challenge. It also preprocesses their validation and test sets using the filters defined in our paper.
 ```bash
 python Dataset_Preparation/Preprocess_CSN.py
 ```

 To create a balanced train-valid-test split for CodeSearchNet networks, the command can be used.
  ```bash
 python Dataset_Preparation/Preprocess_CSN_Balanced_Partition.py
 ```

## Preprocess CodeCorpus for Code Summarization
The following command preprocesses CodeCorpus dataset for [NeuralCodeSum](https://arxiv.org/abs/2005.00653) networks.
  ```bash
 python Dataset_Preparation/Preprocess_NCS.py
 ```

 *** add commands here for bpe ***

# Tokenizer

*** details of the tokenizer ***


# Code Search
After initial setup described at [Quickstart](#quickstart), a forked version of [CodeSearchNet](https://github.com/code-description2020/CodeSearchNet.git) is cloned and preprocessed data of CodeCorpus will be copied to `CodeSearchNet/resources/data/`. To use the preprocessed dataset of balanced partition, clear the above mentioned folder, and copy the content inside of `data/csn_preprocessed_data_balanced_partition/` into it.

Then the following commands will train and test code search networks:
 ```bash
 cd CodeSearchNet/
 
 script/console
 wandb login
 
 python train.py --model neuralbowmodel --run-name nbow_codecorpus
 python train.py --model rnnmodel --run-name rnn_codecorpus
 python train.py --model selfattentionmodel --run-name attn_codecorpus
 python train.py --model convolutionalmodel --run-name conv_codecorpus
 python train.py --model convselfattentionmodel --run-name convattn_codecorpus
 ```

# Code Summarization
*** complete this section ***

# Licenses
Codes, dataset and models from [CodeSearchNet](https://github.com/github/CodeSearchNet.git), and [NeuralCodeSum](https://github.com/wasiahmad/NeuralCodeSum.git) are used with the licenses provided at their respective repositories.   
This code, preprocessed data, and pretrained models are released under the [MIT license](https://github.com/code-description2020/CodeCorpus/blob/master/LICENSE).