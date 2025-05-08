This is an example code to implement Progressive Reconstruction of
Off-diagonals (PRO). The Main_Code.m script is the primary MATLAB file
that sets up and runs the entire simulation and preprocessing workflow
for PRO. When you run Main_Code.m, it performs the following: -Loads and
displays the target object and scattering medium data. -Extracts and
visualizes ground truth off-diagonal aberrations. -Simulates the
distorted reflection matrix. -Runs the Patch-CLASS algorithm to estimate
patch-wise aberrations and reconstructs the stitched image. -Extracts
and compares off-diagonal and PSF correlations between Patch-CLASS and
ground truth data. -Finally, it automatically launches the PRO GUI for
the next stage of interactive PRO optimization.

Directory Structure: \\Root_Dir (named Example_Code) Main_Code.m - Main
execution code PRO_GUI.m - Implement PRO using GUI PRO.m - To implement
PRO without GUI (not required if using GUI) PRO_Python_Optimization.py -
This has to be externally run to optimize the transfer functions and the
object Python_Environment.yaml - Example python enviroment
\\Example_Data - Contains data for object, ground truth transmission
matrices, and details off-diagonals \\Functions - Contains various
functions required for PRO \\PreOptimized_Results_for_Each_Stage -
Contains results of each stage of PRO corresponding to the example data
(doesn't require use of Python). \\Python_Data_and_Result - This is used
by PRO to store training data and optimized results from Python.

NOTE: The required dataset and other files can be downloaded from
https://doi.org/10.6084/m9.figshare.28953386 Please ensure that the base
folder (working directory) in MATLAB or Python is set to the same
location where the main code file exists and follows the above directory
scheme.

\*PRO GUI Usage\* After running Main_Code.m, the PRO GUI window (PRO
Stage Controller) will open automatically. This GUI allows for
interactive management for each stage of the PRO (Optimization) process.
The PRO workflow alternates between MATLAB (for data preparation and
visualization) and Python (for optimization). Following is the workflow
for stage-wise implementation of PRO: -Select the stage. -Click Create
Data for current PRO Stage. -Run PRO_Python_Optimization.py in Python
(set up using the provided environment "Python_Environment.yaml").
-Click Show Results for current PRO Stage. -Optionally, Save the
results. This can be manually Loaded later. -Advance to next stage and
repeat.

Details of available functions in PRO GUI: -Stage Selection: Use the
dropdown menu at the top to select the current PRO stage (I, II, III, or
IV). The GUI will display the relevant target off-diagonals and initial
conditions for the selected stage (for data creation). -Create Data for
PRO Stage: Click this button to generate the training data for the
selected stage. The data will be saved to
"Python_Data_and_Result/Training_Data_from_MATLAB_to_Python.mat". For
Stage I, initialization is from patch-CLASS results. For Stage II
onwards, initial parameters are the results of the previous stage. Next,
run the PRO_Python_Optimization.py script externally to perform the
optimization for this stage. It will result in
"Python_Data_and_Result/Optimized_Data_from_Python_to_MATLAB.mat" -Show
Results for PRO Stage: After running the Python optimization, click this
button to load and display the optimized results from
"Python_Data_and_Result/Optimized_Data_from_Python_to_MATLAB.mat". It
will plot loss curves, the optimized image, off-diagonal, and the
off-diagonal and PSF correlations. It will also create
Aberration_optimized_S and Object_optimized_S corresponding to the Sth
stage. -Save Optimized Data File: Click to save the currently loaded
optimized data (located at
"Python_Data_and_Result/Optimized_Data_from_Python_to_MATLAB.mat") for
future use. The saved file can be later loaded and the results can be
run using Load Optimized Data File. Note: Loading and plotting will
require selection of correct stage, so that should be mentioned in file
name when saving. -Load Optimized Data File: Load a previously saved
.mat result file from Python optimization, select stage, and run.

NOTE: Since the optimization can take long time, optimized results for
each stage is provided in the folder
"PreOptimized_Results_for_Each_Stage". These can be loaded, and after
selecting the stage, the results can be plotted (doesn't require use of
Python). Alternatively, for testing purposes, "num_epoch" can be set to
small value in "PRO_Python_Optimization.py", which will run and save the
optimized data in Python_Data_and_Result without full convergence (e.g.,
10 or 50).

\*The provided codes are tested on personal computer with the following
hardware and software: -OS: Microsoft Windows 10 Pro -CPU: Intel
i7-10700K @ 3.80 GHz -RAM: 128 GB -GPU: NVIDIA GeForce RTX A6000 (48 GB
VRAM) -MATLAB: 2023a -Python: 3.11.4 -PyTorch: 2.0.1 -CUDA: 11.7 -Key
Libraries: -numpy: 1.25.2 -torch: 2.0.1 -matplotlib: 3.7.1 -scipy:
1.11.1 -h5py: 3.9.0
