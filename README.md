

<div align="center">
<a href="http://camma.u-strasbg.fr/">
<img src="https://github.com/CAMMA-public/rendezvous/blob/main/files/CammaLogo.png" width="18%">
</a>
</div>
<br/>

[![](https://img.shields.io/badge/IN-PROGRESS-blue?style=for-the-badge)](https://hamzamohdzubair.github.io/redant/)

# CholecTriplet2022
CholecTriplet 2022 challenge on surgical action triplet detection

<i>C.I. Nwoye, A. Murali, S. Sharma, T. Yu, K. Yuan, D. Alapatt, A. Vardazayan, and N. Padoy</i>


![t50-logo-2022](https://user-images.githubusercontent.com/18656978/175311642-1781509a-b292-4e07-9e99-c043be7ee20c.png)


This repository contains some implementation code: mock demo model, data loader, docker build guides, self-validator system, and evaluation scripts.

<br>


## <u>Getting started</u>
All information about the challenge can be found on the Grand-challenge [website](https://cholectriplet2022.grand-challenge.org).


<br>


## Data loader
- [TensorFlow dataloader](https://github.com/CAMMA-public/cholect45/blob/main/dataloader_tf.py)
- [PyTorch dataloader](https://github.com/CAMMA-public/cholect45/blob/main/dataloader_pth.py)

© [Cholect45 Git Repo](https://github.com/CAMMA-public/cholect45)

## Practice on sample data
Easy starting code of simple model in TensorFlow or PyTorch on small sample data from CholecT50.
- Open in [Colab](https://colab.research.google.com/github/CAMMA-public/cholectriplet2022/blob/main/Getting_Started.ipynb)

<br>


## Evaluation metrics
```
  pip install ivtmetrics
```
 or 
 ```
  conda install -c nwoye ivtmetrics
```

<br>


## Docker and validation guide

- Detailed instruction to build, test, validate, and run your method Docker on the challenge Dockerhub in provided [here](docker.md)


<br>

## Submission protocol
- Follow the [guide](submit.md) to upload your final Docker image.
- Visit the [submission page](https://cholectriplet2022.grand-challenge.org/submission/) to submit your challenge reports

<br>
<br>


## Organizer's Baseline Method

The `Rendezvous (RDV)` for surgical action triplet recognition is modified to produce bounding boxes for the instrument tip of every recognized triplet.

This is made possible by the weakly supervised localization (WSL) aspect of the RDV.
The WSL branch in `RDV`'s encoder is responsible for instrument detection. It is trained on instrument's binary presence labels only. The localization is done via the resulting class activation map (CAM). We added an `adhoc function` to extract the bounding box coordinates for every positive  activation in this layer.

The classifier in the `RDV`'s decoder  produces a vector of probility scores for the triplet class prediction. We extend this with a `heuristic function` to associate every extracted instrument bounding boxes to the corresponding triplet instance within a given frame.

Model produces both vector of classwise probability scores for triplet recognition + bounding boxes of the instruments paired to positive triplet classes. The output can be formatted as a `list of list (lol)` or `list of dict (lod)` for each frame containing several instance triplet-box predictions.
Full video prediction can be saved as a .`TXT` file or as a .`JSON` file

Rendezvous_Det code and weights is provided [here]().

**Requirements:**
- PIL
- Python >= 3.5
- Pyorch >= 1.10.1
- TorchVision >= 0.11
- ivtmetrics


**To Run**

You need to map input/ and output/ directories to the corresponding input/ and output/ directories in the organizer's host folder.

```
    cd ..
    cd rendezvous_det
    python3 main.py \
		--input_dir=/path/to/organizer's/input/data \
		--output_dir=/path/to/organizer's/output/results \
		--gpu='0'
```
Results are saved as .JSON in the output folder.

*During Docker run, the input_dir and output_dir should be default as in the argparse field.*
	

**To evaluate performance**

To see the model performance, execute thr following commands:
```   
    cd ..
    cd $HOST/validator
    python3 eval.py --gt_dir=/path/to/groundtruth --pd_dir=/path/to/predictions --log_dir=/path/to/write/results --threshold 0.5
```


## Participants Code
Participants can release their code on their own discretion. All released code would appear here:

| Method | Team | Institution | Repository |
|--------|------|-------------|------------|
| 1. RDV-Det | CAMMA | University of Strasbourg, France | [GitHub](https://github.com/CAMMA-public/rendezvous)| 
| 2. AtomTKD | SHUANGCHUN | Southern University of Science and Technology, China | Link unavailable| 
| 3. DATUM | KLIV-IITKGP | Indian Institute of Technology Kharagpur, India | Link unavailable| 
| 4. Distilled-Swin | SDS-HD | German Cancer Research Center (DKFZ), Germany  | Link unavailable| 
| 5. DualMFFNet | SK | Muroran Institute of Technology, SK, Japan  | Link unavailable| 
| 6. EnoSurgTRD | INTUITIVE-CORTEX-ML | Intuitive Surgical, USA | Link unavailable| 
| 7. IF-Net | CAMP | Technical University Munich, Germany | Link unavailable| 
| 8. MTTT | CITI | Shanghai Jiao Tong University, China  | Link unavailable| 
| 9. ResNet-CAM-YOLOv5 | WINTEGRAL | Wintegral GmbH, Germany  | Link unavailable| 
| 10. SurgNet | 2AI-ICVS | Applied Artificial Intelligence Laboratory, Portugal  | Link unavailable| 
| 11. URN-Net | URN | University College London, UK  | Link unavailable| 


---
Maintainer @ camma 2022
