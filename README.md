# Multi-stream Crowd Counting
Code of "Where are the People? A Multi-Stream  Convolutional Neural Network for Crowd Counting via Density Map from Complex Images" presented in IWSSIP 2019.

## 1. Environment

We used the following enviroment:

* Python 3
* PyTorch
* OpenCV
* Numpy
* MatPlotLib
* Ubuntu 16.04

You can also run the code using the docker image of [ufoym/deepo](https://hub.docker.com/r/ufoym/deepo).

## 2. Preparing data

We make available UCF-CC-50 and Shanghai Tech datasets [here](), download and unzip it into the root of the repo. Directories should have the following hierarchy:

```
ROOT_OF_REPO
    data
        ucf_cc_50
            UCF_CC_50
                images
                labels
        ShanghaiTech
            part_A
                train_data
                    images
                    ground-truth
                test_data
                    images
                    ground-truth
            part_B
                train_data
                    images
                    ground-truth
                test_data
                    images
                    ground-truth
```

The code was developed such that data augmentation is computed before every other step and the results are stored in the hard drive. Thus, the first time you run the code it will take quite a long time. Augmented data is stored with the following hierarchy:

```
ROOT_OF_REPO
    data
        ucf_cc_50
            people_thr_0_gt_mode_same
        ShanghaiTech
            part_A
                people_thr_0_gt_mode_same
            part_B
                people_thr_0_gt_mode_same
```

## 3. Training

To train using UCF-CC-50 (with all folds) and save the results log in `log/multi-stream` you can run:

```
python3 main.py -d ucf-cc-50 --train-batch 32 --save-dir log/multi-stream
```

In case you want to run a specific fold or part you can use flag `--units`, check the `Makefile` for more examples.

The training log is stored in `log_train.txt` inside the corresponding log/fold/part directory.

## 4. Testing

After training you can re-load the trained weights (using flag `--resume`) and use them for testing:

```
python3 main.py -d ucf-cc-50 --save-dir log/multi-stream --resume log/multi-stream --evaluate-only 
```

The testing log is stored in `log_test.txt` inside the corresponding log/fold/part directory. You can also generate the plots of the predictions using flag `--save-plots`, results are stored in the directory `plot-results-test` inside the corresponding log/fold/part directory.

## 5. Final Notes

If you have any question regarding the code or method don't hesitate to contact [me](https://github.com/RQuispeC). This project was developed using the repo of [svichwa](https://github.com/svishwa/crowdcount-mcnn) as a base.