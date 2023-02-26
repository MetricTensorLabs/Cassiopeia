# Star Catalogue

## Zhang - Star Identification: Methods, Techniques and 

Frequently used star catalogues include the U.S. Smithsonian Astrophysical Observatory Catalogue,Hipparcos Catalogue, Henry Draper Catalogue, Bright Star Catalogue, etc. The SAO J2000 (epoch = J2000) compiled by the U.S. Smithsonian Astrophysical Observatory, recording around 250,000 stars brighter than 17 Mv, is adopted as the standard catalog internationally.


### Smith - Development and Implementation of Star Tracker Based Attitude Determination (2017)
Tycho-2 catalog is the largest collection of stars available, with over 2.5 millions stars recorded from the European Space Agency's Hipparcos Satellite. Along with vast number of stars available, the Tycho-2 catalog is used due to the Hipparcos satellite's ablity to measure changes in a star's position on the order of milliarcseconds per year.

### Sarvi(et. al.) - Design and Implementation of a star-tracker (2015)
In out star sensor, the Hipparcos star catalogue will be used.

## Bratt - Analysis of Star Identification Algorithms due to Uncompensated Spatial Distortion (2013)

Of the catalogs listed, few provide the direct information necessary for star identification as required in this analysis. From this list the most relevant for use of star identification were the Henry Draper, PPM, Hipparcos, and Tycho catalogs.

1. **Henry Draper Database** The Henry Draper star catalog used a prism in front of the telescoping lens to spread the light according to wavelength to obtain spectral information per star. This provides a highly specific means of identifying stars, as each star would emit a unique wavelength spectra. It is a whole sky catalog observing stars up to a magnitude of nine. 

2. **PPM Database** The PPM (Positions and Proper Motions) catalog covers nearly two hundred thousand stars north of the 2.5 degree southern declination for the epoch J2000. The main purpose of the catalog was to provide a dense and accurate net of astrometric reference stars on the northern celestial hemisphere. 

3. **Hipparcos-Tycho Databases** The Hipparcos and Tycho catalogs were developed in 1989 with the launching of the ESA’s (Eurpean Space Agency’s) funded satellite Hipparcos which flew from 1989 to 1993. This name comes from the acronym for High Precision Parallax Collecting Satellite. Its main function was to obtain accurate parallax measurements and star intensities. The Hipparcos database was published in 1997 and cataloged precise lightyear distances and ECI positioning of 118218 principal stars to a resolution of 1 milliarcsecond; an updated version with re-processed data was published in 2007. The Hipparcos catalog was particularly8 notable for its stellar parallax measurements, which were more accurate than those produced by ground- based observations. The Tycho catalog contains nearly ten times more stars, each measured 130 times during the mission to an accuracy of 25 milliarcseconds.

<p align="center">
  <img src="https://github.com/MetricTensorLabs/Star-Tracker/blob/main/documents/notes/figs/bratt_star_catalogue_list.png" width="700">
  </br>
  <em>Fig. Summary of star catalogs</em>
</p>


**Selection**</br>
The Hipparcos Database was chosen due to its high positioning knowledge to 1 milliarsecond and for its comprehensive database listing of stars. It contained a sufficient number of stars in both hemispheres for the ability to identify stars globally. Star intensity information allowed for variability in testing of camera parameters during simulation and experimental analyses. A fully updated version of the database was published in 2007 and was well known for its ease in star indexing and precession.






