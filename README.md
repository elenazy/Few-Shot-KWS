Code Repository for the paper [Few-Shot Keyword Spotting with Prototypical Networks](https://arxiv.org/abs/2007.14463).

![Few-Shot Keyword Spotting Pipeline](figures/Pipeline.png)


# Installation

1. Clone the repository:  

    ```
    git clone https://github.com/ArchitParnami/Few-Shot-KWS 
    ``` 

2.  Create a conda environment:

    ```
    conda create -n FS-KWS
    ```

3.  If pip not installed, install pip by:

    ```
    conda install pip
    ```

4.  Install the required packages:

    ```
    pip install -r requirements.text
    ```

5.  Install the protonets package:

    ```
    cd Few-Shot-KWS
    python setup.py develop
    ```

# Download & Prepare Few-Shot Keyword Spotting Dataset

```
cd Few-Shot-KWS/data/
python download_prepare_data.py
```
# Train

To train a simple 2-way 1-shot experiment.

```
cd Few-Shot-KWS/scripts/train/few-shot/fewshotspeech
./train.sh 2 1 0 mymodel
```
Specify arguments to train.sh in the following manner

train.sh num_ways num_shots exp_type exp_id

- num_ways  
    + Number of classes
    + Eg. 2 or 4
- num_shots
    + Number of samples per class.
    + Eg. 1,5
- exp_type
    + Number indicating the type of experimental setup
        - 0 = Simple N-Way K-Shot Setup. No background, silence or unknown keywords.
        - 1 = Include Background
        - 2 = Include Silence
        - 3 = Include Unknown 
        - 4 = Background + Silence 
        - 5 = Background + Unkown
        - 6 = Unknown + Silence
        - 7 = Background + Silence + Unknown
- exp_id
    + identifier = directory name
    + results are saved in `Few-Shot-KWS/scripts/train/few-shot/fewshotspeech/results/[exp_id]`


# Evaluate

```
cd Few-Shot-KWS/scripts/predict/few-shot
python eval_results.py ../../train/few_shot/fewshotspeech/results/
```

The evaluation can be found in:  
```
cat Few-Shot-KWS/scripts/train/few-shot/fewshotspeech/results/[exp-id]/[timestamp]/eval.txt
```

# Results

Comaring test accuracy of different embedding networks on 4-way FS-KWS as we increase the number of support examples. The results are presented for four different cases discussed in the paper.

![](results/performance-Core.png) ![](results/performance-Core+Background.png)

![](results/performance-Core+Unknown.png) ![](results/performance-Core+Unknown+Background+Silence.png)


# References

The code in this repository has been adapted from:

1. https://github.com/jakesnell/prototypical-networks
2. https://github.com/hyperconnect/TC-ResNet
3. https://github.com/tensorflow/docs/blob/master/site/en/r1/tutorials/sequences/audio_recognition.md


# Citation
```
@misc{parnami2020fewshot,
    title={Few-Shot Keyword Spotting With Prototypical Networks},
    author={Archit Parnami and Minwoo Lee},
    year={2020},
    eprint={2007.14463},
    archivePrefix={arXiv},
    primaryClass={eess.AS}
}
```
