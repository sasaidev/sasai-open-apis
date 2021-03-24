# Sasai Open Apis

## What's New (February, 2021)

We have a new release [Sasai 2.9.20](https://www.sasai.global/)!

It comes with lots of bug fixes, optimizations and support for SasaiPay SDKs.

## Introduction

This repository contains examples and best practices for integrating with Sasai, provided as Jupyter notebooks.

- [Sasai Authorisation](examples/01_prepare_data): authorise and obtain user's basic information 
- [SasaiPay](examples/00_quick_start): process payments using the Sasai Wallet.  

## 1. Authorisation

This is a three step process.

### 1.1 Get Authorisation Code

Add the javascript below on your web page to get the authorisation code

```bash
function authenticateWithSasai() {
    var jsonData = '{"type":"800", "appId": "ownai_client", "scope": "user_info"}';
    window.SasaiCall.openAuth(jsonData);  //for android
    window.webkit.messageHandlers.currentCookies.postMessage(jsonData); // for iOS
}
 
function returnAuth(callbackData) {
    var data = JSON.parse(callbackData);
    alert(data);
}
```

**NOTE** 
- The **appId** and **scope** will be provided. The test values are **"client"** and **"user_info"** respectively.
- The cookie **phoneNumber** contains the Sasai registered phone number.

##### callBackData object structure

```bash
{
    "ret": "0",
    "code": "XYTHSG",
    "scope": "user_info"
}
```
| Field | Description |
| --- | --- |
| ret | "0" = Sucess, "-1" = Failed |
| code | Authorisation code to be used in successive get toke operations |
| scope | Default is **user_info** |

### 1.2 Get Authorisation Code

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
