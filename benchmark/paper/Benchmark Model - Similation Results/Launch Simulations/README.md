# How to Run & Analyze  Baseline and Sensitivity Experiments 

In order to perform the baseline and sensitivity experiments presented in the paper, we used the jar executable contained in the BenchmarkModel_Baseline_Sensitivity archive. This is by far the fastest solution to run Monte Carlo Simulations and it allows setting up the sensitivity experiments through the use of a separated properties file defining the ranges of variation and the increment for each parameter. The archive also contains the R script require to gather the .csv files produced by JMAB, analyze the results and draw the plots presented in the paper.

## Baseline:
To run the baseline just open your Command Line, change the folder to “BenchmarkModel_Baseline_Sensitivity”, and 
•	Under Windows: launch the Baseline.bat file (some Windows versions allow to launch the .bat file by double clicking on it). 
•	Under Mac OS: launch the Baseline.sh file 

You can set the number of Monte Carlo Simulations to be executed by opening the “baseline.prop” file contained in the “Model” folder and specify the desired number of replications (Nmc):
class net.sourceforge.jabm.DesktopSimulationManagersimulationController.numSimulations=Nmc:1:Nmc

Once the simulations are completed just open the R script called “Baseline.R”, set the working directory of R to the script folder, and source the script.
The script will automatically merge the Monte Carlo replications .csv files in a single file for each variable and then produce all the statistics and plots contained in the paper (saved in .ps format). The script requires to have R installed in your PC and the additional Packages: "mFilter", "poweRlaw", "propagate", and "tseries".

N.B. 1 If you encounter memory allocation problems change the setup in the .bat file: Open it by right clicking and then select “Edit”.  Try to reduce the number of Giga allocated by editing the string “-Xmx3G -Xms3G” at the end of the 2 lines, save, and relaunch.

N.B. 2 The merged .csv files need to be generated just once. If you have already generated them, you can comment the following 3 lines of the script (at the top):
source("MergeMonteCarloSim.R")
generateMergedCSV(folder)
generateSums(folder)

N.B. 3 The estimation of the distributions presented in the paper, and in particular the bootstrapping procedure, takes a long time. If you are not interested in producing these figures just comment the corresponding lines code. For your convenience, the lines of code corresponding to the distributions analysis are gathered at the bottom of the script and marked by the heading: DISTRIBUTIONS

## Sensitivity Experiments

To set up a sensitivity experiment open the “sensitivity.prop”  file contained in the “Model” folder with a text editor and de-comment the line(s) referring to the parameter(s) of interest. The 3 numbers following the parameters names (expressed in the “class.field” format, as they appear in the source code) are the minimum value, the increment and the maximum value for the parameter. Note that if you un-comment more than one variable, the Monte Carlo simulation will combine all possible cases of variable values (i.e. exponential number of possible sets). You can set the number of Monte Carlo replications (by default =5) by opening the MainFile.xml with a text editor and then specify the desired number in: <property name="numSimulations" value="5"/> 

To launch the experiments open your Command Line, change the directory to the “BenchmarkModel_Baseline_Sensitivity” folder, and then launch the 
•	the Baseline.bat file - as in the example hereunder - in case you are using Windows OS
•	the Sensitivity.sh file in case you are using Mac OS .  

Once the simulation have been carried out, open the R script called “Sensitivity.R”, set the working directory of R to the script folder, and source the script. The script requires to have R installed in your PC and the additional Package "mFilter".

The script will automatically merge the Monte Carlo replications .csv files of all the sensitivity experiments in a single file for each variable, and then produce all the statistics and plots contained in the paper. 

N.B. 1 The merged .csv files need to be generated just once (see above).

