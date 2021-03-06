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
 
We have uploaded (1) some raw data, (2) files containing XY,T tracks of single histones, 
and (3) a detailed description of the experiment and our microscope. 
Please let us know if there is anything else you would like us to upload and share.

Note that GitHub has a 1GB cap on repositories, and we therefore cannot upload all our raw data here. 
However, all raw data are available from (1) us, or (2) via a Dropbox at University of Massachusetts, or, (3) soon, from the 
4DN Nucleome Data coordinating center portal at https://data.4dnucleome.org.  

## Basic usage and raw data file format (.dat) information

All raw intensity/pixel information is stored in a simple binary format ending in the extension ‘.dat’. 
Binary files are needed for the computer to be able to keep up with the data streaming from the camera. 
These binary file can be read in hundreds of different ways, depending on your needs.

The easiest thing to do is to use ImageJ (or Fiji), which can read raw binary files via File > Import > Raw... 
Then select the .dat file, and select Unsigned 16 bit integer, Little-endian byte order, and the 
Height and Width information (512 x 512). You will also need to set the number of images to whatever 
value is stated the corresponding metadata (.dth) file, which defaults to storing 100 images per file. 
At this point you will have the full dataset, as an image stack, in ImageJ (or Fiji). 
Note that the image may be completely white or black, due to limitations your operating system may 
have WRT displaying depending 16bit resolution greyscale images.

In general, advanced users will simply read in the .dat binary files into their favorite image processing 
environment, such as Matlab or Mathematica.

## Frame-by-frame metadata files (.dth)

Every exposure of the camera is linked to a metadata string that contains information about the instrument,
the lasers, the time, etc in the instant that exposure was taken. This metadata string will be about 350 characters 
long and will be terminated by '\n'. This string is structured as follows, with all fields being 
self-explanatory. N is the index of images, H and W are the height and width of the images, and 
then there is a timestamp and exposure and laser information:

N:0 
H:512 
W:512 
Time:1489775259.3620 
Exp: 50.0 
Gain: 250 
DT_Analog_v1: 5.0 
DT_Analog_v1: 5.0 
DT_Analog_v1: 5.0 
DT_Analog_v1: 5.0 
639: True 
405: True 
488: True 
561: True 
z_nano_z: 98.5427 
motor_stage_x: 13.9445 
686_y: 13.1545 
DT_AOTF_v1: 5.0 
DT_AOTF_v1: 5.0 
DT_AOTF_v1: 5.0 
DT_AOTF_v1: 5.0 
DT_AOTF_singleval: True 
scope_z: 4207.35 
scope_bflamp: 0.0 

## Quantitative analysis of the raw image data in Matlab. 

Right out the box, Matlab can read all .dat files directly. 
```
fileID = fopen('a1.dat');
myImageArray = fread(fileID,'uint16');
```
At this point you have an array with all the data, and you can manipulate this in any way you want. 
Most people use ‘reshape’ to turn this into a simpler 3D array, e.g. [X Y T]. 
You can use ‘imshow’ on this array (or slices thereof) directly, to see/scale/process the images.

## Quantitative analysis of the raw image data in Mathematica. 

Right out the box, Mathematica can read all .dat files directly. 
```
file = "/Users/janliphardt/Desktop/a_1.dat";
bc = Import[file,”UnsignedInteger16”];
```
At this point you have all the data, and you can manipulate the data in any way you want. 
Most people use ‘ArrayReshape[]’ to turn everything into a simple 3D array, e.g. [X Y T] 
or whatever order they like most. You can manipulate the data as data, or you can can explicitly 
designate the data as raster images via Image[] if you prefer do your processing 
in the image space. Staying in ‘data’ space is typically easier. 

## Quantitative analysis of the tracks.

For convenience, we also provide the XY,T tracks if you do not want to do the tracking yourself. 
The .mat files can be opened in your favorite analysis environment (Matlab, Mathematica, Python, ...).

## Biological, code, and instrument details

*U2-OS* Tet-On® Cell Line (#631143) were purchased from Clontech. All mammalian cells were cultured on tissue culture plastic in standard tissue culture incubators held at 37°C with 5.0% CO2 using DMEM supplemented with 20% fetal bovine serum and penicillin-streptomycin antibiotics. 
U2OS cells co-expressing H2B-ArrayGN and mWTGFP were synchronized to G1/S boundary using a double thymidine block procedure. 
~30% confluent cells were blocked with 2.5mM Thymidine for ~20 hours followed by a release step lasting 10 hours, followed by a second Thymidine block. 
Cells were treated with cumate during the 10-hour release step to induce expression of mWTGFP. For imaging cells in prophase, 
cells were released from the second thymidine block after a period of ~16 hours, incubated for 2 hours in fresh medium, 
followed by treatment with 10μM RO-33O6 (Sigma) for 10 hours. Release from the RO-33O6 block allowed cells to synchronously enter mitosis.

*Transfections*. All transfections were performed using the Neon Transfection system (Thermo Fisher Scientific).  
U2OS cells were transfected using 2 pulses of 1,050 V and 30 ms pulse width. 
Upon transfection, cells were seeded on Mattek dishes coated with fibronectin (Sigma Aldrich) in complete DMEM media without Pen/Strep and with teteracycline free FBS (Thermo Fisher Scientific). 
U2OS cell lines were generated by transfecting cells with the relevant PiggyBAC plasmids and a plasmid expressing transposase following manufacturer’s 
protocol and then selecting using appropriate antibiotics. For single stable cell line puromycin was the antibiotic of choice where as for double stable cell lines a combination of puromycin and hygromycin was used. 

*TIRF, dual color TIRF and HiLo-TIRFM imaging*. Total internal reflection microscopy (TIRF or TIRFM), dual-color TIRFM, and HiLo-TIRFM, 
were performed on an Olympus CellTIRF system, with independent motor controlled TIRF angles for each fiber-coupled illumination laser, 
through a 1.49 NA 100x objective and 1.6x Optovar magnifier. 
Images were recorded on an Andor iXon Plus EMCCD camera at 0.5 frames per second.
All dichroics and filters were purchased from Semrock. 
All experiments were performed within a heated, CO2 controlled incubation chamber set to 37 °C and 5%, respectively. 
Additional temperature control was provided by a collar-type objective heater, also set to 37 °C.

*Single particle tracking*. Single particle tracking (SPT) was performed in two steps, all using custom-written Python and C++ code. 
First, detectable particles in each frame were identified by performing a Laplacian of Gaussian filter and then thresholding 
the filtered image based on intensity. A 2D Gaussian centered on each identified particle was then refined onto the raw image data 
using the Levenberg-Marquardt algorithm, with particle x/y position, amplitude, background height, and in some instances standard 
deviation as free parameters. All particle detection parameters were validated by eye for each dataset, using a custom GUI. 
The single particle positions in each frame were then linked into single particle time trajectories using a nearest-neighbor 
type particle tracking heuristic, with a maximum per-frame jump distance parameter. The algorithm iteratively minimized the 
jump distance between frames, with no assumed momentum. All single particle trajectories were spot-validated by eye. For 
signal-to-noise ratio calculations, the signal was defined as the peak height of the Gaussian fit above background level, 
and noise was defined as the standard deviation of a 5x5 pixel window centered around the particle location after subtracting 
fitted Gaussian.

*Fractional Brownian Motion*. The raw XY,T data were directly fit to a three parameter fBM model 
```
Mathematica version 11.1.1.0, 
FractionalBrownianMotionProcess[μ, σ, h], ProcessEstimator -> "MaximumLikelihood"
``` 
The first term μ captures constant ‘drift’, σ captures the covariance (= σ2 (s2h+t2h-Abs[t-s]2h)/2), and h is the Hurst parameter. 
Note that h is simply 1/2 of α, the slope of LogLog transformed MSD.


 



  
