---
layout: post
title: Kaggle Competition-Understanding the Amazon from Space
github: 'https://github.com/JunhongXu/planet-kaggle-pytorch'
---

This competition asks the competitors to classify each satellite image into multiple classes. This is a multilabel classification problem. The main difficulty in this competition is the data imbalance problem. This problem can be addressed by ensemble methods.

Something I have learned from this competition:

1. Fine-tuning pre-trained models(ResNets, VGGs, Densenets) is better when you have a small or medium amount of data.

2. Ensemble methods (submission ensemble or model ensemble) can improve the result.

3. Augmentation method including test ting augmentation and training time augmentation prevents overfitting.

4. Always check if your predictions are aligned to the submission files.

Solution:

Use pretrained models from:

1. ResNet-34, ResNet-50, ResNet-101, ResNet-151
2. DenseNet-121, DenseNet-161
3. VGG16-BN

Training time augmentation:

1. Horizontal flip
2. Vertical flip
3. Random gaussian noise
4. Random crop.

I have found that using too many data augmentation methods hurts performance, so I just used these four.

Test time augmentation: This is an extremely interesting and useful trick.

1. Horizontal flip
2. Vertical flip

Ensemble:

Weighted majority voting. The weights are learned from a two layer fully connected neural network.

--------------------------------------------------------------------------------

Final result:

Public LB: f2-0.93260, ranking-35

Private LB: f2-0.93078, ranking-unknown

The private on private LB was ~0.57 before aligning the file_xxx and places me around 910. After aligning, I got 0.93078, ranking is approximately 36\. There are others have the same issue, so the ranking may shift down a bit. Too upset that I got really bad score just because I forgot to align the file names. This should be a lesson.
