# cntk-and-fast-r-cnn
Getting it set up with Azure DSVM, CNTK and Fast-R-CNN.

# setting up
Spin up an Azure DSVM. Come with CNTK.

# get Fast-R-CNN
Clone from : https://github.com/Microsoft/CNTK
Fast-R-CNN can be found at: https://github.com/Microsoft/CNTK/tree/master/Examples/Image/Detection/FastRCNN

- open a command prompt

```python
# at command prompt, type in the following:

`conda env list

# conda environments:
#
cntk-py34                C:\Anaconda\envs\cntk-py34
py35                     C:\Anaconda\envs\py35
root                  *  C:\Anaconda
```

- change to cntk environment

```python
activate cntk-py34
```

- `cd C:\CNTK\Examples\Image\Detection\FastRCNN`

Then,

```python
python install_fastrcnn.py
```

Now, follow either:

https://github.com/Azure/ObjectDetectionUsingCntk, from **Part 1**

or:
https://github.com/Microsoft/CNTK/tree/master/Examples/Image/Detection/FastRCNN, from **Preprocess data**
