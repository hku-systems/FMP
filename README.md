# [ICLR'24] Adversarial Feature Map Pruning for Backdoor 
This is the official repo for the paper "Adversarial Feature Map Pruning for Backdoor".


##  :round_pushpin: Abstract

Deep neural networks have been widely used in many critical applications, such as autonomous vehicles and medical diagnosis. However, their security is threatened by backdoor attacks, which are achieved by adding artificial patterns to specific training data. Existing defense strategies primarily focus on using reverse engi- neering to reproduce the backdoor trigger generated by attackers and subsequently repair the DNN model by adding the trigger into inputs and fine-tuning the model with ground-truth labels. However, once the trigger generated by the attackers is complex and invisible, the defender cannot reproduce the trigger successfully then the DNN model will not be repaired, as the trigger is not effectively removed.

In this work, we propose Adversarial Feature Map Pruning for Backdoor (FMP) to mitigate backdoor from the DNN. Unlike existing defense strategies, which focus on reproducing backdoor triggers, FMP attempts to prune backdoor fea- ture maps, which are trained to extract backdoor information from inputs. After pruning these backdoor feature maps, FMP will fine-tune the model with a secure subset of training data. Our experiments demonstrate that, compared to existing defense strategies, FMP can effectively reduce the Attack Success Rate (ASR) even against the most complex and invisible attack triggers (e.g., FMP decreases the ASR to 2.86% in CIFAR10, which is 19.2% to 65.41% lower than baselines). Second, unlike conventional defense methods that tend to exhibit low robust accu- racy (that is, the accuracy of the model on poisoned data), FMP achieves a higher RA, indicating its superiority in maintaining model performance while mitigating the effects of backdoor attacks (e.g., FMP obtains 87.40% RA in CIFAR10).

## :rocket: Updates
**02/20/2024:** Code released

**01/16/2024:** :tada:Our paper is accepted to ICLR'24

## :ballot_box_with_check: How to run FMP for different attack?

### First, generate injected model

Taking badnet attack and cifar10 dataset as a example.
```
python ./attack/badnet_attack.py --yaml_path ../config/attack/badnet/cifar10.yaml --dataset cifar10 --dataset_path ../data --save_folder_name badnet_cifar10
```

### Second, use FMT to repair the DNN model.

```
python ./defense/feature.py  --yaml_path ./config/defense/feature/cifar10.yaml --dataset cifar10 --result_file badnet_cifar10
```

### (Optional) Run baseline approaches~(e.g., FT) for comparisoon.

```
python ./defense/ft/ft.py --result_file badnet_cifar10 --yaml_path ./config/defense/ft/cifar10.yaml --dataset cifar10
```

<br/>

*Please refer to [BackdoorBench](https://github.com/SCLBD/BackdoorBench) for detailed code usage and documentation.*


## :page_facing_up: Citation 
If you found our work useful or inspiring, please consider citing:
```
@inproceedings{
bu2024adversarial,
title={Adversarial Feature Map Pruning for Backdoor},
author={Qingwen Bu and Dong HUANG},
booktitle={The Twelfth International Conference on Learning Representations},
year={2024},
url={https://openreview.net/forum?id=IOEEDkla96}
}
```

## Acknowledgement

Our implementation is built upon [BackdoorBench](https://github.com/SCLBD/BackdoorBench). Thanks for their great work!
```
@inproceedings{backdoorbench,
  title={BackdoorBench: A Comprehensive Benchmark of Backdoor Learning},
  author={Wu, Baoyuan and Chen, Hongrui and Zhang, Mingda and Zhu, Zihao and Wei, Shaokui and Yuan, Danni and Shen, Chao},
  booktitle={Thirty-sixth Conference on Neural Information Processing Systems Datasets and Benchmarks Track},
  year={2022}
}
```
