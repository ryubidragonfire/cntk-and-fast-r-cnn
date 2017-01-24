# cntk-and-fast-r-cnn
Notes on setting up CNTK and Fast-R-CNN with Azure DSVM.

# setting up
Spin up an Azure DSVM. Come with CNTK.

# get Fast-R-CNN
Clone from : https://github.com/Microsoft/CNTK
Fast-R-CNN can be found at: https://github.com/Microsoft/CNTK/tree/master/Examples/Image/Detection/FastRCNN

- open a command prompt

```python
# at command prompt, type in the following:

conda env list

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

pip install -r requirements.txt
```

For Windows users, visit http://www.lfd.uci.edu/~gohlke/pythonlibs/, and download:

scikit_image-0.12.3-cp34-cp34m-win_amd64.whl [link](http://www.lfd.uci.edu/~gohlke/pythonlibs/#scikit-image)  
opencv_python-3.1.0-cp34-cp34m-win_amd64.whl [link](http://www.lfd.uci.edu/~gohlke/pythonlibs/#opencv)

Install them by:

```python
pip install your_download_folder/scikit_image-0.12.3-cp34-cp34m-win_amd64.whl
pip install your_download_folder/opencv_python-3.1.0-cp34-cp34m-win_amd64.whl
```
Now, follow either:

https://github.com/Azure/ObjectDetectionUsingCntk, from **Part 1**

or:

https://github.com/Microsoft/CNTK/tree/master/Examples/Image/Detection/FastRCNN, from **Preprocess data**

In case you need `past`:

>`past` is a package to aid with Python 2/3 compatibility. Whereas `future` contains backports of Python 3 constructs to Python 2, `past` provides implementations of some Python 2 constructs in Python 3. It is intended to be used sparingly, as a way of running old Python 2 code from Python 3 until it is ported properly.

``` python
pip install future
```
