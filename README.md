# How to setup the environment
## On Local Machine
Create & activate the conda enviornment with python3.8.2 version
```
conda create --name <env-name> python=3.8.2
conda activate <env-name>
```
Install the required libraries to run the code from requirements.txt
```
pip install -r requirements.txt
```
Run code
```
cd src
python run.py
```
## With Docker
The repo also contains Dockerfile to run the code
```
cd ..
docker build -t <image_name>:<tag> missing_data_imputation/Dockerfile .
docker run -t -n <container-name> <image_name> <experiment-to-run>
```
Example:
```
cd ..
docker build -t missing_data_imputation:0.1 missing_data_imputation/Dockerfile .
docker run -t -n mdi missing_data_imputation:0.1 python run.py
```
# How to reproduce the results of the papaer
## MCAR state-of-the-art comparison:
 * DAEMA: `python run.py`
 * DAE: `python run.py --daema_attention_mode no --daema_ways 1`
 * AimNet: `python run.py --model Holoclean --batch_size 0 --lr 0.05 --metric_steps 18 19 20 21 22`
 * MIDA: `python run.py --model MIDA --batch_size -1 --metric_steps 492 494 496 498 500 --scaler MinMax`
 * MissForest: `python run.py --model MissForest --metric_steps 0 --scaler MinMax`
 * Mean: `python run.py --model Mean --metric_steps 0`
 * Real: `python run.py --model Real --metric_steps 0`

## MNAR state-of-the-art comparison:
 * Same as above, but with an additional argument: `--ms_setting mnar`

## Missingness proportions:
 * Same as above, but with an additional argument (e.g. for 10% missingness): `--ms_prop 0.1`

## Ablation study part 1:
 * Full: `python run.py`
 * Classic: `python run.py --daema_attention_mode classic`
 * Sep.: `python run.py --daema_attention_mode sep`

## Ablation study part 2:
 * DAEMA: `python run.py`
 * Reduced loss: `python run.py --daema_loss_type dropout_only`
 * Full loss: `python run.py --daema_loss_type full`
 * No art. miss.: `python run.py --daema_pre_drop 0`
