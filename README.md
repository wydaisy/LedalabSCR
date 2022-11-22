# LedalabSCR
This script is used to analyze skin conductance level using Ledalab implenmented in MATLab

1.	Raw data file
Using Brain Product, the raw SCR was in eeg, vhdr, and vmrk format.
*.eeg file contains voltage values of the SCR. *vhdr file contains recording parameters and further meta-information. *vmrk file contains information about the events/markers in the data.

2.	Preprocessing
Using Ledalab, the SCR recording is first down sampled to 250 Hz and smoothed with a 1000-samples moving average function. Then the data are low-pass filtered with a cut-off frequency of 2 Hz. 

3.	Main analysis
The preprocessed data are put through continuous deconvolution analysis (CDA) in which the data were decomposed into the tonic and the phasic components. The tonic component reflects baseline activity, while the phasic component reflects a direct response to a stimulus. For each trial, SCR from 1 second after heat onset to 4 second after heat offset account for delayed autonomic responses. 

Example 1:
Ledalab('P:\EDA_Data\', 'open', 'biotrace', 'downsample', 2, 'analyze','CDA', 'optimize',4, 'export_era', [1 4 .01 3])
... imports all Biotrace files from directory P:\EDA_Data\, downsamples them by factor 2 (e.g. from 32 Hz to 16 Hz), analyzes them by means of CDA (performing optimization of four initial values), exports the event-related data (for a response window of 1 to 4 sec after each marker, with an SCR amplitude threshold of .01 muS) to Excel-result files and saves them to Ledalab files (including data and analysis).

Example 2:
Ledalab('P:\EDA_Data\', 'open','leda', 'smooth',{'gauss',16}, 'analyze','DDA', 'optimize',3, 'overview',1)
... opens all Ledalab files from directory P:\EDA_DATA\, performes data smoothing using the gauss-method and a window width of 16 samples analyzes them by means of DDA (performing optimization of 3 different initial values), saves the Ledalab files (now including analysis), and saves an analysis overview to an image file.
