# Data and code for 'Evaluation of vegetation indices and imaging spectroscopy to estimate foliar nitrogen across disparate biomes'

Preferred citation (DataCite format):  
 	Farella, Martha Mary; Barnes, Mallory L.; Breshears, David D.; Mitchell, Jessica; van Leeuwen, Willem J. D.; and Gallery, Rachel E. (2020)
	Data and code for "Evaluation of vegetation indices and imaging spectroscopy to estimate foliar nitrogen across disparate biomes"
  	github. Dataset. 
	https://doi.org/10.25422/azu.data.12904412

Corresponding Author:   
  Martha Farella, Indiana University, School of Public and Environmental Affairs, farellam@iu.edu

License:
    CC BY 4.0

DOI:
  https://doi.org/10.25422/azu.data.12904412


---------------------------------------------
## Summary
Dataset contains code and data used in analysis presented in manuscript.
Data was downloaded from the National Ecological Observatory Network (NEON) data portal(https://data.neonscience.org/) and includes sites where airborne hyperspectral data was collected in conjunction with foliar chemistry sampling from 2016-2019.
Data was analyzed with code included in the "code" folder (contents listed below).

---------------------------------------------
## Files and Folders


#### code: code used in the analysis presented in the manuscript. 
- download_data.R: R code to download foliar chemistry data from the NEON data portal
- plantclip_locations.R: R code to get locations for herbaceous and woody plant clip samples
- plantclip_shp.R: R code to 1.	Convert plant clip (x,y) locations to spatial points object; 2.	Define projections of plant clips based on projections of NDNI raster for each site; 3.	Extract NDNI values at location of plant clips (buffer = X); 4. combine all herbaceous (where cover > 85%) and woody samples into a single data frame and write csv
- 3mbuff.R: R code to create 3m2 rectangle buffer around all plant clip locations. Export as polygon feature class .shp file.
- brdf_topoR2py.py: python code to perform topographic and BRDF corrections on the hyperspectral reflectance data. Will need to define ross and li kernel types for BRDF correction.
- hyperspec_info.py: python code to add metadata (e.g. spatial reference info) to the topo and BRDF corrected imagery
- extract_hyperspec.py: python code to extract the corrected hyperspectral reflectance values for each of the pixels IDed in '3mbuff.R'
- ref_agg.R: R code to aggregate the reflectance values at sampleID level to get a single averaged reflectance for each sample.
- site_meta.R code to get GLI, LAI, and sample proximity meta-data for each site/sample
- Map_KG-Global.R: R code to get Koppen-Geiger climate classifications for all sample locations.
- Fig1.R: R code used to create Fig1-- plots of reflectance data by biome, run ANOVA and create boxplot of foliar N by biome
- Table2.R: R code used to create Table2-- comparing foliar N values to previously published foliar N indices. 
- FNIcalc_Fig3.R: R code to calculate Foliar nitrogen indices (FNI) for all 2-band combinations according to NDVI, RVI, and SAVI- style calculations; Add these calculated FNI values to a matrix and remove all 0 values (when band 1 and band 2 are the same band); Create a matrix of regression coefficients for all 2 band FNIs; Then, create a heat map of these results.
- PLSRloop.R: R code to perform 100 iterations of PLSR analysis saving model outputs from each run.
- Fig4.R: R code to create the PLSR VIP graphs presented in Fig. 4
- Fig5.R: R code to create a heatmap of the PLSR VIP values from FNI presented in Fig. 5
- applyPLSR.R apply PLSR model coefficients to hyperspectral readings for all locations soil was sampled
- PLSR_Testsites.R evalaute model performance at testing sites.

#### data: datasets used in the analysis and with code included 
- herbs_foliarchem_locations.csv: Locations for all herbaceous samples. output from 'plantclip_locations.R'. 
	For a description of columns, see 'allsites.csv'
- woody_foliarchem_locations.csv: Locations for all woody plant samples. output from 'plantclip_locations.R'. 
	For a description of columns, see 'allsites.csv'
- flightlines.csv: NEON flightline used for each plant sample
- allsites.csv: reflectance and descriptive variables for all of the NEON samples
	Description of columns:
	clipID: NEON defined ID for herbaceous clip samples
	indvdID: NEON defined ID for woody samples; for all SRER, the sample ID for each plot
	climate: Climate classification determined from 'Map_KG_Global.R'
	domanID: NEON defined domain ID
	ntrgnPr: % nitrogen in plant sample
	crbnPrc: % carbon in plant sample
	CNratio: value of ntrgnPr/crbnPrc
	nlcdCls: NEON defined NLCD classification
	smplTyp: type of sample values are either 'Herbaceous clip strip' or 'Woody individual'
	scntfcN: scientific name for Woody individual plant samples
	utmZone: utmZone plant sample is located in
	adjDcmlLt & adjDcmlLn: longitude and latitude coordinates of plant sample
	clpLngt: length of clip strip for herbaceous samples
	clpWdth: width of clip strip for herbaceous samples
	prcntCC: percent clip cover for herbaceous samples
	code & biome: biome delineations determined from 'Map_KG_Global.R'
	samplID: NEON defined unique ID for each sample
	siteID: NEON defined site ID
	raster: hyperspectral .h5 file associated with plant sample
	avgEasting & avgNorthing: average easting and northing coordinates for plant sample
	385 nm - 2510 nm: reflectance values in ~5 nm bandwidths from 385 - 2510 nm
- testsites.csv: reflectance and descriptive variables for all of the NEON testing samples (see 'allsites.csv' for a description of variables)
- bandcombos.csv: the 115,260 unique 2-band combos used in the FNI calculations.
	-shp_files: subfolder containt the shapefiles for each utm zone in analysis; each file contains all of the woody and herbaceous (where cover is > 85%) samples from each zone 

---------------------------------------------
## Materials and Methods
Analysis was run with R-4.0.2; and Python 3.7.0

