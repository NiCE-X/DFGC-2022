## Overview
The DFGC-2022 dataset originates from [the Second DeepFake Game Competition ](https://codalab.lisn.upsaclay.fr/competitions/2149#learn_the_details-overview) held with IJCB-2022. This competition provides a common platform for benchmarking the game between the current state-of-the-arts in DeepFake creation and detection methods. The overview of the competition and the dataset can be seen in the following figures and tables. We refer to the competition summary paper for more details. **This dataset has 4394 video clips in total, among which 2799 are face-swap DeepFake videos created with various methods, post-processing, and compressions. Researchers in both face-swap and DeepFake detection may find this dataset useful.** 

![image1](./figs/workflow.png)
<img src="./figs/dataset.png" alt="image2" style="zoom:50%;" />

![image3](./figs/demo.png)

## Application

The dataset is only for non-profit research usage. Applicants need to sign the dataset terms and cite the following research in order to use this dataset.

## The Creation Dataset

It has two sub-folders, *Resource Clips* that include all original clips which are used as resources for creating face-swaps, and *Result Clips* that include all face-swap submissions in the three evaluation rounds of DFGC-2022 creation track.
The *Resource Clips* sub-folder has the following file structure:  ./GroupIndex/ID-Index/ClipIndex.mp4, and it has 20 groups that each containing 2 identities to be mutually face-swapped. The total number of resource clips is 505.

```
Resource Clips  
│
└───1 (Group Index)
│   │
│   └───1 (ID Index)
│   │   │   1.mp4 (Clip Name)
│   │   │   2.mp4
│   │   │   ...
│   │
│   └───2
│       │   1.mp4
│       │   2.mp4
│       │   ...
│   
└─── ...
```

The *Result Clips* sub-folder has the following structure. It has 3 rounds each containing several face-swap submissions from the competition participants or from the organizer baseline. The three txt files *metadata_C1.txt, metadata_C2.txt, metadata_C3.txt* each defines 80 face-swap clips to be made in each submission round. For example, the "1/1/3" means the 3.mp4 of ID-1 in Group-1 needs to be face-swapped (with the ID-2 of Group-1 as the ID donor). The *Method Descriptions.xlsx* file contains descriptions of face-swap methods used to create each submission. The evaluation results for these face-swap submissions can be seen at https://codalab.lisn.upsaclay.fr/competitions/2149#learn_the_details-evaluation.
```
Result Clips  
│   metadata_C1.txt
│   metadata_C2.txt
│   metadata_C3.txt
│   Method Descriptions.xlsx
│
└───Round1 (Round Name)
│   │
│   └───organizer-baseline (Submission Name)
│   │   │
│   │   └───1 (Group Index)
│   │   │   │
│   │   │   └───1 (ID Index)
│   │   │   │   │   3.mp4 (Clip Name)
│   │   │   │   │   7.mp4
│   │   │   │
│   │   │   └───2
│   │   │       │   2.mp4
│   │   │       │   4.mp4
│   │   │
│   │   └─── ...
│   │
│   └───JoyFang-2
│   │   └─── ...
│   └─── ...
│   
└───Round2
│   └─── ...
│
└───Round3
    └─── ...
```
**The dataset users can compare their face-swap methods with DFGC-2022 participants' methods using this dataset, using your preferred evaluation metrics and evaluation methods.**

## The Detection Dataset
The dataset contains two subsets used in the DFGC-2022 competition: the *Public* set that contains 2228 real and fake video clips, and the *Private* set that contains 2166 video clips. The two sets have disjoint IDs. Here we only release the Private-1 part (described in the competition summary paper), since the Private-2 has copyright restrictions. The ground-truth labels are in *Public Label.json* and *Private Label.json*, where the label 0 represents real and 1 represents fake.

```
Detection Dataset  
│   Public Label.json
│   Private Label.json
│   Detection Dataset Meta.csv
│
└───Public
│   │   aaflfhiktb.mp4
│   │   aapifkmrli.mp4
│   │   abbefwjpxv.mp4
│   │   ...
│   
└───Private
    │   ...
```
The file *Detection Dataset Meta.csv* has detailed meta-information for each clip. This csv file is better  viewed in a plain text viewer, and Microsoft Excel is problematic showing some fields as date format. The meta-information includes "videoName", "label", "split", "target", "compression", "face-swap method". The "target" refers to the original resource video (groupIndex/idIndex/clipIndex) that the fake video originates from, or the groupIndex/idIndex that the real video originates from. Here, a real video may not correspond exactly to a resource video clip, hence we only narrow down to the idIndex. The "compression" refers to the quality of ffmpeg compression we conduct on submitted videos: "c40", "c23", "none" are respectively 
heavy compression, light compression and no compression. The "face-swap method" only applies to fake videos that refers to the submission identifier from the creation track. Refer to the *Result Clips* in the creation dataset.

**The dataset users can use this dataset to train or test their DeepFake detection models or methods.**

