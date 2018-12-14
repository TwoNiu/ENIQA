# ENIQA: Entropy-based No-reference Image Quality Assessment

![framework](https://github.com/jacob6/ENIQA/blob/master/pics/framework.png)

## Abstract

> This paper presents a high-performance general-purpose no-reference (NR) image quality
assessment (IQA) method based on image entropy. The image features are extracted from two
domains. In the spatial domain, the mutual information between the color channels and the
two-dimensional entropy are calculated. In the frequency domain, the two-dimensional entropy
and the mutual information of the filtered sub-band images are computed as the feature set
of the input color image. Then, with all the extracted features, the support vector classifier
(SVC) for distortion classification and support vector regression (SVR) are utilized for the
quality prediction, to obtain the final quality assessment score. The proposed method, which
we call Entropy-based No-reference Image Quality Assessment (ENIQA), can assess the quality
of different categories of distorted images, and has a low complexity.  

## Authors

Guangyi Yang, Qingyi Zhang, Manhui Lin, Deshi Li, and Chu He, Member, IEEE

## Experiments

All experiments are carried out on Matlab R2016a on 64-bit Windows 7 and the detailed
results are given in the paper. The codes are also testified on Ubuntu 16.04 with
Matlab R2016b and work well.

Two IQA datasets, [LIVE](http://live.ece.utexas.edu/research/quality/subjective.htm) and
[TID2013](http://www.ponomarenko.info/tid2013.htm), are used in out experiments.

This table shows the good performance of ENIQA compared with several classical NR and FR
IQA methods

MEDIAN SROCC VALUES ON THE LIVE DATABASE
|Method|JP2K|JPEG|WN|GBlur|FF|All|
|:----:|:--:|:--:|:-:|:--:|:-:|:-:|
|PSNR|0.9053|0.8866|**0.9844**|0.8120|0.8981|0.8850|
|SSIM|**0.9517**|**0.9671**|0.9631|0.9306|0.9404|0.9255|
|VIF|0.9160|0.9482|0.9435|**0.9600**|**0.9617**|**0.9287**|
| | | | | | | |
|BIQI|0.8401|0.8425|0.9362|0.8924|0.7383|0.8340|
|DIIVINE|<u>0.9363</u>|0.9051|0.9692|0.9478|0.8778|0.9261|
|BLIINDS-II|**0.9389**|0.9449|0.9596|0.9447|0.8653|0.9362|
|BRISQUE|0.9349|0.9480|0.9725|<u>0.9616</u>|0.8821|**0.9411**|
|NIQE|0.9171|0.9094|0.9697|**0.9678**|0.8715|0.9142|
|ILNIQE|0.9199|0.9335|<u>0.9730</u>|0.9526|**0.8991**|0.9219|
|SSEQ|0.9355|**0.9509**|0.9689|0.9554|<u>0.8943</u>|0.9349|
|ENIQA|0.9333|<u>0.9485</u>|**0.9808**|0.9531|0.8568|<u>0.9363</u>|

## Usage

For evaluating, we provide two ways:
You can first load the RGB image and then calculate the score by

```MATLAB
img = imread(img_path);
score = ENIQA(img);
```

or simply input the path of the image

```MATLAB
score = ENIQA(img_path);
```

For training a new model on LIVE, try `crossValidationOnLIVE`

For cross-database evaluation, try `testOnTID2013`

To do this, you have to prepare a model pretrained on another dataset.

## Pretrained models

We have trained a model on the whole LIVE dataset and you can find it on ENIQA_release/model.

## Dependencies

libSVM, explicitly the mex files, is required to perform the classification and regression.
You can download it from [here](https://www.csie.ntu.edu.tw/~cjlin/libsvm/).
