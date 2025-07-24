# Summarize Demographics ArcGIS Tool - beta version

Megan Kung, Equity Data Specialist, OPEETA, State Water Resources Control Board, megan.kung\@waterboards.ca.gov

### Overview

Areas of interest to the Water Boards often do not align with Census-designated boundaries, making it difficult to estimate the demographics of a population within areas being considered for Water Board actions, such as watersheds, drinking water systems, or contaminated groundwater plumes. Following the methodology of USEPA's EJScreen version 2.3 ([mirror site](https://pedp-ejscreen.azurewebsites.net/)), the Water Boards' ArcGIS Pro Summarize Demographics tool allows staff to easily create demographic summaries for one or multiple areas of interest.

Specifically, the tool estimates total population and population-weighted averages of 2023 median household income, race, and languages spoken at home for those who speak English "not very well" within user-specified boundaries.

### Files

-   **CA_Demographic_Analysis.ppkx** - ArcGIS Pro package that contains Summarize Demographics tool in the project toolbox as well as layers as described in 'Package layers' section

-   **Summarize_Demographics_code.py** - Python code for the Summarize Demographics tool

### **Setup**

1)  Download the "CA_Demographic_Analysis.ppkx" to a folder you would like to work from, then open in ArcGIS Pro. You can find the tool in the Project Catalog, under Toolboxes \> CA_Demographic_Analysis.atbx \> Summarize Demographics.

    <img src="https://github.com/user-attachments/assets/6c786a64-5dd2-42ce-9146-1a89299086b7" alt="Image" width="1427" height="779"/>

2)  Assuming you already have shapefiles or geodatabase files for your boundaries of interest, connect to the folders where those files are located by right-clicking on Folders in the Catalog. Click 'Add Folder Connection' and select the folder where your boundary files are located. Right-click on the file and click 'Add to Current Map'.

    <img src="https://github.com/user-attachments/assets/8560e506-230a-412d-96e0-5d073b4fd31b" alt="Image" width="1486" height="827"/>

3)  Double-click on the Summarize Demographics tool. Fill in the parameter fields, described in pop-up fields if you hover over the red asterisk and in the following 'Tool Parameters' section. Click 'Run', cross your fingers, and say a prayer to the GIS gods.

    <img src="https://github.com/user-attachments/assets/38df2891-f00e-419f-9590-6fddc7b9c27c" alt="Image" width="1486" height="826"/>

4)  If all goes well, it should create an Excel report of summary demographic statistics exported to the folder you specified in the tool.

    <img src="https://github.com/user-attachments/assets/6fe1f1cc-42a5-4d35-9158-636c3e6c00eb" alt="Image" width="1285" height="969"/>

### Tool Parameters

-   **Analysis boundaries** - feature layer of single or multiple boundaries on which to summarize demographics. Layer must be shapefile or geodatabase file.
-   **Analysis ID** - ID variable from the analysis boundaries layer over which to summarize. Field must be text and unique, meaning each ID value can only appear once. Do NOT select OBJECTID.
-   **Export file** - filename and location for summary output.

### Package layers

The **CA_Demographics_2023** layer contains data on the aforementioned variables, which were compiled from the 5-year 2019-2023 U.S. Census American Community Survey, as well as disadvantaged community status by block group. The definition of disadvantaged community follows Water Code 79505.5, where a community with an annual median household income less than 80% of the statewide median household income is considered disadvantaged, and a community with an annual median income less than 60% is considered severely disadvantaged. Income and race data were collected at the block group level, and language data was collected at the census tract level.

The **Tribal_Lands_and_Tracts** layer is a union of two layers, PRO_Indian_Lands and PRO_Tracts_All, from the Pacific Region Office of the Bureau of Indian Affairs.

**Demographic_analysis_layer_2023** is a compilation of 2020 block-level population data and 2023 data from the CA_Demographics layer. This layer is what the Summarize Demographics tool utilizes for its estimates. In most cases, the user can ignore this layer.

### Apportionment

When the user specifies analysis boundaries that do not align with Census boundaries, Census polygons will fall partially within and outside the analysis boundaries. The Summarize Demographics tool accounts for this by apportioning based on population weighting at the Census block level, following the methodology of US EPA's EJScreen version 2.3 ([mirror site](https://pedp-ejscreen.azurewebsites.net/)). Note that as long as the user chooses analysis boundaries much larger than one block group, estimates should be reasonably representative of the population within the boundaries. Use caution with analysis boundaries that are about the size of only a few block groups or smaller. More details can be found in the [EJScreen Technical Documentation](https://www.epa.gov/system/files/documents/2024-07/ejscreen-tech-doc-version-2-3.pdf) under the Buffer Reports section.

### Tips

-   Analysis ID variable must be unique and in text format.
-   Make sure there are no spaces in your analysis layer name.

### Notes

-   CalEnviroscreen 4.0 scores were not incorporated due to its use of 2019 data, which was based on Census boundaries that differ from 2023. OPEETA staff plan on incorporating CES scores when CalEnviroscreen is next updated.
-   The summarized MHI23 (median household income 2023) value in the tool output is the population-weighted mean value of median household income. Due to data limitations, the actual median household income is not estimated, but the estimated mean income value is a reasonable approximation. In areas where the income distribution is more skewed, i.e. there are relatively few people with incomes that are much higher or lower than everyone else, the mean value will differ more from the median.

### Data Dictionary

| Variable | Description |
|----|----|
| TotalPop | Total population |
| MHI23 | Median Household Income |
| White | White (non-Hispanic) |
| Black | Black (non-Hispanic) |
| AmerInd | American Indian (non-Hispanic) |
| Asian | Asian (non-Hispanic) |
| PacIsl | Pacific Islander (non-Hispanic) |
| Other | Other (non-Hispanic) |
| Mixed | Mixed race (non-Hispanic) |
| Hisp | Hispanic |
| White_Perc | Percent white (non-Hispanic) |
| Black_Perc | Percent Black (non-Hispanic) |
| AmerInd_Perc | Percent American Indian (non-Hispanic) |
| Asian_Perc | Percent Asian (non-Hispanic) |
| PacIsl_Perc | Percent Pacific Islander (non-Hispanic) |
| Other_Perc | Percent Other race (non-Hispanic) |
| Mixed_Perc | Percent mixed race (non-Hispanic) |
| Hisp_Perc | Percent Hispanic |
| English_Only_Perc | Percent households where only English is spoken |
| Spanish_Perc | Percent Spanish-speaking households where English is spoken "not very well" |
| French_Haitian_Cajun_Perc | Percent French, Haitian, and Cajun-speaking households where English is spoken "not very well" |
| German_WestGermanic_Perc | Percent German and West-Germanic-speaking households where English is spoken "not very well" |
| Russian_Polish_Slavic_Perc | Percent Russian, Polish, and Slavic-speaking households where English is spoken "not very well" |
| OtherIndoEuro_Perc | Percent other Indo-European-speaking households where English is spoken "not very well" |
| Korean_Perc | Percent Korean-speaking households where English is spoken "not very well" |
| Chinese_Perc | Percent Chinese-speaking households where English is spoken "not very well" |
| Vietnamese_Perc | Percent Vietnamese-speaking households where English is spoken "not very well" |
| Tagalog_incl_Filipino_Perc | Percent Tagalog including Filipino-speaking households where English is spoken "not very well" |
| OtherAsianPacIsl_Perc | Percent other Asian Pacific Islander-speaking households where English is spoken "not very well" |
| Arabic_Perc | Percent Arabic-speaking households where English is spoken "not very well" |
| OtherLang_Perc | Percent other language-speaking households where English is spoken "not very well" |
| Num_of_blocks | Number of blocks used to estimate total population and averages of demographic variables; only included in output table from Summarize Demographics tool |

### Feedback

Please fill out this [survey](https://forms.gle/c6PiRo5QfR6wQDEE9) to let me know how the tool worked for you!
