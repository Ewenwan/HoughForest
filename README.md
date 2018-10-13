# 霍夫森林(Hough Forest) 随机森林和霍夫投票在计算机视觉中的应用，可以用在物体检测，跟踪和动作识别。 
[参考](http://www.cnblogs.com/walccott/p/4956860.html)

// Author: Juergen Gall, BIWI, ETH Zurich
// Email: gall@vision.ee.ethz.ch

# 编译compile (needs OpenCV)
   make all

# clean
   make clear

# run
   ./run.sh mode [config.txt] [tree_offset]
   mode: 0 - train; 1 - show leafs; 2 - detect
   config.txt: config file
   tree_offset: output number for trees (treetable[index+offset].txt)


   A config.txt example is given in the subdirectory 'example'

   # example train
   ./run_train.sh

   # example detect
   ./run_detect.sh

Config.txt:

    Information for storing and loading trees:
    # Path to trees + prefix 'treetable'
    /scratch/tmp/forest/example/trees/treetable
    # Number of trees
    10

    Image patch size (needs to be the same for training and learning):
    # Patch width
    16
    # Patch height
    16

    Information about the test set:
    # Path to images
    /scratch/tmp/forest/example/testimages
    # File with names of images
    /scratch/tmp/forest/example/test.txt

    Not used:
    # Extract features
    1

    Specify scale and ratio if necessary:
    # Scales (Number of scales - Scales)
    3 0.5 1 2 // 3 scales with factors 0.5, 1, and 2
    # Ratios (Number of ratios - ratio)
    1 1 // 1 aspect ratio with factor 1 = fixed aspect ratio 

    Information for storing the Hough images (scaled by a fixed factor such that max<=255):
    # Output path
    /scratch/tmp/forest/example/detect
    # Scale factor for output image (default: 128)
    50

    Information about positive and negative examples:
    # Path to positive examples
    /scratch/tmp/forest/example/trainimages
    # File with positive examples
    /scratch/tmp/forest/example/train_pos.txt
    # Subset of positive images -1: all images
    -1
    # Sample patches from pos. examples
    50

    # Path to negative examples
    /scratch/tmp/forest/example/trainimages
    # File with negative examples
    /scratch/tmp/forest/example/train_neg.txt
    # Subset of negative images -1: all images
    -1
    # Sample patches from neg. examples
    50

    train_neg.txt:
    50 1 // number of images + dummy value (1)
    neg0.png 0 0 100 40 // filename + boundingbox (top left - bottom right)

    train_pos.txt:
    50 1 // number of images + dummy value (1)
    pos0.png 0 0 74 36 37 18 // filename + boundingbox (top left - bottom right) + center of bounding box

    Output:
    detect-[I]_sc[S]_c[R].png
    I: image id
    S: scale id
    C: ratio id

    The images are slides of the 4D (x,y,scale,ratio) voting space for an image I. 
    For detection, the space needs to be smoothed and the maxima detected (or using mean shift). 
    This is not part of the source code.



Juergen Gall

BIWI, ETH Zurich	17 July 2009
