<img src="https://github.com/nGImagic/TaPy/blob/master/pics/TaPy_logo.png"  width="150" height="150" />

TaPy is used for data reduction of grating interferometer data with X-rays and neutrons. It is designed for experiments with Talbot-Lau interferometers and data that is generated by stepping a grating, thus inducing intensity modulations in each pixel that are then fitted with a sinusoidal function to retrieve mean value, phase and amplitude. These parameters are then used to generate transmission images (TI), differential pahse contrast images (DPCI) and dark-field images (DFI).

# Getting started
It's simple! Download the github repository, then open the "main.py" file and you are ready to go. Just make sure you have a running python 3 environment and the required packages.

Required python3 repositories:
- numpy
- os
- PIL
- matplotlib
- astropy (for fits files)
- fitsio (for some fits files)
- h5py (for hdf files)
- pathlib
- scipy

You might run into problems installing the fitsio package...especially in Windows. This package is not really needed to use TaPy. It is only required if your ".tif" file header is corrupted, or includes non ASCII characters. Most of the time this will not be the case.

# Tutorial
If you are using Jupyter you can use "TaPy_tutorial.ipynb" for a step-by-step tutorial. The file can then also be modified to suit your needs. 

# General usage
We recommend using TaPy either through a Jupyter notebook like "TaPy_tutorial.ipynb" or by using the "main.py" file in the repsitory.
When you execute "main.py" all required functions from "functinos.py" will be imported and are ready to use. TaPy is set up such that "main.py" can be used to sequentially call all the functions defined in "functions.py". The order can be freely modified as the output of all functions can be used as input for any function. That way you can freely sort the functions you would like to execute as well as adding new ones or skipping steps by simply removing the call to the function you do not want to run.
The only order you should keep is the "read_data" as first function and the last two function calls. The function "createIm" results in the transmission image (TI), differential phase contrast image (DPCI), the dark-field image (DFI) and the visibility map. These are the final results which can then be used as input for "saveIm" to save your results.

# Loading data
The standard implementation TaPy ships with a data structure where the open beams, the projections and the dark currents are in individual folders. The folder directories have to be specified in the main.py file. If your data structure is different TaPy allows you to write your own read-in routine to deal with any data structure.
TaPy currently supports most of the common file formats, namely the ".hdf" family, ".fits" and ".tif"/".tiff". For any other datatypes you are welcome to modify the read-in function.

# The functions
The file "functions.py" includes a number of functions that can be used throughout the data reduction process. As we have mentioned before you can freely vary the order and decide for yourself which steps you would like to take to get your raw data ready for the final reduction to TI, DPCI and DFI in the "creatIm" function. Check out the descriptions in "functions.py" for details.
We recommend following series of functions for succesful data reduction: 
 - "read_data": Read the data and load it into variables. If you recorded dark currents and specified their directory this function also does the dark-current correction.
 - "normalization": Select an area outside of the gratings to normalise for variations in flux.
 - "oscillation": This function plots the oscillation of the raw data through the stepping of one grating. You can use it to get an idea of the quality of you motor and visually check the oscillations you use for retrieving the signal.
 - "cropped": Crop the image to a region of interest. This increases the computational speed.
 - "binning": If you would like to bin you data - here you go.
 - "createIm": Take the stack of OBs and projections to create TI, DPCI, DFI and visiblity map. The algorithm used in this step is based on Marathe et al. (2014) http://dx.doi.org/10.1063/1.4861199.
 - "saveIm": Save your results.
 
 # Have it your way
 Feel free to develop your own functions and add them to "functions.py". If you need more complex read-in routines to fit your data structure we suggest modifying "main.py". If you think you developed things that could be interesting to the community let us know and we will incorporate it and make it available to everybody.
 
 Contact:
 Ralph P. Harti - Ralph.Harti@psi.ch
 Jacopo Valsecchi - Jacopo.Valsecchi@psi.ch
 
