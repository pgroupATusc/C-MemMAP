# C-MemMAP

This repo contains code accompaning the manuscript, "C-MemMAP: Clustering-driven Compact, Adaptable, and Generalizable Meta-LSTM Models for Memory Access Prediction"

## Dataset 
The trace uses the PARSEC benchmark(https://parsec.cs.princeton.edu/), generated using Pin tool, see example *Memory Reference Trace* (https://software.intel.com/sites/landingpage/pintool/docs/97503/Pin/html/)

Each application is rerun for three times for inconsistent configuration traces.

## Specialized-Rerun
### Dependencies
* NVIDIA GPU
* TensorFlow v1.0+
* Keras v1.0+

### Preprocessing
First, `cd ./Specialized_Rerun`

Then run `python3 ./Preprocessing.py 200000`, where the argument is the length of deltas sequences.

Preprocessing.py tokenize and binarize the sequence for doubly-compress LSTM training and testing. For each application, T1 and T2 traces are concatenated as training set and T3 is the testing set.

### Speclialized Model Training and Testing
`python3 Train2Test1.py 200000 20`, where argv[1] is the length of sequences and argv[2] is the training epochs.

## Delegated Model Clustering
Run the DM clustering use script `python3 ./Delegated_Model_Clustering.py`

The script uses the DCLSTM models in folder *Specialized_rerun_model*. The model weights of the DCLSTM models are concatenated, dimension reduced using PCA, and clustered using k-means. 

### Meta-DCLSTM
