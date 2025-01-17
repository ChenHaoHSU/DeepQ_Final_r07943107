# Machine Learning Final Project (2019, Spring)

**by NTU_r07943107_**

RSNA Pneumonia Detection Challenge (DeepQ Challenge)

Kaggle: [link](https://www.kaggle.com/c/ml2019spring-final-deepq/overview).

## Directory Structure

- `src/`: folder of source code including all `.py` files
- `requirements.txt`: python3 package requirements. Please try to install all the packages listed.
- `data_setup.sh`: script to set up the environments for dataset, not packages.
- `train_50.sh`: script to train model with Resnet50 as backbone.
- `train_101.sh`: script to train model with Resnet101 as backbone.
- `train_152.sh`: script to train model with Resnet152 as backbone.
- `test.sh`: script to make inferences. Before making any inferences, please make sure that the environments are set up properly.
- `reproduce.sh`: script to reproduce the result on kaggle.
- `settings.json`: json file for all file path settings.
- `report.pdf`: report.

## Software 
(python3 packages are detailed separately in `requirements.txt`):

- Python 3.6.x (required)
- Ubuntu 18.04 LTS or CentOS 7 (optional)
- CUDA 9.0 (optional)
- cuDNN 7.0.5 (optional)
- NVIDIA driver v.390.116 (optional)

## Data and Keras-retinanet Setup

- **Data setup**: Run the following shell commands from the top level directory
```
bash ./data_setup.sh  [train_png_dir]  [test_png_dir]  [train_label_csv]  [train_metadata_csv]  [test_metadata_csv]
```

Example:
```
bash ./data_setup.sh ./data/train ./data/test ./data/train_labels.csv ./data/train_metadata.csv ./data/test_metadata.csv
```

`settings.json` should be well configured after running the above command.

- **Keras-retinanet setup**: Run the following shell commands from the top level directory
```
cd src/keras-retinanet
python3 setup.py build_ext --inplace
cd ../../
```

## Model Training

There are three different RetinaNets used as backbones in our solution, which are trained by the following scripts.

- Use Resnet-50 as backbone:
```
bash ./train_50.sh
```

- Use Resnet-101 as backbone:
```
bash ./train_101.sh
```

- Use Resnet-152 as backbone:
```
bash ./train_152.sh
```

Snapshots after each epoch of training are saved in `snapshots/`.

Note: we used Resnet-50 as backbone in our best model on [kaggle](https://www.kaggle.com/c/ml2019spring-final-deepq/overview).

## Prediction

Move the inference models to `models/` and modify "MODELS" in `settings.json`. Then, run the following command. 

Usage:

	bash ./test.sh [prediction_path]

Example:

	bash ./test.sh prediction.csv

Prediction is saved to `prediction_path` in run-length encoding (RLE) format.

## Reproduce

To reproduce the result on kaggle, run the following command.

Usage:

	bash ./reproduce.sh [prediction_path]

Example:

	bash ./reproduce.sh prediction.csv

Prediction is saved to `prediction_path` in run-length encoding (RLE) format.

## References

1. 3rd place solution in RSNA Pneumonia Detection Challenge. [Github](https://github.com/pmcheng/rsna-pneumonia)
2. T.-Y. Lin, P. Goyal, R. Girshick, K. He, and P. Dollar, "Focal loss for dense object detection," In ECCV, 2017.
