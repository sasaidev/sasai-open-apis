# Sasai Open Apis

## What's New (February, 2021)

We have a new release [Sasai 2.9.20](https://www.sasai.global/)!

It comes with lots of bug fixes, optimizations and support for SasaiPay SDKs.

## Introduction

This repository contains examples and best practices for integrating with Sasai, provided as Jupyter notebooks.

- [Sasai Authourisation](examples/01_prepare_data): Third party web applications, accessed via Sasai's built-in browser can obtain the basic information of the user through the SaSai webpage’s authorization mechanism below
- [SasaiPay](examples/00_quick_start): Sasai pay allows a third-party merchant to process payments using the Sasai Wallet.  

## Getting Started

Please see the [setup guide](SETUP.md) for more details on setting up your machine locally, on a [data science virtual machine (DSVM)](https://azure.microsoft.com/en-gb/services/virtual-machines/data-science-virtual-machines/) or on [Azure Databricks](SETUP.md#setup-guide-for-azure-databricks).

To setup on your local machine:

1. Install Anaconda with Python >= 3.6. [Miniconda](https://conda.io/miniconda.html) is a quick way to get started.

2. Clone the repository

```bash
git clone https://github.com/Microsoft/Recommenders
```

3. Run the generate conda file script to create a conda environment: (This is for a basic python environment, see [SETUP.md](SETUP.md) for PySpark and GPU environment setup)

```bash
cd Recommenders
python tools/generate_conda_file.py
conda env create -f reco_base.yaml  
```

4. Activate the conda environment and register it with Jupyter:

```bash
conda activate reco_base
python -m ipykernel install --user --name reco_base --display-name "Python (reco)"
```

5. Start the Jupyter notebook server

```bash
jupyter notebook
```

6. Run the [SAR Python CPU MovieLens](examples/00_quick_start/sar_movielens.ipynb) notebook under the `00_quick_start` folder. Make sure to change the kernel to "Python (reco)".

**NOTE** - The [Alternating Least Squares (ALS)](examples/00_quick_start/als_movielens.ipynb) notebooks require a PySpark environment to run. Please follow the steps in the [setup guide](SETUP.md#dependencies-setup) to run these notebooks in a PySpark environment. For the deep learning algorithms, it is recommended to use a GPU machine.

## Related projects

- [Microsoft AI Github](https://github.com/microsoft/ai): Find other Best Practice projects, and Azure AI design patterns in our central repository.
- [NLP best practices](https://github.com/microsoft/nlp-recipes): Best practices and examples on NLP.
- [Computer vision best practices](https://github.com/microsoft/computervision-recipes): Best practices and examples on computer vision.
- [Forecasting best practices](https://github.com/microsoft/forecasting): Best practices and examples on time series forecasting.
