# Classifying hazard levels 
ThinkHazard! communicates level of hazard for 11 natural hazards, for each Administrative Unit 2 (ADM2) globally, in the classes High, Medium, Low, and Very Low. The hazard levels are used to communicate how aware a user needs to be of each hazard when planning a project at a selected location. Hazard level is aggregated to ADM1 and ADM0 unit levels, providing a view of hazard for users with a less certain project location, or projects spanning large areas in a country.
The four hazard levels are derived from hazard maps, which present the spatial distribution of hazard intensity (e.g., flood depth, ground shaking) at a given frequency, or ‘return period’ (e.g., Figure 2). A hazard map is the visualization of hazard at one point of a frequency-severity curve; the distribution of hazard intensity varies differs at each frequency. Such maps contain valuable information on where and how often an event of certain magnitude or intensity might occur, but often require specialist knowledge for interpretation. Often, it can be difficult to identify and access such maps. ThinkHazard! aims to overcome these issues by collating specialist hazard maps and communicating hazard level accurately but more simply for hazard non-specialists. 
 
<div class="c-box-image">
  <img src="images/posts/hazarddata/sharemap.png" alt="An earthquake hazard map for Europe (from the SHARE project). Hazard is shown as expected peak ground acceleration (PGA) with a 10% chance of being exceeding in a 50-year interval (return period of 475 years)"/>
</div>


Hazard levels can be described as:
•	High: Users should be highly aware of potentially severe damage from this hazard for the project location. Without taking measures to mitigate the hazard and risk, high levels of damage can be expected to occur within the project or human lifetime (and potentially frequently in that timeframe, for hydro-meteorological hazards, e.g., floods, extreme heat). 

•	Medium: Users should be aware of potentially damaging effects of this hazard for the project location. Potentially damaging events can be expected to occur within the project or human lifetime and measures to mitigate the hazard and risk should be considered. For hydro-meteorological hazards, damaging effects could occur frequently in that timeframe.

•	Low: Potentially damaging events are less likely to occur within the project or human lifetime but are still possible. Measures to mitigate the hazard and risk would be prudent at critical locations. Hazard has been classified based on long-term averages, and there is still potential that damaging events could occur in this timeframe.

•	Very Low: Available data suggest that potentially damaging effects are unlikely to occur, on average, in the project or human lifetime. Hazard has been classified based on long-term averages, and there is still potential that damaging events could occur in this timeframe.

•	No Data Available: No dataset covering the chosen location is currently available in ThinkHazard!

NOTE: The timeframe considered in classification of each hazard is dependent on historical data available to assess long-term averages, and the timescales over which the hazard causal processes operate. This is elaborated later in this chapter.
Hazard data is available at different geographic scale, spatial extent or domain, and content. It can be provided as probabilistic data, providing estimated hazard severity and frequency, or index data showing susceptibility of an area to a hazard. The type of data typically differs between hazard – earthquake and flood are generally available as probabilistic data but landslide is not. Different organizations also provide different data according to their geographic remit or focus on one hazard or one group of hazards. It has been necessary to develop a consistent framework of classification, but which is implemented in different ways to accommodate different data types. The sections below describe the input data types, data storage, selection of data source, and the classification process. 

## Input data types
ThinkHazard! accepts data in raster (grid) format only. It classifies probabilistic and index-based data using different methods, though the theory remains consistent. Probabilistic data are commonly available for: flood (river, urban and coastal), earthquake, cyclone, extreme heat, wildfire, water scarcity, and tsunami. Probabilistic data are produced for landslide and volcano in local-scale analysis, but at the global scale data are more commonly available as a spatial susceptibility index for landslide. For volcanic hazards there are very limited global sources of information: a spatial hazard index is available, but otherwise the other global source is a catalogue of previous events. 
Probabilistic data are imported to ThinkHazard! directly and all classification is conducted in the tool algorithms, described in section 0. In some cases, pre-processing is required to convert data into a format accepted by ThinkHazard!. Pre-processing comprises spatial analysis and / or data conversion prior to use in ThinkHazard!, using external GIS software such as ArcGIS or QGIS. This is described in section 2.4.2.

## Data storage
GeoNode, an open source geospatial content management system, is used to store all hazard data and additional information layers for ThinkHazard!, which is set up to retrieve data directly from a defined GeoNode server. The current version of ThinkHazard! harvests data from the GFDRR Innovation Lab GeoNode (geonode-gfdrrlab.org). 
ThinkHazard! administrators curate input data directly in GeoNode (see Section 7). This includes hazard data upload and metadata curation using the template shown in Appendix 3: Metadata template. The metadata template is adapted from an ISO standard to contain additional information specifically required for ThinkHazard!, including: hazard type, intensity unit, geographic coverage, return period and hazard set ID (all used in hazard classification), and data quality score (used in deciding which data set to use in classification). Documents provided in the further information section of ThinkHazard! are also managed in GeoNode.

GeoNode is also used in ThinkHazard! to communicate layer and document metadata and provides the route for users to download data. Clicking on a ‘data source’ or ‘further information’ link in ThinkHazard! takes the user to GeoNode, from where they can download publicly available data and reports, or navigate to the data owners’ website for access. License information for data is also stored in the layer metadata and communicated via GeoNode.

## Hazard data selection
ThinkHazard! aims to uses the best available hazard information to derive the hazard level for each administrative unit. A data selection algorithm determines which layer to use in classifying hazard levels, where more than one hazard data set is available for a hazard and ADM2 Unit (see Figure 3). This algorithm is based on the spatial extent of the data, identified from its metadata; and a data quality rating, which is stored in metadata by ThinkHazard! administrators according to criteria in Appendix 4: Data Quality Criteria.

The data quality criteria provide a high-level assessment of ‘Scientific Quality’ (i.e. is the data produced using a peer-reviewed method; is it official government data) and ‘Calculation Method Quality’, which focuses on the fidelity of the hazard model and its components (e.g. resolution of base data, vintage of analysis).

Hazard data may be available with global, regional or national coverage, depending on the scope of the generating project, or intended primary use of the data. ThinkHazard! can accept all levels of data, and implements a hierarchical selection to prefer local data (regional and national) where it is available, over global data. Global data is considered to provide a less robust view of hazard for an individual country than local data, because it is generally produced at lower resolution, and uses a greater number of global assumptions (not tailored to a regional or national situation). However, global data can provide a consistent view of hazard across all (or most) countries and is valuable in the absence of data with more local extent, which is expected to be of greater fidelity due to its more focused scope.

To summarize the data selection algorithm, conducted for each ADM2 Unit:
1.	If only one dataset is available, that dataset is used by default to classify hazard level; 
2.	If more than one dataset is available, the dataset with the highest summed data quality score is used to classify hazard level; 
3.	If more than one dataset is available, with equal summed data quality scores, then local data is preferred over global data to classify hazard level; 
NOTE: The data quality scores are assigned for the purposes of ThinkHazard! are in no way a judgment on the applicability of the data for other applications.
 
<div class="c-box-image">
  <img src="images/posts/hazarddata/decisiontree.png" alt="Decision-making algorithm for selection of data used in hazard classification
"/>
</div> 
 
## Classification Process
The ThinkHazard! hazard classification employs a spatial analysis that intersects raster hazard data, with a global raster layer describing every ADM2 Unit in the world. The ADM2 raster is derived from the FAO GAUL vector dataset of administrative unit boundaries . Three levels of administrative units are used in ThinkHazard!: ADM0 (country), ADM1 (e.g., state in the U.S.) and ADM2 (e.g., county in the U.S.).

Following the above data selection process, to determine which layer should be used for which ADM2 Unit, ThinkHazard! imports the selected data from the GeoNode database, classifies the hazard level and stores the hazard level for each hazard and ADM2 Unit in the tool database. This hazard level is communicated in text descriptions on the user interface, and the spatial distribution of hazard is also shown in the map window. 

The classification of hazard level is based on the aim to communicate how aware a user needs to be of each hazard when planning a project at a selected location, or alternatively, how frequently a project location may sustain damage from a hazard. The process relies on defining a level of hazard intensity, above which damage may occur, and the likelihood of that intensity occurring at each location.

### Probabilistic data
ThinkHazard! uses frequency and severity information to communicate how frequently a project location may sustain damage from a hazard. This is a well-defined process for probabilistic data, which provide both elements required for this assessment (estimates of hazard frequency and severity).
To do this, we first identify an intensity level for each hazard, above which damage is expected to occur, and then assess how frequently that intensity might be exceeded. This information is available on frequency-severity curves, which are a product of probabilistic analysis (see Figure 4, right). The more common use of these curves is to define how severe an event would be at a defined frequency (Figure 4, left) to define required building strength, for example. The first formulation is chosen as the key communication point, because ThinkHazard! aims to help users prioritize and manage multiple hazards with the greatest chance of causing damage to their interests, rather than identify the exact impact (this should be done in a more focused risk assessment as part of the project).  
Frequency of a hazard intensity being exceeded can be defined in terms of average recurrence interval, or return period, expressed as ‘1 in 100 years’, or the ‘100-year return period’. Alternatively, this can be expressed as the chance of the intensity value being exceeded on an annual basis: for the 100-year return period hazard this would be 1% chance of exceedance in any given year (1.0% = 1/100); for the 500-year return period this is 0.2% (0.2% = 1/500). This report uses return period as the reference to frequency. Longer return periods correspond to having a smaller chance that the damaging intensity will be exceeded during the reference timeframe lifetime, hence the risk of damage is lower.
 
<div class="c-box-image">
  <img src="images/posts/hazarddata/approach.png" alt="Comparison of Think Hazard frequency-based approach, and common intensity-based approach"/>
</div>

#### Classification steps
A step by step procedure is applied to classify hazards based on probabilistic data in ThinkHazard!. This procedure is applied for each ADM2 Unit:
1.	Hazard = HIGH if hazard intensity exceeds, at any location in the ADM2 Unit, the damaging intensity threshold at the shortest return period (highest frequency threshold); 

2.	Hazard = MEDIUM if (1) is not satisfied and if hazard intensity values exceed the damaging intensity threshold at the medium return period;

3.	Hazard = LOW if (1, 2) are not satisfied and if the hazard intensity values exceed the damaging intensity threshold at the longest return period (lowest frequency threshold);

4.	Hazard = VERY LOW if (1, 2, 3) are not satisfied in data values given for the ADM2 Unit.

5.	NO DATA is recorded if there are no data values given for the ADM2 Unit.

The ‘damaging intensity threshold’ and ‘frequency threshold’ are described in the next two sections.

#### Damaging intensity threshold
Damaging intensity threshold, the intensity above which damage would be expected to occur, is defined specifically for each hazard (Table 1). In this version of ThinkHazard! the type of project is not specified by the user, and guidance is intended to be project- and sector-agnostic, to be applicable to a wide range of project types. The defined damage threshold is therefore not tailored specifically to account for damage to any specific group of structures or infrastructure. Conservative (i.e. low) damage thresholds are used because they are intended to reflect intensity that can cause damage for projects in International Development Association (IDA) countries, in which investments may be more vulnerable (in relation to construction and/or availability of resources for recovery). Therefore, the thresholds used may be not be realistic in relation to highly-engineered structures. Later sector-specific versions of ThinkHazard!, may have damage thresholds tailored to that sector, for example, using construction standards for critical facilities to determine the intensity of event that could be considered damaging.

The three intensity thresholds for a hazard can be identical across the hazard levels, or they can differ to provide the flexibility to further distinguish each hazard level. For example, earthquake shaking reaching intensity VI on EMS98 scale are considered damaging for most projects, so the equivalent ground acceleration value of 0.1 g is defined as the intensity threshold for very low, low and medium hazard. For high hazard, the threshold reflects an intensity value typical of more damaging events that cause damage to structures: 0.2 g. In doing so, the number of high hazard zones is reduced compared to if a threshold of 0.1 g had been used, preserving the significance of high hazard by not distributing ‘high’ widely. 

Hazard data for the same hazard may be provided with different intensity units. For example, earthquake ground acceleration can be provided in gal, g as a decimal, or g as a percentage. Flood depth may be provided in m, cm, or dm (decimeter). The unit for each data layer is defined in its metadata, and ThinkHazard! classifies the data according to the correct unit.

A summary of damaging intensity parameters, units and thresholds used in the classification of probabilistic data (only one common unit shown for hazard):

<center><table><tr><td><b>Hazard</td><td><b>Intensity parameter</td><td><b>Intensity Unit</td><td colspan=3><table><tr><td colspan=3><b>Intensity threshold value</td></tr><tr><td><b>High</td><td><b>Medium</td><td><b>Low</b></td></tr></table></td></tr>
<tr><td>Earthquake</td><td>Acceleration (PGA)</td><td>g</td><td>0.2</td><td>0.1</td><td>0.1</td></tr>
<tr><td>Extreme heat</td><td>Wet Bulb Globe Temperature (WBGT)</td><td>°C</td><td>32</td><td>28</td><td>25</td></tr>
<tr><td>River flood*</td><td>Inundation depth</td><td>m</td><td>0.5</td><td>0.5</td><td>0.5</td></tr>
<tr><td>Urban flood*</td><td>Inundation depth</td><td>m</td><td>0.5</td><td>0.5</td><td>0.5</td></tr>
<tr><td>Coastal flood</td><td>Inundation depth</td><td>m</td><td>2</td><td>0.5</td><td>0.5</td></tr>
<tr><td>Cyclone</td><td>Mean wind speed</td><td>km/h</td><td>80</td><td>80</td><td>80</td></tr>
<tr><td>Tsunami</td><td>Coastal maximum amplitude</td><td>m</td><td>2</td><td>1</td><td>0.5</td></tr>
<tr><td>Water scarcity</td><td>Water availability</td><td>m3/capita/yr</td><td><=500</td><td><=1000</td><td><=1700</td></tr>
<tr><td>Wildfire</td><td>Canadian Fire Weather Index</td><td>FWI</td><td>30</td><td>20</td><td>15</td></tr></table></center>

* Although river flood and urban flood data are provided as probabilistic data, it was found in ThinkHazard! version 1 that use of a damaging intensity alone overestimates high hazard (it is common for flood data to have a very small number of cells attributed to high hazard, which overestimate the hazard for the whole ADM2 Unit). Therefore, it was decided to use an additional spatial assessment in a pre-processing stage, to classify hazard based on a minimum area exceeding the damaging threshold. Further information is given in section 8.1.

#### Frequency thresholds
Frequency thresholds determine which hazard level is assigned to a location, given that the damaging intensity threshold is achieved. These thresholds are assigned on a hazard-specific basis, based on de facto standards for a given peril – i.e. the return periods at which data are usually produced. The common return periods reflect the timescales over which a hazard operates. For example, damaging floods occur more frequently than earthquakes due to atmospheric process operating on much shorter timeframes than tectonic processes.

Return periods may vary depending on the source of the data: earthquake data are more commonly produced at the 100, 250, 500, and 1000 years by the insurance industry due to their required outputs, instead of the standard 475, 975 and 2475 years used by researchers and engineers. For flood data, return periods commonly include some but not all of 5, 10, 25, 50, 100, 500, and 1000 years. ThinkHazard! has some flexibility to account for these differences in the classification, i.e., a 475 or 500-year return period is used to classify medium hazard. This enables as many datasets as possible to be used. De facto return periods do not exist for all hazards. In these cases, the frequency thresholds are defined using expert judgement based on the frequency of impacts. Generally, hazards threatening life due to construction damage (earthquake, cyclone, volcanoes) can be assessed considering, at a minimum, a 50 years lifespan. Hazards threatening people’s living conditions more regularly (flood, drought) are often assessed using shorter durations (e.g., 10 years).

ThinkHazard! uses the return periods given in Table 3Error! Reference source not found. to classify hazard based on probabilistic data. A value range indicates the maximum range that can be used in the calculation. The administrator can determine the exact return period used by including (or excluding) certain return periods from data storage and import to ThinkHazard!. 

Suggested return periods for each hazard classified from probabilistic data:

<center><table><tr><td><b>Hazard</td><td colspan=3><table><tr><td colspan=3><b>Return period (years)</td></tr><tr><td><b>High</td><td><b>Medium</td><td><b>Low</b></td></tr></table></td></tr>
<tr><td>Earthquake</td><td>100 - 250</td><td>475 - 500</td><td>1000 - 2500</td></tr>
<tr><td>Extreme heat </td><td>5</td><td>20</td><td>100</td></tr>
<tr><td>River flood</td><td>10</td><td>50</td><td>1000</td></tr>
<tr><td>Urban flood</td><td>10</td><td>50</td><td>1000</td></tr>
<tr><td>Coastal flood</td><td>10</td><td>50</td><td>100</td></tr>
<tr><td>Cyclone</td><td>50</td><td>100</td><td>1000</td></tr>
<tr><td>Tsunami</td><td>100</td><td>500</td><td>2500</td></tr>
<tr><td>Water scarcity</td><td>5</td><td>50</td><td>1000</td></tr>
<tr><td>Wildfire</td><td>2</td><td>10</td><td>30</td></tr></table></center>

### Pre-processed data
Preprocessing of data into a format suitable for ThinkHazard! may be needed if:
1.	Original hazard data are not available with frequency and severity information as provided by probabilistic data. These are ‘non-probabilistic data’.
a.	Volcanic hazard data, globally, is not is not widely communicated probabilistically, so global hazard levels can only be derived based on databases of eruptive histories. Hazard data for individual sites / small areas may be the exception. See section 8.9 for more information.
b.	Landslide hazard data. Global landslide data is presently available as susceptibility classes or hazard classes, because there is insufficient historical information to understand the frequency of events on such a wide scale. See section 8.10 for more information.
c.	Note that probabilistic data for the volcanic and landslide hazards are more likely to be available at regional and local scale. Where such analysis is available, we will seek to use the information in ThinkHazard!.

2.	Available hazard data do not intersect administrative units, preventing use of the general procedure. This is true of some coastal hazard data, e.g., tsunami, which are often provided as data points at some distance offshore because there is high computational expense of simulating flow onto land large areas. Depending on the location of points, some pre-processing is required to transfer the data points to the coastline or onshore. This is may be through spatial analysis to relocate points with the same values, or may involve analytical steps that account for change in values to the new location (e.g., application of tsunami run-up equations). See section 8.7 for more information.

3.	Where classification of intensity is insufficient to determine variations in hazard level at the Administrative Unit scale. River flood and urban flood damaging intensity thresholds are found to be exceed at least one grid cell in most Administrative 2 Units, leading to a large proportion of areas with high hazard. This was the case in ThinkHazard! version 1, and makes it difficult to define and communicate the truly high hazard areas. To resolve this, hazard classification in ThinkHazard! version 2 uses the ‘area of an Admin 2 unit flooded’ to the damaging intensity, which identifies the units with most area flooded to a damaging flood depth. See section 8.1 for more information.

### Aggregating hazard levels
Hazard classification is conducted for at the level of ADM2 Unit. That is, ThinkHazard! calculates the hazard level for each Admin 2 Unit in the world, by applying the process shown in section 2.4.1.1 to the grid cells within each ADM2 Unit boundary. The hazard level of a higher level ADM1 or ADM0 units is defined as the maximum hazard level in all lower units that it contains. In Figure 5, the Moroccan ADM1 unit named Center comprises eight ADM2 units. At the ADM2 level, there are some classified as ‘Low’ hazard (e.g. Settat) but the maximum hazard level is ‘High’ (Azilal and Beni Mellal) so the hazard level of ADM1 unit Center, is classified as ‘High’. The hazard levels in the six ADM1 units of Morocco are ranked in this example as either ‘Low’ or ‘High’. The ADM0 unit (Morocco) takes the maximum hazard level: in this case, ‘High’.

The aggregation process means that, in the extreme case, just one ADM2 unit in a country categorized as ‘High’, would result in the user seeing a ‘High’ hazard level for the whole country. This is intentionally conservative, so that ThinkHazard! shows the maximum hazard in any ADM unit. This is to safeguard against underestimating the overall hazard, when a large area (e.g., Province or country) is selected. The hazard map on the user interface provides further context, showing the distribution of hazard level across ADM units within the selected unit, enabling the user to see how the hazard level varies across the whole unit. 

<div class="c-box-image">
  <img src="images/posts/hazarddata/aggregation.png" alt="Principles of hazard level aggregation from ADM2 up to ADM0 (country level)"/>
</div>



# Communication of hazard levels
Hazard level is communicated through text description and color. On the location overview page, the horizontally arranged hazard icons are colored according to hazard level (High: red, through orange, to Very Low: yellow). On the overview page, the 11 hazards are listed vertically according to hazard level, with a colored text label. 

<div class="c-box-image">
  <img src="images/posts/hazarddata/hazlevThailandov.png" alt="Hazard levels communicated via the multi-hazard overview page"/>
</div>

On the hazard-specific page, the colored icons of all hazard are retained, and a colored text label specific to the hazard is shown. All icons are shown on every page, to always highlight the presence of multiple hazards, and to provide easy navigation to other hazards.
The spatial distribution of hazard is also shown in the map window. The map window provides limited user navigation. The user can select neighboring units, or zoom in and out to hierarchically-associated units (e.g., from ADM0 to ADM1 to ADM2, and vice versa). 

There is a text description of what the hazard means for the user, in terms of the likelihood of damage, and encourages the user to take the hazard into consideration appropriately. For example:
‘In the area you have selected river flood hazard is classified as high based on modeled flood information currently available to this tool. This means that potentially damaging and life-threatening river floods are expected to occur at least once in the next 10 years. Project planning decisions, project design, and construction methods must take into account the level of river flood hazard. The following is a list of recommendations that could be followed in different phases of the project to help reduce the risk to your project. Please note that these recommendations are generic and not project-specific.’
A brief statement is made to describe the potential impact of climate change on the hazard. This statement is derived from expert knowledge of the hazard, and IPCC  reports, and is specific to the hazard and the region. For example: ‘Climate change impacts: High confidence in an increase in intense precipitation. The present hazard level is expected to increase in the future due to the effects of climate change. It would be prudent to design projects in this area to be robust to river flood hazard in the long-term.’
 
<div class="c-box-image">
  <img src="images/posts/hazarddata/hazlevThailandcy.png" alt="Hazard levels communicated via the single-hazard and risk reduction guidance page"/>
</div>

