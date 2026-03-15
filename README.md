# DyProL: Protein interaction prediction benefits from learning dynamic conformational ensembles

## 1 Introduction
DyProL is a deep learning framework for predicting nucleic acid–binding residues on proteins by integrating protein structural dynamics.  
Unlike traditional static structure–based methods, DyProL models protein conformational ensembles and learns dynamic structural representations using geometric deep learning. The framework supports both static structures and multi-conformation dynamic ensembles generated from molecular simulations or structure prediction models.

## 2 Installation
### 2.1 Clone the repository
```
git clone https://github.com/yiman-liu/DyProL.git
cd DyProL
```
### 2.2 Create environment
We recommend using conda.
```
conda create -n dyprol python=3.9
conda activate dyprol
```
### 2.3 Install dependencies
```
pip install torch
pip install numpy
pip install scipy
pip install scikit-learn
pip install tqdm
pip install joblib
pip install biopython
pip install MDAnalysis
pip install fair-esm
```
If GPU training is needed, please install the appropriate CUDA version of PyTorch.
### 3 Dataset Preparation
### 3.1 Download dataset
The datasets can be downloaded from Zenodo:
```
wget https://zenodo.org/record/XXXXXXX/files/DyProL_datasets.tar.gz
```
Extract the dataset:
```
tar -xvf DyProL_datasets.tar.gz
```
### 3.2 Directory structure
Place the dataset under the project directory as follows:
```
DyProL
│
├── script
│   ├── train.py
│   ├── model.py
│   ├── Arguments.py
│   └── dataloader
│
├── Datasets
│   ├── DNA
│   │   ├── DNA-1022_Train.txt
│   │   └── DNA-256_Test.txt
│   │
│   ├── RNA
│   │   ├── RNA-932_Train.txt
│   │   └── RNA-234_Test.txt
│   │
│   └── GraphBind
│       ├── DNA
│       │   ├── DNA-573_Train.txt
│       │   └── DNA-129_Test.txt
│       └── RNA
│           ├── RNA-495_Train.txt
│           └── RNA-117_Test.txt
```
The code automatically loads datasets using relative paths, so the dataset only needs to be placed inside the Datasets/ directory.
### 4 Training
Training is performed using train.py.
### 4.1 Train on DNA dataset from DyProL
```
python train.py --ligand DNA --data_source dyprol --dynamic dynamic
```
### 4.2 Important arguments
Argument	Description
```
ligand                  -> Ligand type (DNA or RNA)
dynamic                 -> Structure type (static or dynamic)
checkpoints_dir         -> Where the log and model save
ensemble                -> Which ensemble method to use.(esmdiff or bioemu or esmflow  or alphaflow)
data_source             -> Dataset source (dyprol or graphbind)
train_file              -> Path to training set file. If not set, it will be chosen automatically from ligand. If you want to train on other datasets, please enter the real path, eg:/home/lym/DyProL/Datasets/DNA/DNA-1022_Train.txt
test_file               -> Path to test set file. Ditto.
PDB_dir                 -> Path to PDB directory for static model. If not set, it will be generated automatically from ligand.If you want to train on other datasets, please put the PDB directory to the PDB_dir, eg:/home/lym/DyProL/Datasets/DNA/PDB
PDB_dir                 -> Path to XTC directory for dynamic model. Ditto.If you want to train on other datasets, please put the PDB directory to the PDB_dir, eg:/home/lym/DyProL/Datasets/DNA/output
cluster_method          -> Clustering method for dynamic pdbs. (DBSCAN or KMeans or hierarchical or random)
use_llm                 -> Whether to use ESM for llm or not.
n_cluster               -> Number of clusters for dynamic pdbs for the method of KMeans or hierarchical or random clustering.
device                  -> Which gpu/cpu to train on.
n_layers_structure      -> Number of convolutional layers.
emb_dims                -> Number features of hidden layers.
batch_size              -> Number of proteins in a batch.
seed                    -> Random seed.
lr                      -> Learning rate.
```
## 5 Citation
If you use DyProL in your research, please cite:
Author et al.
DyProL: Dynamic Protein Learning for Binding Site Prediction.



