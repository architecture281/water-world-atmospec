# Water World Atmospheric Spectroscopy

*This work was completed by Marcus King as a high school senior year research project, under the mentorship of Dr. Schaefer from Stanford's Planetary Modeling Group. This project was also presented at the National Junior Science and Humanities Symposium (NJSHS) as well as the International Science and Engineering Fair, linked [here](https://isef.net/project/phys047-identification-of-water-world-exoplanet-tracers).*
## Project Summary
Recent discoveries like GJ 9827 d's water-rich atmosphere [(Piaulet-Ghorayeb et al., 2024)](https://ui.adsabs.harvard.edu/abs/2024ApJ...974L..10P/abstract) have brought to light an understudies class of exoplanets—water worlds. The discover of water in this exoplanet atmosphere simultaneously showed current capabilities while demonstrating a need to understand this type of planet better, as many similar discoveries are soon likely. Our current understanding of these water-worlds is limited by models due to the lack of reliable observations, and this study confronts this problem by developing high-resolution models of these water world atmospheres, their associated spectra, and the implications of this data with regard to exoplanet observations through the identification of tracers.

## How to Access the Spectra
The spectra files are stored as `.pkl.gz` files. You'll need to open the files in binary-read (rb) model using the gzip package, and then load them using pickle's .load function to correctly access the data, which is stored as a list of dictionaries.

## Architecture
- Equicalc (Gibbs Energy Minimization Model)
	- Used to perform equilbrium chemistry calculations
- Python packages
	- matplotlib, pandas, numpy
		- Data analysis, cleaning, and visualization
	- seaborn, plotly
		- Data visualization
	- io, os, google.colab
		- File organization & processing
	- petitRADTRANS
		- Used to model spectra from atmosphere column abundances
	- pickle, gzip
		- Used for file compression
	- sklearn
		- Used for K-means clustering analysis
## Methods & Analysis
This study employs the use of both existing chondrite composition data and equilbrium chemistry models to find an approximation for the abundances of 65 output species over a pressure-temperature space within an input grid of 23 elements. The data for this equilibrium chemistry can be found in the `enriched` and `depleted` folders. These chemistry abundances are then fit to existing pressure-temperature (P-T) gradients, and used to create full-atmosphere models of these synthetic exoplanet atmospheres [(Kempton et al., 2023)](https://iopscience.iop.org/article/10.3847/1538-4357/ace10d). 

A novel framework is created to integrate these pressure-variant atmosphere abundances via [`petitRADTRANS`](https://github.com/nborsato/petitRADTRANS), and then over 5,000 synthetic spectra are created over a grid of planetary radii and surface gravities to cover the density parameter space. A K-Means clustering algorithm (tuned via Silhouette score optimization) is then trained on the data and used to find three main clusters, and these clusters are compared to the mean transit spectra to find exoplanet tracers for these water worlds.

## Findings
Based on correlations between transit radius and cluster, key tracers were found for $\rm H_{2}, HF,$ and $\rm CO_2$, implying they have the greatest effect on the spectral features of these exoplanets. Molecular hydrogen is notably known to only accrete on more massive planets, and likely serves as an important tracer due to the planetary radius $R_p$ considered here for the spectra calculations due to the mass-radius relation. Carbon dioxide and hydrogen fluoride are both also unique, Venus-adjacent tracers, and they help reinforce the properties of these exoplanets across the parameter space. Other tracers, such as $\rm SO_{2}$ and $\rm CO$ were also identified given lower correlations. 

Based on this model, the most likely to be observed subtype of water world (e.g., cluster) is types '0' and '1', both high carbon dioxide and water vapor clusters primarily differing with respect to minor species. 

## Next Steps
Ultimately, the goal of an exploratory project like this would be for use in exoplanet survey applications. However, the current dearth of information regarding water world candidates limits these possibilities significantly. Immediate next goals would be a comparison of the spectra identified here against the spectra of NASA's Exoplanet Archive and the currently established water worlds to identify correlations and similarities, and future goals would be an application of these tracers in the analysis of a wider range of exoplanet spectra to verify the efficacy of these predictors in the true water world population. However, without a large dataset these models and tracers serve as effective representations of this exoplanet population as we know it. 
