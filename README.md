## SICK-TR 1.0  (Sentences Involving Compositional Knowledge benchmark Turkish)

English SICK benchmark dataset translated into Turkish using Google Cloud Translation API. No human corrections have been made to the translations. There are **4500** pairs in the train split, **500** in the trial split used for development and **4927** in the test split. 

**Note:** we have used the version of SICK dataset which is available in [SentEval toolkit](https://github.com/facebookresearch/SentEval)


## Discription about SICK benchmark

The Sentences Involving Compositional Knowledge (SICK) dataset is a dataset for compositional distributional semantics. It includes a large number of sentence pairs that are rich in the lexical, syntactic and semantic phenomena. Each pair of sentences is annotated in two dimensions: relatedness and entailment. The relatedness score ranges from 1 to 5. The entailment relation is categorical, consisting of entailment, contradiction, and neutral. 

## Downloading dataset


## Reading dataset

#---------------------------
# SICK-dataset reader
import re
import json
import os
import numpy as np

class SICKReader():  
  def __init__(self, filepath):
    self.filepath = filepath
    self.filename = {}
    self.filename['train'] = 'SICK_train_tr.txt'
    self.filename['test']  = 'SICK_test_tr.txt'
    self.filename['trial'] = 'SICK_trial_tr.txt'
    self.label2index = {'CONTRADICTION': 0.0 , 'NEUTRAL': 1.0 ,  'ENTAILMENT': 2.0}

  def get_data(self, data_split ):
    id, x1 , x2 , annotator_labels , scores , labels, all_data = [] , [] , [] , [] , [], [], []
    kk=-1
    with open(os.path.join(self.filepath, self.filename[data_split]), 'r') as f:
      next(f)
      for line in f:
          line=(line.rstrip().split("\t"))
          id.append((line[0]))
          x1.append ((line[1]))
          x2.append ((line[2]))
          labels.append(self.label2index[line[4]])
          scores.append (float(line[3]))
          annotator_labels.append(line[4])

      [all_data.append([id[i], x1[i], x2[i], labels[i], scores[i], annotator_labels[i]]) for i in range(len(id)) ]   

    return id, x1, x2, labels, scores, annotator_labels, all_data

  def get_label2index(self):
      return self.label2index 


path_SICK =   '/content/gdrive/My Drive/Colab Notebooks/dataset_raw/sick/sick_tr'

sick_reader = SICKReader(path_SICK)
data_split = ['train' , 'test', 'trial']


id, sent_1 , sent_2 , labels  , scores , annotator_labels , all_data  = sick_reader.get_data (data_split[0])

all_data[0]
                  
