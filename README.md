# Illumination-Based Data Augmentation for Robust Background Subtraction

This repository contains the Keras code used in the paper [Illumination-Based Data Augmentation for Robust Background Subtraction](http://nrl.northumbria.ac.uk/40944/1/Sakkos%20et%20al%20-%20Illumination-Based%20Data%20Augmentation%20for%20Robust%20Background%20Subtraction%20AAM.pdf),
which received the **Best paper award** at [**SKIMA 2019**](http://skimanetwork.info/) which was held from 26 to 28 August 2019 in Island of Ulkulhas, Maldives. 


# SABS dataset
The dataset used in this study was developed by [Stuttgart University](https://www.vis.uni-stuttgart.de/forschung/visual-analytics/visuelle-analyse-videostroeme/stuttgart_artificial_background_subtraction_dataset/).
For training the models the *Darkening* video sequence was used, while the test set consists of the *LightSwitch* video.

# Training

Once the dataset has been downloaded, it needs to be extracted in the same directory as the source code files and placed in a folder named `SABS`, which should contain the *Darkening* and *LightSwitch* subfolders.

To use the VGG16 pre-trained backbone, you can download the weights from [this link](https://github.com/fchollet/deep-learning-models/releases/download/v0.1/vgg16_weights_tf_dim_ordering_tf_kernels_notop.h5) and save the file in the working directory.

You are then ready to run the `train.py` script to start training, which accepts various self-explanatory arguments. All of these have pre-determined values for your convenience.
To use the proposed illumination augmenter, provide the *augment_local* and *augment_global* arguments followed by the minimum and maximum pixel values of the mask intensity.
For example, to train a model with a VGG16 backbone and the proposed augmentation method, run the script as follows:

```
python train.py \
    --model_name vgg16_augmented \
    --backbone vgg16 \
    --augment_local 120 160 \
    --augment_global 40 80 \
    --augment_regular False
```

The training arguments will be saved at your working folder, to ease the tracking of your experiments. To turn off the proposed method and use the regular augmentor instead, run the following:

```
python train.py \
    --augment_local 0 0 \
    --augment_global 0 0 \
    --augment_regular True
```


# Testing
For evaluating a trained model, you need to provide the filename of the trained model.
Optionally, you can save the predictions, set a different binarisation threshold and control the depiction of a progress bar as follows:

```
python test.py \
    --model_name vgg16_augmented \
    --threshold 0.7 \
    --save_results False \
    --verbose True
```

# Notes
During training, the script will monitor, for each epoch, the F1 score on the validation set and overwrite the saved model in case of improvement.
Training stops after a number of consecutive epochs of no improvement, which is pre-set as 15.

## Citation

If you use this code in your research, please use the following BibTeX entry.

````
@inproceedings{sakkos2019illumination,
  title={Illumination-Based Data Augmentation for Robust Background Subtraction},
  author={Sakkos, Dimitrios and Shum, Hubert and Ho, Edmond},
  booktitle={SKIMA},
  year={2019}
}
```` 

## Contact
For any questions or discussions, you can contact me at dksakkos@gmail.com.