# Implementation of our proposed method

## 1. Robot base registration

Here we provide a demo for the robot base registration, where the related-config* file is also given in [registration](./registration/).

a. Replace `pretrain` in `indoor.yaml` with the path of your model. You can download our trained model from [here](https://1drv.ms/u/s!AnRiouA_fmTVjMRTEBwoO2O7PRHDhg?e=RIDaYD). For example,

``` bash
pretrain: './model_best_loss.pth'
```

b. You can train your own model using (if  you have a robot base other than UR3e, UR5 and UR5e)
```
python main.py configs/train/indoor.yaml
```

c. Open `PredatorRegistration-demo.ipynb` to test. The function for PREDATOR is
```
 tsfm, consuming_time = PredatorRegistration(src_data, tgt_data)
```