# Multiplex-Pipeline

Overview

The Multiplex Pipeline operates using a three part system on both MATLAB and CellProfiler:

1) Region of Interest (ROI) selection on overlay images to cut out unwanted areas in image for the step 2.

2) Fluorescence detection and preliminary counts through CellProfiler pipeline. This step uses the selected ROIs from step 1 to accomplish the following:
Detection of all nuclei and approximate cell outlines around each nuclei
Detection of fluorescence in all individual channels
Preliminary counts of each probe positive cell

3) The final step takes the ROI data from step 1 and the cell outlines, individual probes, and overlay information from step 2 to complete further analysis. The code calculated the following for each fluorophore/channel in an image set: non-object/background area, area/puncta, total area of puncta/cell, non-specific binding rate (sum of puncta area/non-object area), and probability of off-target binding for each puncta based on a binomial distribution. A cell was counted as positive for a channel when the amount of puncta in each cell was found to be greater than the cell size*non-specific binding rate/channel. A Bonferroni correction was applied to each p value of all counted cells in an image  (p value < 0.01/total number of cells). Total counts of all individual channels and colocalized cells and percentage of each compared to total cells were generated for each image set. Once these final calculations are made they are exported into a MATLAB spreadsheet that one can directly copy into other analysis programs.


Limitations: 
-Only three fluorophores, one DAPI. Not useful for HiPlex
-Does not work on Z-stacked images
-Used specifically for Keyence BZ-X710 epifluorescent microscope images
-Used only with TIF files

Preparation:

Necessary Downloads:
-MATLAB (or can try on MATLAB Online)
Need license to download

Once downloaded, search and add the following toolboxes:

‘Imaging Processing Toolbox’
‘Statistics and Machine Learning Toolbox’

-CellProfiler
Open access

-Pipeline Files:

‘STEP1_MultiplexPipeline_ROISelector_BS’ (if images are already greyscale, use grey version)
‘MultiplexPipeline_CPStep#2_BS_BaseAll3Fluorophores’
‘STEP3_MultiPlex_RNAScopeAnalysis_BS’

Recommended: Watch CellProfiler and MATLAB resources

Once everything is downloaded and ready:

-Put all the image sets you intend to analyze into the same folder. Make sure all the tif files for each image set are present and not in individual folders. 
  If you are analyzing more than one area of the brain, separate them into distinct folders. (example: All NAc image sets in same folder, and all VTA image   sets in a different folder.
-Create a folder to store all your output information.
-Create a folder for all the channels in your image set (CH1, CH2, CH3, CH4, Overlay). They can be named any way you like, but this is required to complete step 1. 
-Keep the following pattern for organizing:
  CH1 folder (named what you prefer) : egfp/Alexa 488 fluorophore tifs
  CH2 folder: mcherry/Atto 550 fluorophore tifs
  CH3 folder: DAPI tifs
  CH4 folder: cy5/Atto 647 fluorophore tifs
-Now, put all the corresponding tifs into their folders. Simply, search in the main folder for what you have labeled for each channel (example: search ‘CH1’ for egfp). All files matching the keyword should show up. Then, hit Control+A (Command + A on Mac) and all should be selected. Drag and drop the selected into the correct folder.

Once all this is done, you are ready to begin!
