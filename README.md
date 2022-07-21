# digital-breakthrough-hack
N-th place solution of RZD hackathon

## Data dir tree structure
```
-- data
    |-- test [1000 entries exceeds filelimit, not opening dir]
    |-- train
    |   |-- images [8203 entries exceeds filelimit, not opening dir]
    |   `- mask [8203 entries exceeds filelimit, not opening dir]
```

## Prepare env
``` 
cd mmsegmentation/docker
docker build . -t rlh
```

## Launch docker
```
bash launch_docker.sh
```

## Prepare training masks & split
```
cd /workspace/rlh
python3 create_split.py
python3 create_masks.py
```

## Data dir structure now

```
-- data
    |-- stratified_split
    |   |-- test.txt
    |   |-- train.txt
    |   `-- val.txt
    |-- test [1000 entries exceeds filelimit, not opening dir]
    |-- train
    |   |-- images [8203 entries exceeds filelimit, not opening dir]
    |   |-- mask [8203 entries exceeds filelimit, not opening dir]
    |   |-- meta.csv
    |   `-- new_mask [8203 entries exceeds filelimit, not opening dir]
```


## Train model

```
cd /workspace/rlh/mmsegmentation
bash tools/dist_train.py /workspace/rlh/configs/config_27_augs.py 2 --work-dir /workspace/rlh/work_dirs/exp37
```

## Inference trained model
```
python3 inference.py --exp exp37
```
