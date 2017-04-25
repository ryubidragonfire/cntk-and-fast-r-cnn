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

### For Linux VM
it might be helpful to include the "sudo" command, if you receive "permission denied"-exceptions:

```bash

sudo python install_fastrcnn.py

```

If the pip install fails, move to the root directory with and grant permissions to the whole anaconda directory.

```bash
cd/
sudo chmod -R 777 anaconda
```

### For Windows users
visit http://www.lfd.uci.edu/~gohlke/pythonlibs/, and download:

scikit_image-0.12.3-cp34-cp34m-win_amd64.whl [link](http://www.lfd.uci.edu/~gohlke/pythonlibs/#scikit-image)  
opencv_python-3.1.0-cp34-cp34m-win_amd64.whl [link](http://www.lfd.uci.edu/~gohlke/pythonlibs/#opencv)

Install them by:

```python
pip install your_download_folder/scikit_image-0.12.3-cp34-cp34m-win_amd64.whl
pip install your_download_folder/opencv_python-3.1.0-cp34-cp34m-win_amd64.whl
```
Now, follow either:

https://github.com/Azure/ObjectDetectionUsingCntk, from **Part 1**. 
- **Part 1**: How to use as-it-is. Extract feature via NN, SVM as classifier.
- **Part 2**: 'Re-train' based on AlexNet, with softmax as output layer.
- **Part 3**: using your own data, image annotation and labelling, about hyper-parameters, publishing model as REST API.
- **Part 4**: Reproduce results with Pascal VOC dataset.

or:

https://github.com/Microsoft/CNTK/tree/master/Examples/Image/Detection/FastRCNN, from **Preprocess data**

or:
https://github.com/Microsoft/CNTK/wiki/Object-Detection-using-Fast-R-CNN

### Expected Inputs
- see https://github.com/Azure/ObjectDetectionUsingCntk/tree/master/data/grocery

### Additional possible things to setup
- Ensure you have visual C++ common tools: https://github.com/Microsoft/CNTK/wiki/Setup-CNTK-on-Windows
- [Pre-compiled](https://github.com/Microsoft/CNTK/wiki/Object-Detection-using-Fast-R-CNN#pre-compiled-binaries-for-bounding-box-regression-and-non-maximum-suppression) binaries for bounding box regression and non maximum suppression 
-  goto `C:\git\CNTK\Examples\Image\Detection\FastRCNN\fastRCNN\utils` to rename ~cython_bbox.cp34-win_amd64.pyd~ to `cython_bbox.pyd`

### Reference:
[Free online book on neural network and deep learning](http://neuralnetworksanddeeplearning.com/index.html)

### Bugs??
- https://github.com/Microsoft/CNTK/blob/master/Examples/Image/Detection/FastRCNN/cntk_helpers.py 
Line 652:
```python
def imread(imgPath, boThrowErrorIfExifRotationTagSet = True):
    if not os.path.exists(imgPath):
        print("ERROR: image path does not exist.")
        error

    rotation = rotationFromExifTag(imgPath)
    if boThrowErrorIfExifRotationTagSet and rotation != 0:
        print ("Error: exif roation tag set, image needs to be rotated by %d degrees." % rotation)
    img = cv2.imread(imgPath)
    if img is None:
        print ("ERROR: cannot load image " + imgPath)
        error
    if rotation != 0:
        img = imrotate(img, -90).copy()  # got this error occassionally without copy "TypeError: Layout of the output array img is incompatible with cv::Mat"
    return img
```
The error message after running:

>> `python C1_DrawBboxesOnImages.py`

is:

`NameError: name 'imrotate' is not defined`

**possible fixes:**
Courtesy of P. Bue....
```python
from PIL import Image

def imrotate(img, angle):
        imgPil = imconvertCv2Pil(img)
        imgPil = imgPil.rotate(angle, expand = True)
        return imconvertPil2Cv(imgPil)

def imconvertCv2Pil(img):
    cv2_im = cv2.cvtColor(img,cv2.COLOR_BGR2RGB)
    pil_im = Image.fromarray(cv2_im)
    return pil_im

def imconvertCv2Numpy(img):
    (b,g,r) = cv2.split(img)
    return cv2.merge([r,g,b])

def imconvertPil2Cv(pilImg):
    return imconvertPil2Numpy(pilImg)[:, :, ::-1]
```

