# HistoneTracking

This repository contains high resolution tracking data for histones inside living cells. 

The overall goal of these experiments is to understand the temporal dynamics of chromatin. 
We explore temporal dynamics by stochastically expressing labeled histones, which are 
incorporated into the chromatin. We then use single molecule TIRF microscopy to 
track those labeled histones. 

We image the cells once every two seconds. Every cell contains between 40 to 180 labelled histones, and we generally try to track all of them. 
This means that for every cell, we obtain between 40 to 180 XY,T trajectories. These trajectories can then be used to study how the 
chromatin is moving. A basic analysis of these data is presented in Figure 3 of 
https://www.biorxiv.org/content/early/2017/07/03/159004.   
 
We have uploaded (1) all raw data, (2) files containing XY,T tracks of single histones, 
and (3) a detailed description of the experiment and our microscope. 
Please let us know if there is anything else you would like us to upload and share.

# Basic usage and file structure information:

1/ All raw intensity/pixel information is stored in a simple binary format ending in the extension ‘.dat’. 
Binary files are needed for the computer to be able to keep up with the data streaming from the camera. 
These binary file can be read in hundreds of different ways, depending on your needs.

The easiest thing to do is to use ImageJ (or Fiji), which can read raw binary files via File > Import > Raw... 
Then select the .dat file, and select Unsigned 16 bit integer, Little-endian byte order, and the Height and Width information, 
which depends on how you set your camera. A typical value will be 512 x 512. 
Note that essentially all programs disagree about what is meant by the height and width 
of an image, so you may need to flip the values if your images look funny. 
This is true for all programs (Fiji, Matlab, Mathematica, ...). 
You will also need to set the number of images to whatever value is stated the corresponding metadata (.dth) file, 
which defaults to storing 100 images per file. At this point you will have the full dataset, as an image stack, 
in ImageJ (or Fiji). Note that the image may be completely white or black, depending on your experiment 
and how you set the gain etc. Then, go to Select Image > Adjust > Brightness/Contrast... to see the data. 
Note that you cannot permanently apply any Brightness/Contrast values to the image stack, 
since it is in 16 bit format, and ImageJ/Fiji only allows you to do that with 8 bit images.

In general, advanced users will simply read in the binary files into their favorite image processing 
environment, such as Matlab or Mathematica. Briefly, 



  
