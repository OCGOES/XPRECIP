EAE 483/583 – Final Paper
Olivena Carlisle, Joseph Toniolo 
Geoscience problem:
Contemporary research has demonstrated that anthropogenic climate change (ACC) is directly influencing regional precipitation patterns and hydroclimatic extremes. Specifically, the magnitude and frequency of extreme precipitation events, as well as consequential flooding, are projected to increase with future warming climate scenarios (Kim and Villarini 2024). Additionally, flash flooding as a result of extreme precipitation is a significant peril of severe convective storms (SCS); the number one convective peril for human fatalities (Arguez et al. 2025). This suggests research surrounding extreme precipitation is becoming increasingly important. The Weather Prediction Center’s (WPC) Excessive Rainfall Outlooks (ERO) are graphics depicting categorical risk levels for rainfall events exceeding the River Forecast Center’s Flash Flood Guidance threshold, demonstrating a potential flash flood risk. Out of all the 2010-2020 flooding reports, 83% of all flood-related damages and 39% of flood-related fatalities were near to or within an ERO High Risk area (Burke et al. 2023). Moreover, EROs provide a unique way of defining excessive rainfall—a term difficult to define, consisting of multiple definitions across the meteorological community—by attributing extreme precipitation to flash flood potential. Through this perspective, EROs provide a localized and normalized definition, making them especially useful in hazard analysis and public safety. Most significantly, EROs are a significant means of communicating potential flood risk to the public by creating understandable, probabilistic visualizations. Due to these principal considerations, analyzing the atmospheric ingredients and synoptic regimes that promote excessive rainfall for days where an ERO exists, a thorough spatial analysis of the corresponding outlooks can be conducted. In doing so, the presence of dynamical variables can be attributed to specific ERO risk levels and generalized spatial extent. This project aims to create analog forecasting tools for excessive rainfall and flash flood risks to improve future forecasting of extreme pluvial events. 
 
1.	Proposed data and methods
The first step will consist of parsing through the ERO maps to create a .csv file of all days where a Slight Risk or higher exists in an area of the Eastern Contiguous United States (ECONUS). This project will only perform an analysis for the ECONUS, excluding the western third of the U.S. due to the dynamic differences, as well as to minimize terrain-induced forecasting problems that arise with the existing orography. Additionally, the timescale will be set through the 2021-2025 period due to the availability of ERO data files. Similarly, appropriate dynamical variables will be downloaded for the same days as the EROs. To conduct a comprehensive analysis of the different generalized synoptic regimes that promote excessive rainfall, kinematic, thermodynamic, land-surface, and moisture field variables will be downloaded:  
o	500 geopotential height (Z500)
o	Total column water vapor (PWAT ERA5 alternative)
o	CAPE 
The addition of more variables may be considered through the completion of initial processes and further literature review. It is important to note that all of the included derived variables are pre-processed on ERA5, which will significantly cut down on data acquisition and preprocessing time. These variables will be the input to the machine learning model. The model that will be implemented in this project is self-organizing maps (SOM). SOMs will be used to identify similar synoptic patterns and group them into nodes. From there, an analysis of the events from each node will be performed by combining all of the EROs for each member within each node, and from there create a “mean” excessive rainfall outlook by rasterizing/gridding the ERO shapefiles, and subsequently using operations in that data format. Several concerns do arise regarding the ERO shapefile portion of this project; see “Potential Issues” section for more information.

Python Tool	Purpose	Experience Level	Notes
Xarray	Gridded analyses	Fair (2/4)	Our group has done some toy examples, but never a full analysis like this
Scikit-learn	Machine learning	Poor (1/4)	Our group has only looked at the website and has never actually used this package
Cartopy	Mapping	Great (4/4)	Both group members have used this package extensively and are comfortable with it
Matplotlib	Plots	Great (4/4)	Both group members have used this package extensively and are comfortable with it
MiniSOM	Machine learning	Poor (1/4)	Neither of us have worked with this package before, but have seen peers utilize it for SOMs
Pandas	CSV utilization	Great (4/4)	Both group members have used this package extensively. This will almost exclusively be used for downloading ERA5 data via their API.





































2.	Feasibility and ambition
1. Has this type of project been done before?
Similar projects have been done, though not exactly of the same methodology:
•	The most similar project is from Schumacher et al. 2021 at Colorado State University. This group utilized random forests to create the CSU-MLP model for essentially making a first guess at WPC Excessive Rainfall Outlooks before they were issued. This allowed greater efficiency and effectiveness in forecasting excessive rainfall by quantifying risk through a model output and providing another perspective for forecasters.
•	Agel et al. 2017 had a tangential paper utilizing SOMs in the Northeast CONUS, but primarily focused on tropopause heights. While this does use early machine learning techniques, some of their methods can be considered.
•	A couple studies using GEFS reforecast, most notably Herman and Schumacher 2018, which used random forests to predict exceedance of QPF thresholds and identified the primary patterns associated with extreme rainfall.

2. Does your team have the required geoscience knowledge?
The required geoscience knowledge is considered to be in place for this project by the team. Both members are one semester away from obtaining a B.S. in Meteorology and have a background in Geographic Information Systems (GIS). Therefore, extensive exposure to geoscience/geospatial datasets has occurred within the team, meaning there is a relatively high comfort level working with such data.

3. Is your team comfortable with Python?
The team is somewhat comfortable with Python. Both members have taken multiple classes using Python and have some recent experience using Python on research projects. However, neither member has completed a research project of this caliber from start to finish and typically had code from others to reference. Additionally, neither member has performed any machine learning research projects, nor have an extensive knowledge of the processes. However, given the experience gained over the last couple of semesters, there is sufficient background in Python to complete this project effectively. 

4. How much data is required for this project? 
The total data storage cost required for this project is not excessive. In terms of the ERA5 data via the Copernicus Data Store, an exact number has not been calculated, however given estimates from their website, the total reanalysis data should about be around 10GB. This is plausible since the CONUS grid was grabbed for only 1000 timesteps at a 0.25-degree resolution. In terms of the WPC shapefile data, these have also not been calculated but will be around several hundred megabytes given the shapefiles (and its functional counterparts within each zip folder) are generally just under 1 MB. As a whole, data is NOT a major bottleneck in the process, and will not risk breaching any of the storage limits imposed by the NIU TRITON server.

5. What type of computing is required for this project (i.e., CPU vs. GPU)?
This project will require CPU due to its advantages in performing serial tasks, and that the computations of using a SOM with only a couple variables means this project will not be very computationally intensive, this GPU resources will not be necessary. 

6. What is your general understanding of all parts of this envisioned project?
A solid general understanding of the major project components has been established by the team through consistent meetings, discussion, and planning. The broad workflow that this project is expected to follow includes first parsing the WPC excessive rainfall days manually, acquiring data from both ERA5 and WPC ERO shapefiles, preprocessing this data, the application of SOMs, then interpreting the patterns that occur from running SOMs through a series of analytical figures. Additional knowledge working with SOMs and other machine learning techniques will be needed to most effectively complete this project, and this is expected to be developed through course lecture material and supplemental online resources.

7. Is this project appropriate for the experience level of the team? Explain why.
This project is considered appropriate given the level of experience of the team. The primary dataset of ERA5 has been used previously by both members for other projects, adding a solid level of familiarity with this dataset. In addition, SOMs were the chosen machine learning technique for this project because they are commonly regarded online and by peers as one of the more intuitive and beginner friendly techniques to employ. Ongoing projects using SOMs within the department will provide plenty of extra support and resources from those who are more experienced, if the team runs into any roadblocks. Overall, this project scope matches well with the group experience by including strong familiarity with the data, yet still leaving room for technical growth.
[MOU1.1]
 
Potential issues
Several potential issues may arise throughout the progression of this project. The first lies in the process of regridding and merging datasets. Given the desired variables to feed into our SOMs span anything from the surface, different pressure levels, and a column integral, data will likely need to be gathered from multiple ERA5 data sources. Specifically, the hourly data on single levels, and hourly data on pressure levels will be needed (e.g., 500 mb geopotential heights on pressure levels, while total rainwater content and soil moisture on the single levels). Thus, these two sources must be merged. Considering that both datasets use 0.25° x 0.25° grid spacing, regridding will likely not be a problem. However, if a variable from another ERA5 dataset is desired for a more comprehensive analysis, this process could result in further issues.
Another potential concern results from some EROs being too small and localized. 
Since EROs are based off of flash flood guidance, not every single day with a SLGT risk or higher will be synoptically driven, especially into the summer months. Given ERA5 has a horizontal resolution of around 30-40 km, this project may miss some of the more localized days since the synoptic pattern might be nebulous, and subtle mesoscale processes may get neglected.       
	Lastly, the categorical nature of the EROs can create potential problems. Unlike SPC outlooks, EROs had very unique probabilities assigned to the categorical outlooks (e.g., a MDT risk only 5 years ago meant 20-50%, while nowadays it means “at least 50%”). The categories and probabilities have been updated several times, which also could cause some inconsistencies. Additionally, the project aims to make mean EROs for each node, and merging shapefiles might be difficult, hence why with the probabilistic approach for EROs may be more efficient. However, that becomes a problem for the years before 2022. If the project becomes constrained to those years, a lack of data might be possible. If not, EROs are accessible dating back to 2014, which should be sufficient data coverage.
 
3.	Timeline
Task	Estimate	Confidence	Notes
Parse through ERO days 	1 week	Great (4/4)	Very simple process clicking through days and adding to the excel… busy work but not super slow
Gather ERA5 data 	1 week	Great (4/4)	The group has worked with the ERA5 data on TRITON and knows where to obtain it and how to use it
Preprocess ERA5 data	2 weeks	Fair (2/4)	The group has preprocessed ERA5 data before, but are not familiar with what format or formats we need for machine learning
Train the machine learning models	3 weeks	Poor (1/4)	No group members have trained a machine learning model before, so it is hard to anticipate how long this will take
Interrogate nodes & assign EROS	2 weeks	Poor (1/4)	Same as the above, no member has trained a model, so working with the nodes will be a new ability
Write up the results	1 weeks	Great (4/4)	Both group members have written up scientific results before and discussed them in a course paper or research article.




















6. Results
Progress towards running, training, and tuning the model goes as far as looking at PWAT and Z500, which are relatively standard metrics for excessive rainfall (Gao et al. 2014), but not extending beyond the other variables (e.g., MSLP, CAPE). When tuning the SOM, the process evaluated combinations of map size (4x4, 5x4), neighborhood radius (sigma = 1.0-2.0), learning rate (0.05-0.15), and training iterations (5000-7500). Model performance was assessed using quantization error (QE) to determine how well the model is accurately representing the data. A grid of such parameters was looped through, calculating the QE for each combination, and ranked to determine the most productive SOM. Additionally, statistics were ran to calculate which hyperparameters had the strongest influence on the SOM’s performance. [MOU2.1]The optimal combination of parameters was identified as the 5x4 SOM with sigma=1.0, learning rate=0.1, and 5,000 iterations to yield the smallest QE of 155.57. 

After running the “winning” SOM, the results yielded a modest distribution of cases per node, with the highest being in the 84 and the lowest being 24. This may also imply that some excessive rainfall synoptic regimes occur more frequently than others. Thus, the application of SOMs proved to be highly effective (Hewitson and Crane 2002, Gibson et al. 2017), as these differing regimes were easily visualized in Figure _. Overall, the results show the amplest moisture centered in the top left nodes, decreasing in moisture content moving to the bottom right, where the best moisture content gets confined to the Gulf Coast. More sensitive patterns with the height field arise from the node-to-node differences. A couple examples include further and further central ridging and eastern troughing in row 0 moving left to right, or tighter height fields moving down columns 2 and 3. 

Afterwards, the members of each node were pulled out along with their corresponding ERO, and statistical analysis was plotted. For each node, the percentage of members having any ERO category was plotted matching the grid. This allows spatial patterns to arise between the mean synoptic pattern and where a forecasted ERO would be most likely to exist. With the nodes that include a smaller extent of moisture, the heat map focuses mainly where the moisture is, but for the more widespread moist regimes, more variability on ERO frequency occurs. This visualization of the data proved to yield better results than the raw node ERO counts, which fail to visually represent the nodes that having fewer members. Similar spatial patterns evolved for utilizing the frequency map for ERO that were a SLGT or greater risk, which provides insight on where more substantial events are typically forecasted. Finally, by stacking all of the risks on top of each other allowed for the analysis of a maximum risk category plot to understand which synoptic regimes produce which prolific events, and how common they may be. Several regimes produced relatively infrequent MDT and HIGH risks, while others, especially the ones with ample moisture and a western trough, produced widespread MDT and HIGH risks across the ECONUS. 

Not only do the locations of EROs vary with synoptic regime, but the sizes do too. Similar to the above, regimes with widespread moisture tend to vary in terms of the spatial sizes of outlooks more than their confined moisture counterparts. Likewise, dominant troughing patterns appear vary less than dominant ridging patterns, which is likely a result of warm season mesoscale factors driving excessive precipitation potential. This idea drove the motivation of a seasonality plot. Many of the nodes that were suspected to occur from seasonality did, as it aligned relatively well with which three-month category the majority of members came from per node (Fig. X). Other nodes demonstrating more transient patterns do not have a dominant season, and typically were the modestly spread moisture and somewhat amplified troughing, essentially lacking extremes in terms of the synoptic attributes.

 
 
 
    
 





7. Summary 

The preliminary development of this project’s model utilized precipitable water (PWAT) and 500 mb geopotential heights (z500) by applying SOMs to generate common synoptic regimes that may dictate the spatial patterns of EROs in the ECONUS. With the WPC only providing a broad overview climatology of where EROs are issued throughout the annual cycle, much nuance was missing from this, creating the motivation behind this study. Given previous studies using these variables and methods to group synoptic regimes, the model performed adequately in its early stages. Minor tuning of the SOM was completed by running through various hyperparameter configurations until a better QE was reached.

After tuning was complete, the selected SOM was analyzed by plotting the synoptic regimes along with statistics of each node’s ERO members. Preliminary results find that this method works fairly well and quantifies patterns that are typically internal pattern recognition used during the forecast process. Such work could aid in forecasting excessive rainfall in the future as a type of “analog” system, where certain synoptic regimes may lead forecasters’ eyes to a specific portion of the ECONUS immediately, quantified by these results. 

Future work and next steps for this project include a “validation” section where a precipitation metric shall be added. This is inherently complex, as EROs are defined by flash flood guidance, which vary based on time of year, recent climate conditions, topographical and climatological effects from location, and more. Thus, the future path the group envisions is adding a total precipitation metric, likely from the PRISM dataset, in order to see what regimes lead to how much precipitation, including the extremes. This would be going down the pathway of “Practically Perfect” but instead of severe storm reports, it would be centered around excessive rainfall. 









 
8. Works Cited

Agel, L., Barlow, M., Feldstein, S.B. et al. Identification of large-scale meteorological patterns associated with extreme precipitation in the US northeast. Clim Dyn 50, 1819–1839 (2018). https://doi.org/10.1007/s00382-017-3724-8

Arguez, A., P. Bissolli, C. Ganter, R. Martinez, A. Mekonnen, L. Stevens, and Z. Zhu, Eds., 2025: Regional Climates [in “State of the Climate in 2024“]. Bull. Amer. Meteor. Soc., 106 (8), S401–S513, https://doi.org/10.1175/2025BAMSStateoftheClimate_Chapter7.1.

Burke, P. C., A. Lamers, G. Carbin, M. J. Erickson, M. Klein, M. Chenard, J. McNatt, and L. Wood, 2023: The Excessive Rainfall Outlook at the Weather Prediction Center: Operational Definition, Construction, and Real-Time Collaboration. Bulletin of the American Meteorological Society, 104, E542–E562, https://doi.org/10.1175/BAMS-D-21-0281.1.

Gao, X., C. A. Schlosser, P. Xie, E. Monier, and D. Entekhabi, 2014: An Analogue Approach to Identify Heavy Precipitation Events: Evaluation and Application to CMIP5 Climate Models in the United States. J. Climate, 27, 5941–5963, https://doi.org/10.1175/JCLI-D-13-00598.1.

Gibson, P. B., S. E.Perkins-Kirkpatrick, P.Uotila, A. S.Pepler, and L. V.Alexander (2017), On the use of self-organizing maps for studying climate extremes, J. Geophys. Res. Atmos., 122, 3891–3903, doi:10.1002/2016JD026256.

Hewitson BC, Crane RG (2002) Self-organizing maps: applications to synoptic climatology. Clim Res 22:13-26 https://doi.org/10.3354/cr022013

Kim, H., Villarini, G. Floods across the eastern United States are projected to last longer. npj Nat. Hazards 1, 23 (2024). https://doi.org/10.1038/s44304-024-00021-

Schumacher, R. S., A. J. Hill, M. Klein, J. A. Nelson, M. J. Erickson, S. M. Trojniak, and G. R. Herman, 2021: From Random Forests to Flood Forecasts: A Research to Operations Success Story. Bull. Amer. Meteor. Soc., 102, E1742–E1755, https://doi.org/10.1175/BAMS-D-20-0186.1.











9. Requirements 
Items marked in green have been completed, items marked in yellow are in progress, items in gray are to be completed, and items marked in red have been removed/revised.

PR-01: Parse WPC Days of Excessive Rainfall Risk “SLGT” or Higher
Priority: High
Sprint: 1
Assigned to: Both Members
As a developer of a machine learning model, we must sift through cases that is valid to our study in order to determine if it is worth downloading data.
Acceptance Criteria:

•	A minimum of 1000 days collected 
•	All days must contain a risk level of SLGT or higher 
•	All days must have a risk level situated in the ECONUS
Status: Complete

PR-02A: Download WPC ERO Shapefiles
Priority: High
Sprint: 1
Assigned to: Joey T
As a developer of a machine learning model, we must gather the necessary shapefile data in order to preprocess and analyze.
Acceptance Criteria:

•	Downloaded files must be saved to scratch directory 
•	Downloaded files must include all ERO outlook days corresponding to the parsed >=SLIGT and ECONUS dataset 

Automatic Test: Create a script that ensures none of the shapefiles have a maximum risk lower than ‘SLGT’. If failed, print error prompting to reanalyze downloaded data.
Status: In progress

PR-02B: Download ERA5 Data
Priority: High
Sprint: 1
Assigned to: Olivena C
As a developer of a machine learning model, we need to gather reanalysis data set so that the SOM can identify patterns/regimes associated with excessive rainfall events. 
Acceptance Criteria:

•	Downloaded files must be pulled at a similar time step to that of the issued ERO (09Z)
•	Downloaded files should bet set to ECONUS, though expanded slightly further west near the continental divide to ensure outlook coverage 
•	Downloaded files must be saved to scratch directory 
•	Downloaded files should have 2 directories: surface variables and variables at differing pressure levels
•	Downloaded files should be formatted into 1 singular file 

Automatic Test: Create a script that ensures none of the variables exist outside of the spatial and temporal domain. If failed, print error prompting to reanalyze downloaded data. 
Status: In progress 

PR-03: Preprocessing: Rasterize WPC ERO Shapefiles 
Priority: High
Sprint: 1
Assigned to: Olivena C
As a developer of a machine learning model, we must convert the vector WPC ERO shapefiles into raster format so that they can be spatially aligned with the ERA5 gridded data.
Acceptance Criteria:

•	Shapefiles must be converted from vector polygons to raster grid sets 
•	Raster grid resolution must match the ERA5 spatial grid  
•	Processes should be completed using regionmask and properly encode the categorical risk using integers as opposed to strings
•	Output should be saved as a NetCDF file

Automatic Test: Create some tests that asserts that the grids match the ERA5 grids, as well as automatically plotting the rasterized version next to the original vector form for comparison
Status: To be completed 

PR-04: Preprocessing: ERA5 data
Priority: High
Sprint: 1
Assigned to: Joey T
As a developer of a machine learning model, we need to format the data and variables that we have gathered so we can develop and train our model.
Acceptance Criteria:

•	Combine all of the ERA5 days into a singular netCDF for ease of use
•	ERA5 data should be normalized
•	ERA5 data should be flattened into a 1D array using scikit-learn
•	All of the desired variables should be concatenated to the 1D array

Automatic Test: Use a script to either interpolate or drop NaNs, and ensure time dimensions match for our variables after merging
Status: To be completed


PR-05: Train & Tune SOM
Priority: High
Sprint: 2
Assigned to: Both Members
As a developer of a machine learning model, we need to train the SOM using the ERA5 variables we downloaded to identify the atmospheric regimes that promote excessive rainfall and characterize their average magnitude and spatial structure through a mean ERO. 
Acceptance Criteria:

•	SOM model should use scikit-learn framework 
•	SOM should employ MiniSom 
•	The best representative SOM grid dimensions should be identified and employed 

Automatic Test: Create a script that runs summary statistics on the SOM nodes as sanity check for validity, essentially a tuning report card.
Status: To be completed

PR-06: Interpret/Analyze SOM Output
Priority: High
Sprint: 3
Assigned to: Both Members
As developers of a machine learning model, we need to summarize what each SOM node/regime may represent, and how regimes may differ during excessive rainfall setups.
Acceptance Criteria:

•	Composite figures of the key atmospheric regimes should be created after proper tuning has been completed
•	Statistics should be run in order to quantitively understand what each node means and how those values compare to typical synoptic setups

Automatic Test: Ensure that every day belongs to one node and does not belong to multiple
Status: To be completed

PR-07: Group EROs by SOM Node and Analyze 
Priority: Medium
Sprint: 3
Assigned to: Both Members
As a developer of a machine learning model, we need to connect atmospheric regimes capable of excessive rainfall to the overall ERO behavior.
Acceptance Criteria:

•	A script that grabs and creates statistics about all of the EROs per node should be developed (such as overall risk area, per category, probability of landing under a risk category)
•	Raster math must be ran to create a “mean ERO” 
•	Composite plots that place the newly created mean EROs atop the atmospheric regimes should be developed
•	Plots that visualize probabilities and statistics (possibly regime or seasonality histogram tables) should be created 

Automatic Test: Run a script to ensure categorical probabilities correspond to the numerical scale above after node assignments have been completed. Ensure each ERO is only assigned to one node.
Status: To Be Completed


