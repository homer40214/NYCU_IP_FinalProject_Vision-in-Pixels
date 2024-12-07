# NYCU_IP_FinalProject_Vision-in-Pixels

### Environment

-	Ubuntu 18.04
-	Tensorflow 1.15
-	Python 3.7

### Dataset

- Place noisy datasets in dataset folder.
  - [[Darmstadt Noise Dataset]](https://noise.visinf.tu-darmstadt.de/), [[SIDD-Medium Dataset/Validation Data and Ground Truth]](https://www.eecs.yorku.ca/~kamel/sidd/)

- Final dataset directories should be like 
```
dataset
├─ dnd2017
│  └─....
├─ SIDD_Medium_Srgb
│  └─....
├─ ValidationNoisyBlocksSrgb.mat
└─ ValidationGTBlocksSrgb.mat
```

- Run prepare_dataset.py to make tfrecords and validation npy .

[comment]: <> (- you can use custom images as training dataset by glob command for dataset argument)

### Training code
```
python train.py --gpu [GPU_ID] --name [Experiment Name] --dataset [SIDD or DND]

Arguments
    --gpu       GPU ID
    --name      Name of Experiment. Checkpoints and tfevents will be saved in ckpts/[name].
    --dataset   Training dataset(tfrecords) : SIDD or DND (default: SIDD)
    --patchsize Size of training patch. Must be dividable by stride_b and stride_i. (default: 120)
                Use 240 for better performance.
```


More details about optional arguments can be found with 
```
python train.py --help 
```


### Test code

```
python infer.py --gpu [GPU_ID] --modelpath [Checkpoint_path] --imagepath [Image_glob] --savepath [Output folder]
```

You can use the following sample command to test the denoiser with sample images.

```
python infer.py --gpu 0 --modelpath ./pretrained/CBSN_SIDDtrain.ckpt --imagepath ./Figures/sampleimage*.png --savepath ./results/
```