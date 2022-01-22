# Coughvid-19-CRNN-attention
**For Vietnamese student, you can read the `Nhận diện covid qua tiếng ho.pdf` and `Covid19_slide.pdf` which is written in Vietnamese. For foreign reader, I wrote all the important information in `coughvid-19-crnn-attention.ipynb`, `Mechanism of cough.pptx`, and my Git Repo [COVID-19-Cough-Classification-phase-1](https://github.com/mrzaizai2k/COVID-19-Cough-Classification-phase-1-#covid-19-cough-classification-phase-1)**

The Kaggle notebook: https://www.kaggle.com/bomaich/coughvid-19-crnn-attention

You may find the advantages of the Covid classification system based on cough sound, the background technique like scaling, K-fold... or the way I implemented it in **my Git  [COVID-19-Cough-Classification-phase-1](https://github.com/mrzaizai2k/COVID-19-Cough-Classification-phase-1-#covid-19-cough-classification-phase-1)**. But the last git has some huge flaws due to the lack of experiences about cough or I have to depend much on the processed dataset (not sound files). In this Git, I recommend reading this Git in conjunction with `coughvid-19-crnn-attention.ipynb`  


## Table of contents
* [1. Cough mechanism](#1-Cough-mechanism)
* [2. Primary features](#2-Primary-features)
* [3. Scaling data](#3-Scaling-data)
* [4. Imbalanced data](#4-Imbalanced-data)
* [5. Model](#5-Model)
* [6. K - fold cross validation](#6-K-fold-cross-validation)
* [7. Result](#7-Result)

## 1. Cough mechanism
I won't talk much about this part cause you can have detail information in `Mechanism of cough.pptx` and this [Cough sound analysis and objective correlation with spirometry and clinical diagnosis](https://www.researchgate.net/publication/340025267_Cough_sound_analysis_and_objective_correlation_with_spirometry_and_clinical_diagnosis). To sum up, different diseases create different coungh sounds. And those sounds are different with:
* The enery of cough sequence, 
* The energy distribution between cough bouts 
* The sound of breath
* The duration of the coough or breath 
and so on 

So I discovered the author of the dataset of **my last Git [COVID-19-Cough-Classification-phase-1]** calculate the mean value of all the features on all of the time series, which was a significant error. Like we just have one ZCR mean value on the whole sound. It's not logical because ZCRs are often utilized in association with energy to determine when there is sound and when there is quiet 
>"The results suggest that zero crossing rates are low for voiced part and high for unvoiced part where as the energy is high for voiced part and low for unvoiced part."

[Separation of Voiced and Unvoiced using Zero crossing rate and Energy of the Speech Signal](https://www.researchgate.net/publication/259828967_Separation_of_Voiced_and_Unvoiced_Speech_Signals_using_Energy_and_Zero_Crossing_Rate)

**From the base knowledge, I decided to use CRNN (Because of it's outperformance inn dealing with series data) and preprocess features in a different way**

## 2. Primary features
The feature extracted in this project were MFCCs, Mel frequency spectrogram, chroma and those are mean value `np.mean`. 

<p align="center"><img src="result/oversamp_AUC.PNG" width="500"></p>
<p align="center"><i>Figure 4. AUC = 93% with SMOTE </i></p>
