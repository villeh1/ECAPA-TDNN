## Introduction

This repository contains unofficial code to train the [standard ECAPA-TDNN](https://arxiv.org/pdf/2005.07143.pdf) for speaker recognition in VoxCeleb2 dataset.

This repository is modified based on [voxceleb_trainer](https://github.com/clovaai/voxceleb_trainer)

Advantages of this repository: 

1) Simple: 6 python files with 600 lines.

2) Fast:  36 hours to train by one 3090 GPU 

3) Robust: EER = 0.86 in VoxCeleb1

## Best Performance in this project (with AS-norm)

| Dataset |  Vox1_O  |  Vox1_E  |  Vox1_H  |
| ------- |  ------  |  ------  |  ------  |
|  EER    |   0.86   |  1.18    |  2.17    |
|  minDCF |  0.0686  | 0.0765   |  0.1295  |

***

## System Description

I will write a technique report about this system and all the details later. Please wait.

### Dependencies

Start from building the environment
```
conda create -n ECAPA python=3.7.9 anaconda
conda activate ECAPA
pip install -r requirements.txt
```

Start from the existing environment
```
pip install -r requirements.txt
```

### Data preparation

Please follow the official coda to perpare your VoxCeleb2 dataset from [here](https://github.com/clovaai/voxceleb_trainer), the 'Data preparation' part. Please read that part carefully and make sure you do it correctly.

Dataset you need to perpare for training: 1) VoxCeleb2 training set, 2) MUSAN dataset, 3) RIR dataset.

Dataset you need to perpare for evaluation: 1) VoxCeleb1 test set (Vox1_O, Compulsory), 2) VoxCeleb1 train set (Vox1_E and Vox1_H, Optional).

### Training

Change the data path in the `trainSpeakerNet.py`, then you can train ECAPA-TDNN model for speaker recognition end-to-end by using:

```
python trainSpeakerNet.py --save_path exps/exp1 
```

In every `test_step` epoches, system will be evaluated in Vox1_O set and print the EER. The result will be saved in `exps/exp1/score.txt`, the model will saved in `exps/exp1/model`

### Pretrained model

Our pretrained model performs `EER: 0.96` in Vox1_O set without AS-norm, you can download our pretrain model you can check it by using: 
```
python trainSpeakerNet.py --eval --initial_model pretrain.model
```

With AS-norm, this system performs `EER: 0.86`, we will release the code of AS-norm later.

***


### Reference

```
@article{desplanques2020ecapa,
  title={Ecapa-tdnn: Emphasized channel attention, propagation and aggregation in tdnn based speaker verification},
  author={Desplanques, Brecht and Thienpondt, Jenthe and Demuynck, Kris},
  journal={arXiv preprint arXiv:2005.07143},
  year={2020}
}
@inproceedings{chung2020in,
  title={In defence of metric learning for speaker recognition},
  author={Chung, Joon Son and Huh, Jaesung and Mun, Seongkyu and Lee, Minjae and Heo, Hee Soo and Choe, Soyeon and Ham, Chiheon and Jung, Sunghwan and Lee, Bong-Jin and Han, Icksang},
  booktitle={Interspeech},
  year={2020}
}
```

### Acknowledge

We study many useful projects in our codeing process, which includes:

[clovaai/voxceleb_trainer](https://github.com/clovaai/voxceleb_trainer).

[lawlict/ECAPA-TDNN](https://github.com/lawlict/ECAPA-TDNN/blob/master/ecapa_tdnn.py).

[speechbrain/speechbrain](https://github.com/speechbrain/speechbrain/blob/96077e9a1afff89d3f5ff47cab4bca0202770e4f/speechbrain/lobes/models/ECAPA_TDNN.py)

[ranchlai/speaker-verification](https://github.com/ranchlai/speaker-verification)

Thanks for these authors to open source their code!

If you have any questions about this project, please ask me from the 'issue' part (Please do not ask me though any social media, thanks!)