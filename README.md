hateful_memes
======================================

## Contents
input2/: download dataset and unzip it here.

model/: The whole code(*.ipynb) and some output files. You can delete all the other files since ipynb will generate them.
1.  Run pre.ipynb to preprocess.
2.  you can download all the weight files to the folder weights and run model7/model8/model12.ipynb to reproduce the result. Or you can train all models by setting the ISPREDICT = False.
3.  Run merge.ipynb to merge and postprocess output files.

mmf/: use mmf to predict dev and test here.   
1.  Install mmf as https://github.com/facebookresearch/mmf/tree/master/projects/hateful_memes .
2.  Run mmf_convert_hm --zip_file=x --password=y where you replace x with location of your zip file and y with the password you noted.
3.  Run mmf_predict config=projects/hateful_memes/configs/visual_bert/from_coco.yaml model=visual_bert dataset=hateful_memes run_type=val checkpoint.resume_zoo=visual_bert.finetuned.hateful_memes.from_coco checkpoint.resume_pretrained=False dataset_config.hateful_memes.annotations.val[0]=hateful_memes/defaults/annotations/dev_seen.jsonl. Rename the output file as coco_output.csv.  
4.  Run mmf_predict config=projects/hateful_memes/configs/visual_bert/from_coco.yaml model=visual_bert dataset=hateful_memes run_type=val checkpoint.resume_zoo=visual_bert.finetuned.hateful_memes.from_coco checkpoint.resume_pretrained=False. Rename the output file as coco_output2.csv.
5.  Run mmf_predict config=projects/hateful_memes/configs/visual_bert/from_coco.yaml model=visual_bert dataset=hateful_memes run_type=test checkpoint.resume_zoo=visual_bert.finetuned.hateful_memes.from_coco checkpoint.resume_pretrained=False dataset_config.hateful_memes.annotations.test[0]=hateful_memes/defaults/annotations/test_seen.jsonl. Rename the output file as coco_sub.csv.  
6.  Run mmf_predict config=projects/hateful_memes/configs/visual_bert/from_coco.yaml model=visual_bert dataset=hateful_memes run_type=test checkpoint.resume_zoo=visual_bert.finetuned.hateful_memes.from_coco checkpoint.resume_pretrained=False. Rename the output file as coco_sub2.csv.

coco_sub2 is used to final submission and other three files would be used as validation.


## Solution

This solution implies some networks to predict difference of hateful between samples.  
Here is a simple description about our models.  


script | simple later fusion model |  pairloss model | bias model |  max length of text 
-|-|-|-|-
model7.ipynb | √ | √ | |96|
model8.ipynb | √ | √ | |64|
model12.ipynb |  | √ | √ |96 |
mmf | | | | |  

At last, merge.ipynb considers predictions of pairs data and reconstruct the distribution of the results.

## Contributor

Zhenzhe Ying, 443407384@qq.com  
Jun Lan, lanjun_yelan@163.com  
Haotian Wang, 1031821435@qq.com  

