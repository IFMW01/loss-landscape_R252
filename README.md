# Explicit Regularisation, Sharpness and Calibration. 

## Setup

Conda environment:

```
conda create --prefix r252-env python=3.8
conda activate path/to/here/r252-env
```

Install PyTorch:

```
pip install torch torchvision torchaudio --extra-index-url https://download.pytorch.org/whl/cu113
```

Install other requirements

```
pip install -r requirements.txt
```

## Calculating Sharpness Measures

To calculate sharpness measures for an arbitrary classification network, simply instanciate the `MetricsProcessor` class found in `src/trainers/metrics_processing.py` with the trained model and data loaders. Then call `.sharpness_metrics()`. Which sharpness measures are calculated can be configured with a config object passed to `MetricsProcessor`.

## Experiments

Specify in the config which metrics/measures to compute. To replicate our results, run the following for CIFAR10 and CIFAR100:

```
python main.py \
    --config_file ../configs/base_config.yaml \
    --model_name VGG19 \
    --baseline True \
    --dataset CIFAR10  \
    --save_name baseline 

python main.py \
    --config_file ../configs/reliability_plots.yaml \
    --model_name VGG19 \
    --baseline True \
    --aug True \
    --dataset CIFAR10  \
    --save_name baseline_augmentations 

python main.py \
    --config_file ../configs/base_config.yaml \
    --model_name VGG19 \
    --baseline True \
    --dropout 0.5 \
    --dataset CIFAR10  \
    --save_name baseline_dropout_0_5

python main.py \
    --config_file ../configs/base_config.yaml \
    --model_name VGG19 \
    --baseline True \
    --weight_decay 5e-4 \
    --dataset CIFAR10  \
    --save_name baseline_weight_decay_0_0005

```


Repository from the Visualizing Loss Landscapes Paper to visualise loss landscape results (src/vizualisation)

```
@inproceedings{visualloss,
  title={Visualizing the Loss Landscape of Neural Nets},
  author={Li, Hao and Xu, Zheng and Taylor, Gavin and Studer, Christoph and Goldstein, Tom},
  booktitle={Neural Information Processing Systems},
  year={2018}
}
```
