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

# Basic usage and file structure information

1/ All raw intensity/pixel information is stored in a simple binary format ending in the extension ‘.dat’. 
Binary files are needed for the computer to be able to keep up with the data streaming from the camera. 
These binary file can be read in hundreds of different ways, depending on your needs.

The easiest thing to do is to use ImageJ (or Fiji), which can read raw binary files via File > Import > Raw... 
Then select the .dat file, and select Unsigned 16 bit integer, Little-endian byte order, and the 
Height and Width information (512 x 512). You will also need to set the number of images to whatever 
value is stated the corresponding metadata (.dth) file, which defaults to storing 100 images per file. 
At this point you will have the full dataset, as an image stack, in ImageJ (or Fiji). 
Note that the image may be completely white or black, due to limitations your operating system may 
have WRT displaying depending 16bit resolution greyscale images.

In general, advanced users will simply read in the binary files into their favorite image processing 
environment, such as Matlab or Mathematica.

# Quantitative analysis of the raw image data in Matlab. 

Right out the box, Matlab can read all octopus files directly. 

fileID = fopen('a1.dat');
myImageArray = fread(fileID,'uint16');

At this point you have an array with all the data, and you can manipulate this in any way you want. 
Most people use ‘reshape’ to turn this into a simpler 3D array, e.g. [X Y T]. 
You can use ‘imshow’ on this array (or slices thereof) directly, to see/scale/process the images.

# Quantitative analysis of the raw image data in Mathematica. 

Right out the box, Mathematica can read all octopus files directly. 

file = "/Users/janliphardt/Desktop/a_1.dat";
bc = Import[file,”UnsignedInteger16”];

At this point you have all the data, and you can manipulate the data in any way you want. 
Most people use ‘ArrayReshape[]’ to turn everything into a simple 3D array, e.g. [X Y T] 
or whatever order they like most. You can manipulate the data as data, or you can can explicitly 
designate the data as raster images via Image[] if you prefer do your processing 
in the image space. Staying in ‘data’ space is typically easier. 

# Quantitative analysis of the tracks.

For convenience, we also provide the XY,T tracks if you do not want to do the tracking yourself. 
The .mat files can be opened in your favorite analysis environment (Matlab, Mathematica, Python, ...).

 



  
