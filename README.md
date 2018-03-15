# DMPSJ Report on Felony Crime in DC for 2016

This is the repository that was used to produce the [DMPSJ Report on Felony Crime in the District of Columbia for 2016](http://lims.dccouncil.us/Download/39642/RC22-0132-Introduction.pdf), which is the first edition of the report required by the [NEAR Act](https://saferstronger.dc.gov/page/near-act-safer-stronger-dc) Title II Subtitle H. This repository contains all of the code and a subset of the source data used to produce the report. It also contains a data dictionary, a copy of our data use agreement with the Superior Court, and several additional files useful for following our work. The first edition of the report covers criminal justice events that occurred between January 1, 2016 and December 31, 2016 and was submitted to Council on February 2, 2018.

A copy of the raw PDF (as opposed to the exact copy received and scanned by the Council) is available in this repository and on the [Open Science Framework](https://osf.io/db8sy/).

### Requirements

The code in this repository is written in Python. We used Python 3.6.3, and in fact require Python 3.6+ due to the use of the `secrets` module. The work is done in Jupyter notebooks. If you do not have Python installed on your machine, we recommend [Anaconda](https://www.anaconda.com/download/?lang=en-us). All other Python package requirements are contained in `requirements.txt` and can be installed with `conda install -r requirements.txt -c conda-forge` if using conda, or `pip install -r requiremements.txt` if not.

### Data this repository contains

This repository contains a subset of the data used to generate this report, namely:

* Records of felony arrests made by the Metropolitan Police Department (MPD) in 2016, and
* Records of felony crime incidents recorded by MPD in 2016.

To our knowledge, this is the first time that the District of Columbia has ever released a dataset of felony arrest records. All data has been deidentified. The exact steps we took to deidentify the data are captured in the `1_data_cleaning` notebook.

The arrest records are structured such that each row represents a charge in an arrest against an individual. If an individual is arrested and charged with multiple crimes (offenses), the dataset will contain multiple rows for each charge all linked by a common arrest number. Note also that if a person was arrested and charged with both felony and misdemeanor offenses, only the felony offenses are included in this dataset. 

The Felony crime incident data is structured such that each row represents an individual involved in a crime incident (a victim or a suspect). Only the top charge in each crime incident is contained in this dataset.

In addition, for posterity, we are including copies of the public datasets we used in the creation of this report, namely the GeoJSONs used for spatial joins and records from the District of Columbia Sentencing Commission on felony sentences imposed in 2016. These came from [opendata.dc.gov](opendata.dc.gov) and the [District of Columbia Sentencing Commission](scdc.dc.gov).

In the first notebook, `1_data_cleaning`, you can see exactly what data we started with, how we cleaned it, and what subset we then used to generate the report. This notebook also takes the raw felony arrest and crime incident data, deidentifies it, and writes the output to this repository for public use. The code used to produce the figures and tables in the report is contained in `2_analysis`.

### Data this repository does _not_ contain

Datasets that we used to create the report report but which are *not* included in this repository: 

* Superior Court case data: records of all criminal court cases filed in the Superior Court of the District of Columbia between January 1, 2012 and December 31, 2016; 
* Department of Behavioral Health (DBH) data: deidentified records from DBH of services received by people who were arrested for felony crimes in 2016; 
* Crisis Intervention Officer (CIO) data: deidentified records from MPD on crisis intervention incidents 

The Superior Court data is not being published because our data use agreement with the Court prohibits releasing the data. The DBH and CIO data are not being released at this point because we want to ensure the highest level of privacy protection for health-related data. 

You can identify the names of the datasets not included in this repository by reading the `.gitignore` file. They are also explicitly referred to in both the code and the data dictionary.

### Sources of public data

#### Geospatial data

The direct links for the open data sets we used are:

* [Ward polygons](https://opendata.arcgis.com/datasets/0ef47379cbae44e88267c01eaec2ff6e_31.geojson)
* [City limits polygon](http://opendata.dc.gov/datasets/02923e4697804406b9ee3268a160db99_11.geojson)
* [Police service area polygons](https://opendata.arcgis.com/datasets/db24f3b7de994501aea97ce05a50547e_10.geojson)

Here's a quick copy and paste script to grab them:

```bash
wget https://opendata.arcgis.com/datasets/0ef47379cbae44e88267c01eaec2ff6e_31.geojson
wget http://opendata.dc.gov/datasets/02923e4697804406b9ee3268a160db99_11.geojson
wget https://opendata.arcgis.com/datasets/db24f3b7de994501aea97ce05a50547e_10.geojson
```

#### Felony sentencing data

Data on felony sentences imposed was obtained from the District of Columbia Sentencing Commission's website. We used the 2016 sentencing data, which is available online [here](https://scdc.dc.gov/node/1280281). For posterity, we have included the copy of the data actually used to generate the report in this repository.

### Limitations of this code

Note that not all of the source data is included in this repository. A consequence of that is that the source code will need to be modified before it runs on the subset of data actually available.

### Update to the report submitted to Council

This code contains an update to the report that was submitted to Council. In the initial report submitted to Council, we based our counts of arrestee characteristics on an incorrect sort order. For some of the individuals who were arrested multiple times, their age, race, and even sex were sometimes recorded differently at different arrests. We initially dropped duplicate observations of individuals and kept the records of their demographic characteristics based on an incorrect sort order. In the update, we ensure that the characteristics of an arrestee as recorded at their most recent arrest are reported. For posterity, we report the code used to create the counts in the published report and the updated counting method. The new counts are not far from the original counts submitted to Council.

### Contributors

The Report on Felony Crime in the District of Columbia for 2016 was produced by the [Office of the Deputy Mayor for Public Safety and Justice](http://saferstronger.dc.gov) in partnership with [The Lab @ DC](http://thelab.dc.gov).

The repository was authored by Eric Foster-Moore (@kindlyplease; eric.foster-moore@dc.gov), Paul Testa (paul.testa@dc.gov), and Kevin Wilson (@khwilson; kevin.wilson@dc.gov). David Yokum, Director of The Lab @ DC, and Kevin Donahue, Deputy Mayor for Public Safety and Justice, provided invaluable strategic guidance and feedback. Finally, this report would not have been possible without the collaboration and assistance we received from both the Metropolitan Police Department and the Superior Court of the District of Columbia.

Please contact Eric Foster-Moore (eric.foster-moore@dc.gov) or the thelab@dc.gov with questions.

### License

See [LICENSE.md](../master/LICENSE.md)
