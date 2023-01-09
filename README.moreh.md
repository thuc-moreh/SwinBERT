# [Moreh] Running Swin-BERT on Moreh AI Framework
![](https://badgen.net/badge/Moreh-HAC/failed/red)

## Prepare

### Data
- The video for demo inference is already included in the repo
- Data for training and evaluation have to be downloaded from source due to copyright issues. The video for demo inference is enough to reproduce the below errors

### Code
```bash
git clone https://github.com/microsoft/SwinBERT.git
cd SwinBERT
```
### Environment
On HAC machine
```bash
conda create -n swinbert python=3.8
conda activate swinbert
```
### Run
1. Reproduce the CUDA out of memory error
Follow [README.md](https://github.com/thuc-moreh/SwinBERT/blob/main/README.md) to the step Before Running Code: Launch Docker Container.
After that run
```bash
export REPO_DIR=$PWD
DATASETS=$REPO_DIR'/datasets/'
MODELS=$REPO_DIR'/models/'
OUTPUT_DIR=$REPO_DIR'/output/'
source launch_container.sh $DATASETS $MODELS $OUTPUT_DIR
```
2. Reproduce Could not install packages due to an OSError: [Errno 2] No such file or directory: '/tmp/build/80754af9/attrs_1604765588209/work'
First, run
```bash
pip freeze > requirements.txt 
```
Then copy the requirements from container to host machine by 
```bash
docker cp container_id:/videocap/requirement.txt SwinBERT_directory
```
replace container_id with the container id and SwinBERT_directory with the dicrectory of the SwinBERT repo on your machine.

Exit the container and run
```bash
pip install -r requirements.txt
```
