# Hazard specific classification methods
This section describes in more detail, the hazard classification process for each hazard.
This section does not explicitly describe the data sources used for all hazards.
The latest data sources can be viewed on the data map at thinkhazard.org and on geonode-gfdrrlab.org.

## River Flood and Urban Flood Hazard Levels
<div class="c-box">
  <span class="box-title"><b>Classification Summary:</b></span>
  <p>The methodology for urban and river flood hazard classification was updated for ThinkHazard! version 2. 
River flood and urban flood hazard are classified using a threshold of ‘area flooded to damaging intensity threshold’. 
The damaging intensity threshold is 0.5 m for both types of flood. The area threshold is 1% of the ADM unit for river flood, and 4% of the ADM unit for urban flood (due to the additional surface flooding included in urban flood, comparably larger areas are flooded)
Hazard is classified using frequency thresholds of 10, 50 and 1000 for high, medium and low hazard, respectively.
The full river and urban flood hazard classification methodology, developed by SSBN Ltd., is provided at the public <a href="https://drive.google.com/drive/folders/0B7QVzSpnQtEnZzNUUFdNOWdLSXc?usp=sharing">ThinkHazard! Methodology Google Drive folder</a>.</p>
</div>

### Intensity
Flood hazard intensity is most commonly expressed as the water depth at a specific location, indicating severity of a flood. Flow velocity may also be given in high resolution local data but required a high level of detailed modeling. Think Hazard! is a global application, so water depth is used as the damaging intensity threshold. In determining a suitable intensity threshold, the European joint research project RiskMap  recommends four water depth classes: <0.5 m; 0.5-1.0 m; 1.0-2.0 m; and >2.0 m. The values represent typical thresholds for which significant changes in damages on buildings occur:
<ul><li>0.5 m: Flood mitigation by sandbags and other preliminary measures are no longer possible. This is a typical height of tables and light switches.
<li>2.0 m: The first floor and its interior are completely flooded.</ul>

A 0.5 m threshold is used; this provide a conservative damage threshold in line with the scope of ThinkHazard!. In version 1, global data used a threshold of 1.0 m due to concerns about uncertainties in the low-resolution elevation data leading to under- and over-estimation of depth at individual grid cells. Research by SSBN shows that at the ADM2 scale to which data are aggregated in ThinkHazard!, any errors seen in individual grid cells are largely cancelled out across the whole ADM2 Unit. 
In development of version 1 there was over-estimation of hazard when using a 0.5 m or a 1.0 m threshold. This overestimation was due to the presence of at least one grid cell exceeding these depths in most ADM2 Units, which resulted in a majority of ADM2 Units being classified as high hazard. After aggregating maximum hazard level to ADM1 and ADM0, most of the world was classified as high flood hazard. The updated methodology, considering the area flooded to a given depth threshold, overcomes the overestimation of hazard when basing the method solely on the presence of at least one grid cell exceeding the intensity threshold. 

### Frequency
The selected frequency thresholds for flood hazard are related to likelihood of experiencing flood in a human lifetime. This can be described as shown for the German Federal Office for Citizen Protection and Disaster Support (BBK, 2010; Table 3).
An alternative approach to using ranges of return periods, would be to interpolate between maps for different return periods to obtain a map for the required period. This requires spatial interpolation of hazard intensity, and uncertainties in the linearity of event boundaries and intensity distributions. Therefore, it was proposed to allow the algorithm to select a dataset within a range of return periods (100-1000 years). In version 2, the methodology explicitly uses the 1000-year return period.
The following frequency classes are used in ThinkHazard! version 2:
<ul><li>high: 10-year return period
<li>medium: 50-year return period
<li>low: 1000-year return period</ul>
    
 <br>
 <center>Example of rationale justifying the choice of return periods, for river flood hazard
    
<table><tr><td><b>Name</td><td><b>Return period</td><td><b>Rationale</td></tr>
<tr><td>High</td><td>10 years</td><td>In many cases a River Flood event of once per year or once every five years already causes considerable damage. NOTE: This return period may not be available in all flood hazard assessments. Therefore, it is proposed to allow ThinkHazard! to use 25 years as an alternative.</td></tr>
<tr><td>Medium</td><td>50 years</td><td>An event that would, on average, be expected to occur once or twice in a lifetime.</td></tr>
<tr><td>Low</td><td>10,000 years</td><td>An event most people will not experience and will only be remembered by previous generations. 
NOTE: Often the 10,000 year return period will not be available. It is proposed to use the highest available return period (and longer than 50 years) for the ‘Low’ hazard class. This can typically be between 100 and 1,000 years.</td></tr>
<tr><td>Very low</td><td>Intensity not exceeded at the ‘low’ return period used.</td><td>No floods expected based on current climate, current models and data. However, some uncertainty remains.</td></tr></table></center>

### Other notes on methodology
Areas of permanent water are masked in the method applied, so river channels and lakes are not considered in the calculation – these water bodies would contribute large areas that exceed the intensity threshold, but due to their permanent nature cannot be considered as periodically flooded. The 3 arc-second (~90m) G3WBM mask (Yamazaki et al., 2015) based on multi-temporal Landsat images is used by SSBN to mask their 90m global flood product.
Urban areas were identified for the definition of urban flood. This was using a combination of two remotely sensed datasets indicating urban activity: the Global Urban Footprint (GUF)  and the 2013 NOAA DMSP ‘stable lights’ (NTLD)  datasets.

### Results of classification
The maps below indicate the ADM2 classification based on SSBN Ltd 90 m global flood hazard maps, which is used for global coverage for river flood and urban flood hazard in ThinkHazard! version 2.

<div class="c-box-image">
  <img src="images/posts/hazardmethods/fig13.png" alt="Final classification for river flood at ADM2 level: blue = very low; yellow = low; orange = medium; red = high"/>
</div>

<div class="c-box-image">
  <img src="images/posts/hazardmethods/fig14.png" alt="Final classification for urban flood at ADM2 level: blue = very low; yellow = low; orange = medium; red = high"/>
</div>

## Coastal Flood Hazard Levels

<div class="c-box"><span class="box-title"><b>Classification Summary:</b></span>
  <p>Coastal flood is classified using onshore flood depth data, provided as frequency-severity data in raster format. The methodology follows that described in section 2.4. The damaging intensity thresholds are 2 m for high hazard, and 0.5 m for low and medium hazard. Hazard is classified using frequency thresholds of 10, 50 and 100 years for high, medium and low hazard, respectively.</p>
</div>

Coastal flooding is caused by increased elevation of coastal waters above usual sea levels commonly caused by a combination of phenomena: Astronomical tide (natural cyclic sea level variation); storm surge during a storm or cyclone (raised water elevation due to low atmospheric pressure and accumulation of water due to wind); and wave set-up resulting from the energy transferred from offshore waves to the water column at coast. Storm surge hazard maps do not necessarily include the effect of tide and wave set-up, therefore may not encompass the full potential hazard.
The extent of inundated area and the depth of floodwater depend on intensity of the event and local topography. Extensive studies and simulation are needed to determine inundation parameters from wave data, since it requires an elevation model comprising both onshore topography and sea floor bathymetry. The ideal input to Think Hazard! is onshore inundation depth maps or inundation depth at the coastline to process the hazard categorization procedure. The former has been provided with global coverage by Muis et al. (2016), who have conducted this type of analysis for coastal flooding; this dataset provides the global coverage for coastal flood hazard in ThinkHazard! version 2.

### Intensity
Damaging intensity threshold is based on a similar rationale as for river flood. The values representing typical thresholds for which significant changes in damages on buildings occur are:
<ul><li>For low and medium thresholds, 0.5 m: Flood mitigation by sandbags and other preliminary measures are no longer possible. This is a typical height of tables and light switches.
<li>For high threshold, 2.0 m: The first floor and its interior are completely flooded. More threat to life occurs with this threshold.
</ul>

### Frequency
The selected frequency thresholds for flood hazard are related to likelihood of experiencing flood in a human lifetime. The following frequency classes are used in ThinkHazard! version 2 (unchanged from version 1):
<ul><li>high: 10-year return period
<li>medium: 50-year return period
<li>low: 100-year return period</ul>
<br><br>

## Water Scarcity Hazard Levels
<div class="c-box"><span class="box-title"><b>Classification Summary:</b></span>
  <p>Hazard is classified using a Water Stress Index, which reflects the availability of water per person per year – a measure of water stress based on hydrological drought and water use.
Water scarcity is the only hazard in ThinkHazard! that uses an ‘inverse damaging intensity threshold’. All other hazards are classified based on intensity value being exceeded. Water scarcity becomes more serious as the water availability decreases, so a lower water availability per capita per year translates to higher hazard.
Hazard is classified as high, when water availability is <500 m3capita/yr at the 5-year return period. Hazard is classified medium when water availability is <1000 m3capita/yr at the 50-year return period. Finally, hazard is classified low when water availability is <1700 m3capita/yr at the 100-year return period.</p>
</div>

Discussion is ongoing over how to best represent drought in ThinkHazard! – whether meteorological, hydrological, or agricultural drought. From version 1, it was chosen to represent drought in terms of water scarcity, using a global dataset of Water Crowding Index (WCI) (Veldkamp et al., 2015) based on water availability per capita (Falkenmark et al., 1989). This index is based on estimates of water requirements in the household, agricultural, industrial and energy sectors, and the needs of the environment.
Water availability data are available as grid rasters and are summarized per water province (a combination of catchments and administrative areas), as well as for several return periods (2, 5, 10, 25, 50, 100, 250, 500 and 1000 years). Water availability is determined over these timeframes from an ensemble of five global circulation models (CMIP5), covering the historic period 1975-2004. This was combined with the population density in 2010 to determine the water availability per capita or Water Crowding Index (WCI) for the current situation.
Assumptions include: 1) This data includes surface water (rivers and lakes) and not soil moisture or groundwater; 2) Aggregation of effects to water provinces includes the effects of flow within a water province and the assumption that it is possible to mitigate drought by distributing water within a province (but not between provinces). Real water stress risks may be lower than represented by these data due to these assumptions. 
The rationale for the categorization choice is given in Table 4. Based on the return periods delimiting each category, the “best case” chance (1/best case Return Period) could be obtained.

### Intensity
It was estimated that 1700 m3 of renewable water resources per capita per year was a threshold, below which a country would experience water stress. For ThinkHazard! the threshold of <500 m3/capita/yr is used for high hazard, as it represents absolute water stress. Thresholds of <1000 m3/capita/yr and <1700 m3/capita/yr are used for medium and low hazard level, as these represent severe water stress and moderate water stress, respectively.

### Frequency
For each category of water scarcity (<500, <1000, and <1700 m3/capita/yr) and return period of original data, the average WCI in each ADM2 Unit was calculated. A trend line and corresponding (power) equation was fitted to this data, to obtain an equation with which the average return period of water stress could be calculated. The average return period and ‘best-case chance’ (i.e. longest possible return period) are related much like average and standard deviation. Both indicate how often water scarcity will occur in a certain water scarcity category, but the former represents the average chance of water scarcity occurring. The other represents the chance of a drought event occurring in the “best case” scenario where an area experiences water scarcity much less frequently than the average country of the same classified hazard. 
The following frequency classes are used in ThinkHazard! version 2 (unchanged from version1):
<ul><li>high: 5-year return period
<li>medium: 50-year return period
<li>low: 1000-year return period
    <br><br>

<table>
    <tr><td><b>Name of category</td><td><b>Best-case RP</td><td><b>Average RP</td><td><b>Best-case chance</td><td><b>Average chance</td><td><b>Rationale</td></tr>
<tr><td>High</td><td>5 years</td><td>2 years</td><td>20%</td><td>50%</td><td>This category represents areas where water scarcity is common but do not occur every year. Many countries in this category experience water stress every other year.</td></tr>
<tr><td>Medium</td><td>50 years</td><td>25 years</td><td>2%</td><td>4%</td><td>The 50 years return period was selected to represent water scarcity that occur once or twice in a lifetime. It corresponds to a large increase in number of water provinces which fall in this category.</td></tr>
<tr><td>Low</td><td>1000 years</td><td>250 years</td><td>0.1%</td><td>0.4%</td><td>Water provinces and countries in this category experience droughts less than once in a human life time, but they may occur occasionally.</td></tr>
<tr><td>Very low</td><td>>1000 years</td><td>1*10^(24) years</td><td>0%</td><td>0%</td><td>In this category no water stress is expected based on longest return period under the current climate, current models and data. However, some uncertainty remains.</td></tr></table>

For each water province and available return period it was then calculated whether Falkenmark’s threshold of 1700 m3 per capita per year was met. In other words, for each water province and return period it was determined if water stress would occur. Figure 15 shows the number of countries with a WCI below 1700 m3 of renewable water resources per capita per year for several return periods. This graph is used as basis for the categorization.

<div class="c-box-image">
  <img src="images/posts/hazardmethods/fig15.png" alt="Graph representing the number of countries with a WCI below 1700 m3 per capita per year in relation to the return period"/>
</div>

### Results of classification
The resulting water scarcity map per water province and per ADM2 Unit is shown in the figures below. The analysis was made on water province level first, because it is assumed that within a water province (a combination of watershed and countries borders) distributing of available water will occur towards water scarce areas when needed.

<div class="c-box-image">
  <img src="images/posts/hazardmethods/fig16.png" alt="Water Crowding Index – Annual water availability per capita by water province"/>
</div>

<div class="c-box-image">
  <img src="images/posts/hazardmethods/fig17.png" alt="Water Crowding Index – Annual water availability per capita by ADM2 Unit"/>
</div>

## Tropical Cyclone Hazard Levels
<div class="c-box"><span class="box-title"><b>Classification Summary:</b></span>
  <p>Tropical cyclone is classified using wind speed, provided as frequency-severity data in raster format. The methodology follows that described previously.
The damaging intensity threshold is 80 kilometers per hour for all hazard levels, using frequency thresholds of 50, 100 and 1000 years for high, medium and low hazard, respectively.</p>
</div>

Cyclone data used for hazard classification is the UNISDR Global Assessment Report 2015 (GAR15) . Based on the metadata, the “tropical cyclonic strong wind and storm surge model uses information from 2594 historical tropical cyclones, topography, terrain roughness, and bathymetry”. Topography was taken from the Shuttle Radar Topography Mission (SRTM) of NASA, which provides terrain elevation grids at a 90 meters resolution. 
The dataset covers the return periods 50, 100, 250, 500 and 1000 years, containing the peak wind velocity in kilometers per hour (km/h). No return period more frequent than 50 years is available from GAR15. Note that this data does not include extra-tropical cyclone winds, for example those that affect Western Europe. Also note that this data does not include the impact of cyclone-induced storm surges. Storm surge is available in another GAR15 dataset, but is represented in ThinkHazard!  as one component of a coastal flood dataset (section 8.2).

### Intensity
The intensity of cyclones is described by the wind speed, e.g. below figure. Based on literature review, an intensity threshold of 80 km/h is applied, which corresponds to the 50-60 miles per hour (MPH) hurricane warning threshold applied by NOAA (U.S. National Oceanic and Atmospheric Administration). The intensity threshold also corresponds to the Beaufort scale 9, described as “strong/severe gale – [at which] first damages occur”. 

<div class="c-box-image">
  <img src="images/posts/hazardmethods/fig16.png" alt="Hurricane zoning in the United States, ranging from 60 miles per hour (first damages) up to higher than 90 miles per hour (most severe damages)"/>
</div>

### Frequency
For cyclones, there are no community standards with respect to the frequency classes or return periods. Therefore, it is recommended to use the frequency classification as applied for river flood, based on human experience. However, as there is no global dataset with a return period more frequent than 50 years, the classification is as follows:
The following frequency classes are used in ThinkHazard! version 2 (unchanged from version1):
<ul><li>high: 10-year return period
<li>medium: 50-year return period
<li>low: 1000-year return period</ul>

### Results of classification
Next figure shows the results of cyclone hazard classification based on GAR15 data.

<div class="c-box-image">
  <img src="images/posts/hazardmethods/fig19.png" alt="Preliminary cyclone hazard classification for ADM2 Units using GAR15 global data"/>
</div>

## Extreme Heat Hazard Levels (new in version 2)
<div class="c-box"><span class="box-title"><b>Classification Summary:</b></span>
  <p>Extreme heat hazard classification is based on daily maximum Wet Bulb Globe Temperature, provided as frequency-severity data in raster format. The methodology follows that described in section 2.4. 
A specific temperature threshold is defined for each hazard level, at the 5, 20, and 100-year return periods, as described below. The full river and urban flood hazard classification methodology, developed by VITO, is provided at the public ThinkHazard! Methodology Google Drive folder.</p>
</div>

Extreme Heat hazard is classified based on an existing and widely accepted heat stress indicator, the Wet Bulb Globe Temperature (WBGT, in °C) – more specifically the daily maximum WGBT. The WBGT has an obvious relevance for human health, but it is relevant in all kinds of projects and sectors, including infrastructure related, as heat stress affects personnel and stakeholders, and therefore the design of buildings and infrastructure. In general, the WBGT is a relevant enough proxy to quantify the strain on physical infrastructure (energy, water, transport), such as increased demands for water and electricity, which may also affect decisions related to infrastructure.

### Intensity
Heat stress studies in the scientific literature that make use of the WBGT apply thresholds of 28°C and 32°C to categorise heat stress risk. The damaging intensity thresholds are applied folling this definition of slight/low (<28°C), moderate/high (28-32°C) and severe/very high (>32°C) heat stress:
<lu><li>high: >32°C
    <li>medium: >28°C
    <li>low: >25°C
    <li>very low: <25°C</ul>
        
### Frequency
There are no standard return periods used in research or engineering design concerning extreme heat events. However, most scientific studies use a 20-year return period in analyzing extreme heat events. This return period is included and because of the consistency with existing literature, results for this return period can be easily compared and verified with previous studies. A short return period (5 years) reflects more frequent extreme heat events, and the longest return period that can be generated based on the 30 years of available daily maximum WGBT data is 100-year return period. For longer return periods, the uncertainties in projected intensity become too large due to the inherent uncertainties in the statistical processing of the input data. 
The following frequency classes are used in ThinkHazard! version 2:
<ul><li>high: 5-year return period
<li>medium: 20-year return period
<li>low: 100-year return period</ul>

### Results of classification
The classification of hazard at ADM2 Units based on a global probabilistic WBGT extreme heat dataset developed by VITO specifically for ThinkHazard!, is as follows:

<div class="c-box-image">
  <img src="images/posts/hazardmethods/fig20.png" alt="Heat hazard classification map at the ADM2-level. The figure visualizes the location with very low (dark green), low (green), medium (orange) and high (red) extreme heat risk"/>
</div>

## Earthquake Hazard Levels
<div class="c-box"><span class="box-title"><b>Classification Summary:</b></span>
  <p>
Earthquake hazard is classified using peak ground acceleration (PGA, representing ground shaking), provided as frequency-severity data in raster format. The methodology follows that described in section 2.4.
The damaging intensity threshold is 0.2 g for high hazard and 0.1 g for medium and low hazard, using frequency thresholds of 100-250 years, 475-500 years, and 1000-2500 years for high, medium and low hazard, respectively.</p>
</div>

Earthquake hazard maps generally consist of a grid of the expected peak ground acceleration (PGA) with a 10% chance of being exceeding in a 50-year interval, which translates to a return period of 475 years. Fifty years is often considered as a standard lifespan for infrastructures. For example, the following map was recently published by the <a href="http://www.efehr.org:8080/jetspeed/portal/hazard.psml">SHARE European project</a>. The 475-year return period is a typical choice for seismic design codes for normal buildings whereas longer return periods are used as the basis of critical infrastructure such as bridges or dams (nuclear installations use even longer return periods, e.g. 10 000 years). 

<div class="c-box-image">
  <img src="images/posts/hazardmethods/fig22.png" alt="Example seismic hazard map (source: FP7-SHARE project)"/>
</div>

ThinkHazard! uses UNISDR GAR15 data to provide global coverage for earthquake hazard, but across the world relies on many regional and local datasets available in the GeoNode to provide higher resolution hazard data with fewer global assumptions. Where available, the higher resolution datasets are utilized in the hazard classification.

### Intensity
The severity of earthquake impact is commonly measured according the effects of the shaking on humans and structures. For example, the European Macroseismic Scale (EMS-98) ranks earthquakes on a 12-degree scale from “not felt” to “completely devastating”, each intensity degree denoting how strongly an earthquake affects a specific place. Intensity is subjective, determined according to post-disaster survey, from the observed effects of the earthquake. 
The European Macroseismic Scale  (EMS98), ranks seismic shaking according to effect on people, buildings and the environment. An event of EMS VI is considered to cause ‘slightly damaging’ effects to structures (Table 5), such as fine cracks in plaster, and can be felt by most people. Shaking with intensity VII result in stronger effects: people are frightened, cracks appear in buildings, and chimney start collapsing. According to widely acknowledged correlations  between intensity and PGA, intensity VI corresponds approximately to a 0.1 g and intensity VII to 0.2 g. Some earthquake hazard data are available only in EMS or Modified Mercalli Intensity (MMI). In such cases, data are converted to PGA value using conversaion equations before storage on GeoNode and import to ThinkHazard!.

Illustration of probability of damages for vulnerable buildings according to the intensity of seismic shaking (EMS98)
Degree of damage for vulnerable buildings	 	 	 	 
 Intensity VI	Many buildings	Some buildings		
Intensity VII			Many buildings	Some buildings
Hazard dataset provide seismic hazard different for PGA. To enable those datasets to be included in ThinkHazard!, several units are accepted in the processing algorithm, which can read PGA in terms of a decimal or percentage value of Gravity (g), or PGA in terms of SI units (e.g., gal or cm/s2) (see Table 6).

conversion table for units of earthquake data
<table><tr><td>Paramete unit</td><td colspan=2><table><tr><td colspan=2>Thresholds</td></tr>
    <tr><td>High</td><td>Medium and Low</td></tr></table></td></tr>
<tr><td>PGA-g</td><td>0.2</td><td>0.1</td></tr>
<tr><td>PGA-g-per</td><td>20</td><td>10</td></tr>
<tr><td>PGA-gal</td><td>196.133</td><td>98.066</td></tr>
<tr><td>PGA-cm/s²</td><td>196.133</td><td>98.066</td></tr>
<tr><td>PGA-m/s²</td><td>1.961</td><td>0.981</td></tr></table>

### Frequency
The earthquake field has standard frequencies for presenting earthquake hazard, for which maps are available from many projects. The standard used by research and engineers is to present 475, 975 and 2475 years. More commonly the 100, 250, 500, 1000, and 2500 years are used by the insurance industry. ThinkHazard! leverages these standards in setting the return periods to maximize the data that can be incorporated. Preferred values for return periods are:
<ul><li>High: 1 in 100 years (10% chance the value is exceeded in 10 years, 50% in 50 years).
<li>Medium: 1 in 475 years (2% in 10 years, 10% in 50 years). 
<li>Low: 1 in 2475 years (0.4% in 10years, 2% in 50 years).
 
If 2475-year return period data are not available, 975-year is an acceptable value (5% chance of exceedance in 50 years) for the longest return period, since it still corresponds to a low probability of exceedance on the lifespan of common projects. 
If 100-year return period data are not available, 250 years is an acceptable value (4% chance of exceedance in 10 years or 20% in 50 years) for the shortest return period, since it still corresponds to a high probability of exceedance on common projects lifespan. For medium return period, data can also be fund for 500-year return period. The 250 and 500-year return periods are often available in datasets produced for the financial sector.


