# Overview
This repository contains the implementation for our paper titled "Analysing heterogeneity in Alzheimer Disease using multimodal normative modelling on ATN biomarkers", under review in Alzheimer's & Dementia [[BiorXiv](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC10473626/)] 

<img align="center" width="60%" height="75%" src="Figures & tables/Figure S1.png">

Figure 1: Our proposed multimodal normative modeling framework (mmVAE).

## Abstract

**INTRODUCTION**: Previous studies have applied normative modeling on a single neuroimaging modality to investigate Alzheimer Disease (AD) heterogeneity. We employed a deep learning-based multimodal normative framework to analyze individual-level variation across ATN (amyloid-tau-neurodegeneration) imaging biomarkers.

**METHODS**: We selected cross-sectional discovery (n = 665) and replication cohorts (n = 430) with available T1-weighted MRI, amyloid and tau PET. Normative modeling estimated individual-level abnormal deviations in amyloid-positive individuals compared to amyloid-negative controls. Regional abnormality patterns were mapped at different clinical group levels to assess intra-group heterogeneity. An individual-level disease severity index (DSI) was calculated using both the spatial extent and magnitude of abnormal deviations across ATN.

**RESULTS**: Greater intra-group heterogeneity in ATN abnormality patterns was observed in more severe clinical stages of AD. Higher DSI was associated with worse cognitive function and increased risk of disease progression.

**DISCUSSION**: Subject-specific abnormality maps across ATN reveal the heterogeneous impact of AD on the brain.

## Environment & Packages

We recommend an environment with python >= 3.7 and pytorch >= 1.10.2, and then install the following dependencies:
```
pip install -r requirements.txt
```
Cortical and subcortical brain atlases were visualized using the ggseg package. The original R implementation can be found [here](https://github.com/ggseg/ggseg). A more recent Python implementation can also be found [here](https://github.com/ggseg/python-ggseg).

## Datasets & Feature extraction

### Datasets

Our analysis included a discovery dataset consisting of individuals from ADNI and a replication dataset consisting of individuals from Charles F. and Joanne Knight Alzheimer’s Disease Research Center (ADRC) dataset at Washington University in St. Louis.

ADNI data used in this study are publicly available and can be requested following ADNI Data Sharing and Publications Committee guidelines: [https://adni.loni.usc.edu/data-samples/access-data/](https://adni.loni.usc.edu/data-samples/access-data/). Knight ADRC data can be obtained by submitting a data request through [https://knightadrc.wustl.edu/data-request-form/](https://knightadrc.wustl.edu/data-request-form/). 

- **Data_extraction/ADNI_KARI_merge_compare.py** - Functions for preprocessing data from ADNI and Knight ADRC and stats comparing ROIs from 2 datasets
  
- **Data_extraction/data_utils.py** - Utility functions related to data extraction
  
- **Data_extraction/ATN_data_extraction.py** - File to be run for the data extraction process. ADNI_KARI_merge_compare.py and data_utils.py are submodules that are called here. 

## Model training

- **Model_training/dataloaders.py** - Dataloader functions for train, test and validation splits
  
- **Model_training/multimodal_VAE.py** - Implements the architecture for mmVAE including the modality-specific encoders and decoders, Product-of-Experts (PoE), and multimodal ELBO loss function
  
- **Model_training/training.py** - mmVAE training.
  - Step 1: Train on healthy controls --> cognitively unimpaired (CDR = 0) amyloid negative participants
  - Step 2: Save trained model
  - Step 3: Calculate deviations on AD patients (amyloid positive) 

## Performance evaluation

- Effect size (Figure 2) - **Results/effect_size.py** 
- Outlier proportion (Figure 3) - **Results/outlier_proportion.py**
- Hamming distance (Figure 4) - **Results/hamming_distance.py**
- Severity staging DSI (Figure 5)- **Results/severity_staging.py**
- DSI associated with cognition (Table 2) - **Results/cognition_association.py**
- DSI related CDR progression (Figure 6)  - **Results/survival_analysis.py**

## Acknowledgement

This work was supported by the Centene Corporation contract (P19-00559) for the Washington University-Centene ARCH Personalized Medicine Initiative and
the National Institutes of Health (NIH) (R01-AG067103). 
  
## Citation
If you find our work is useful in your research, please consider raising a star  :star:  and citing:

```
@article{kumar2025analyzing,
  title={Analyzing heterogeneity in Alzheimer disease using multimodal normative modeling on imaging-based ATN biomarkers},
  author={Kumar, Sayantan and Earnest, Tom and Yang, Braden and Kothapalli, Deydeep and Aschenbrenner, Andrew J and Hassenstab, Jason and Xiong, Chengie and Ances, Beau and Morris, John and Benzinger, Tammie LS and others},
  journal={Alzheimer's \& Dementia},
  volume={21},
  number={4},
  pages={e70143},
  year={2025},
  publisher={Wiley Online Library}
}
```
