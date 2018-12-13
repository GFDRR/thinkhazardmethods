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
    
<center>Example of rationale justifying the choice of return periods, for river flood hazard</center>
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
<li>low: 1000-year return period</ul>
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
Heat stress studies in the scientific literature that make use of the WBGT apply thresholds of 28°C and 32°C to categorise heat stress risk. The damaging intensity thresholds are applied folling this definition of slight/low (<28°C), moderate/high (28-32°C) and severe/very high (> 32°C) heat stress:
<ul><li>high: >32°C
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

<div class="c-box-image"><img src="images/posts/hazardmethods/fig22.png" alt="Example seismic hazard map (source: FP7-SHARE project)"/>
</div>

ThinkHazard! uses UNISDR GAR15 data to provide global coverage for earthquake hazard, but across the world relies on many regional and local datasets available in the GeoNode to provide higher resolution hazard data with fewer global assumptions. Where available, the higher resolution datasets are utilized in the hazard classification.

### Intensity
The severity of earthquake impact is commonly measured according the effects of the shaking on humans and structures. For example, the European Macroseismic Scale (EMS-98) ranks earthquakes on a 12-degree scale from “not felt” to “completely devastating”, each intensity degree denoting how strongly an earthquake affects a specific place. Intensity is subjective, determined according to post-disaster survey, from the observed effects of the earthquake. 
The European Macroseismic Scale  (EMS98), ranks seismic shaking according to effect on people, buildings and the environment. An event of EMS VI is considered to cause ‘slightly damaging’ effects to structures (Table 5), such as fine cracks in plaster, and can be felt by most people. Shaking with intensity VII result in stronger effects: people are frightened, cracks appear in buildings, and chimney start collapsing. According to widely acknowledged correlations  between intensity and PGA, intensity VI corresponds approximately to a 0.1 g and intensity VII to 0.2 g. Some earthquake hazard data are available only in EMS or Modified Mercalli Intensity (MMI). In such cases, data are converted to PGA value using conversaion equations before storage on GeoNode and import to ThinkHazard!.

Illustration of probability of damages for vulnerable buildings according to the intensity of seismic shaking (EMS98)
<table><tr><td>Degree of damage for vulnerable buildings</td><td><img src="images/posts/hazardmethods/hq1.png"></td><td><img src="images/posts/hazardmethods/hq2.png"></td><td><img src="images/posts/hazardmethods/hq3.png"></td><td><img src="images/posts/hazardmethods/hq4.png"></td></tr>
<tr><td>Intensity VI</td><td>Many buildings</td><td>Some buildings</td><td></td><td></td></tr>
<tr><td>Intensity VII</td><td></td><td></td><td>Many buildings</td><td>Some buildings</td></tr></table>

Hazard dataset provide seismic hazard different for PGA. To enable those datasets to be included in ThinkHazard!, several units are accepted in the processing algorithm, which can read PGA in terms of a decimal or percentage value of Gravity (g), or PGA in terms of SI units (e.g., gal or cm/s2) (see Table 6).

Conversion table for units of earthquake data
<table><tr><td>Parameter unit</td><td colspan=2><table><tr><td colspan=2>Thresholds</td></tr>
    <tr><td>High</td><td>Medium and Low</td></tr></table></td></tr>
<tr><td>PGA-g</td><td>0.2</td><td>0.1</td></tr>
<tr><td>PGA-g-per</td><td>20</td><td>10</td></tr>
<tr><td>PGA-gal</td><td>196.133</td><td>98.066</td></tr>
<tr><td>PGA-cm/s²</td><td>196.133</td><td>98.066</td></tr>
<tr><td>PGA-m/s²</td><td>1.961</td><td>0.981</td></tr></table>

### Frequency
The earthquake field has standard frequencies for presenting earthquake hazard, for which maps are available from many projects. The standard used by research and engineers is to present 475, 975 and 2475 years. More commonly the 100, 250, 500, 1000, and 2500 years are used by the insurance industry. ThinkHazard! leverages these standards in setting the return periods to maximize the data that can be incorporated. Preferred values for return periods are:
<ul><li>High: 1 in 100 years (10% chance the value is exceeded in 10 years, 50% in 50 years)
<li>Medium: 1 in 475 years (2% in 10 years, 10% in 50 years)
<li>Low: 1 in 2475 years (0.4% in 10years, 2% in 50 years)</ul>
 
If 2475-year return period data are not available, 975-year is an acceptable value (5% chance of exceedance in 50 years) for the longest return period, since it still corresponds to a low probability of exceedance on the lifespan of common projects. 
If 100-year return period data are not available, 250 years is an acceptable value (4% chance of exceedance in 10 years or 20% in 50 years) for the shortest return period, since it still corresponds to a high probability of exceedance on common projects lifespan. For medium return period, data can also be fund for 500-year return period. The 250 and 500-year return periods are often available in datasets produced for the financial sector.

## Tsunami Hazard Levels
<div class="c-box"><span class="box-title"><b>Classification Summary:</b></span>
  <p>Tsunami hazard data at the scales appropriate for use in ThinkHazard! is generally presented as maximum wave amplitude or height, usually at 100 m water depth, provided as frequency-severity data in raster format. The methodology follows that described in section 2.4. The damaging intensity threshold is 2 m for high hazard, 1 m for medium hazard, and 0.5 m for low hazard, using frequency thresholds of 100 years, 500 years, and 2500 years for high, medium and low hazard, respectively.</p>
</div>

It is decided that a threshold of 0.5 m should be used for low hazard, as it represents a height at which land and buildings are flooded, and which allows for some uncertainty in offshore values of tsunami translated to potential onshore impacts. A value of 1.0 m for medium hazard is proposed to distinguish areas of known hazard e.g., Eastern Mediterranean Sea from areas of lower hazard (e.g., Western Africa). High hazard is classified using a higher threshold of 2.0 m, which corresponds to the depth at which building damage ratio increases significantly, based on post-disaster surveys in Japan, 2011 (MLIT, 2012). 
GFDRR commissioned analysis by the Norwegian Geotechnical Institute, Geoscience Australia, and INGV Italy (under the umbrella of the Global Tsunami Model) to make data developed by Davies et al. (2017) openly available at several return periods. The dataset provides run-up values calculated at offshore hazard points, which have been projected to the shoreline by simple interpolation (described in the NGI report, in ThinkHazard! Methodology Google Drive folder). These coastal values have been rasterized at 0.01-degree resolution (c. 1km at the equator) for import to GeoNode and Thinkhazard!.

<div class="c-box-image"><img src="images/posts/hazardmethods/fig23.png" alt="Tsunami maximum inundation height data at offshore points (output of Davies et al., 2017), for Sulawesi, Indonesia"/>
</div>
<div class="c-box-image"><img src="images/posts/hazardmethods/fig24.png" alt="Tsunami maximum inundation height data at the coast, interpolated from the points offshore Sulawesi, Indonesia"/>
</div>

An alternative pre-processing approach can be used to better define potential areas of onshore inundation, which identify low-lying areas where tsunami may inundate far inland. This can lead to non-coastal ADM2 units being assigned a hazard level, which would otherwise not be identified in the global data. This approach relies on SRTM elevation data, which are not available for the entire domain of global tsunami data, therefore use of this approach is limited to national or regional data. 
Due to the associated computational requirements and aggregated hazard levels presented by ThinkHazard!, it is not appropriate to conduct full inundation modelling to define onshore inundation height and extent. It is instead proposed to apply a simple ‘bathtub’ method which compares wave height from each point, to ground elevation within 10 km of the coastline.  This distance is expected to incorporate the maximum inundation of any tsunami. This processing procedure is as follows:
<ol style="a">
    <li>Extract the pixels covering the coast zone (to 10km inland) from SRTM30 tiles covering the tsunami data extent.
    <li>Produce a buffer polygon around each tsunami data point, to a distance sufficient to intersect the first 10 km inland from the coastline. Assign the point data value to the corresponding polygon.
    <li>Rasterize the polygon layer, aligned with SRTM raster cells, with maximum value of the buffered polygons assigned to the raster value. 
    <li>Perform a raster calculation; Inundation depth is calculated as tsunami height minus SRTM elevation. Where inundation depth is negative, it should be set to zero (the ground is not inundated).
    <li>This process is repeated for each return period layer to produce one ‘bathtub’ inundation map per return period for import to ThinkHazard!</ol>
        
An alternative approach to this, is to use an attenuation-based approach, which applies a degree of attenuation to the tsunami data points, to better represent the potential height inland. The attenuation relationship used is derived from post-tsunami surveys of inundation height decreasing with distance inland (Leonard et al. 2008). Another alternative is to use tsunami run-up equations to estimate tsunami run-up inland. Both approaches would be best suited to local data, and retain a significant amount of uncertainty in the onshore heights produced. These approaches and their impact on hazard level may be explored in future.
Next table example of pre-processed rasters for tsunami in Indonesia. Red zones show regions were wave height exceeds both elevation and the threshold on the buffered coastline
<table><tr><td>RP100 years, Red: h>2m</td><td>RP500 years, Red: h>0.5m</td><td>RP2500 years, Red: h>0.5m</td></tr>
<tr><td><img src="images/posts/hazardmethods/t100.png"></td><td><img src="images/posts/hazardmethods/t500.png"></td><td><img src="images/posts/hazardmethods/t2500.png"></td></tr></table>
		
### Intensity
Tsunami hazard is the potential for damage by massive volumes of water flowing onshore, with high velocity and depth, as tsunami waves. Damage occurs due to the force of waves, debris contained in the waves, floatation and scour of structures, and deposition of sediment/rocks. Tsunami waves are generated primarily by submarine earthquakes displacing the water column above, but also landslides or volcanic eruptions, which can displace large volumes of water if they occur underwater or at the coast. Small tsunamis can have very localized effects. The largest tsunamis, generated along subduction zones, can travel across the whole ocean affecting coastlines of multiple countries and inundating long distances and up to several kilometers inland, depending on topography.
Tsunami hazard data is commonly probabilistic and provides a view of hazard (generally wave height, rather than velocity) for multiple return periods. Data may be available as onshore inundation maps (typical of local analyses, e.g., for a city or province) or, more commonly for large areas such as national or global analysis, point data at locations offshore. Due to the computational overheads of simulating the nearshore and onshore flow of tsunami, data points are often spaced several kilometers (or tens of km) apart and are located offshore, e.g., at the 100m isobath (water depth). On the other hand, availability of inundation maps is likely to be limited, since models have very high technical and computational requirements.

### Frequency
Tsunami hazard data do not have de facto standard frequencies. However, given tsunamis’ primarily tectonic causes, the timescales used are commonly in the range of 100 to 2500-year return periods are used. Analysis commissioned for ThinkHazard! has enabled global tsunami data at 10, 50, 100, 200, 500, 1000, and 2500-year return periods to be openly available. Return periods of 100, 500, and 2500-year are used to define high, medium and low hazard, respectively.

### Results of classification
The classification of global data results in the following distribution of hazard levels:

<div class="c-box-image"><img src="images/posts/hazardmethods/fig25.png" alt="Global tsunami hazard levels at ADM1"/>
</div>
<div class="c-box-image"><img src="images/posts/hazardmethods/fig26.png" alt="Global tsunami hazard levels at ADM2"/>
</div>
<br>

## Volcanic Hazard Levels
<div class="c-box"><span class="box-title"><b>Classification Summary:</b></span>
  <p>Hazard levels are defined outside of ThinkHazard!, using a combination of historical eruption records: maximum recorded eruption size (Volcanic explosivity index) and last known eruption date).</p>
</div>

A volcano is a place where magma comes to the surface, during volcanic activity. Volcanoes present potential threats to people and property, due to:
<ul><li>Proximal hazards, affecting the area within 100 km around a volcano 
	<ul><li>Lava flows are very hot materials that can destroy the built environment and can release harmful gases.
	<li>Pyroclastic flows are a mixture of extremely hot rocks, sediment and gases that moves downhill, destroying most things it encounters and depositing large quantities of debris.
	<li>Lahars are flows of water, rock and sediment that destroy most things they contact, and deposit large quantities of debris. They can occur without an eruption during wet weather when rainfall mobilizes loose volcanic material.</ul>
	<li>Distal hazards, affecting larger distances 
	<ul><li>Ash (or tephra) consists of small fragments projected in the air during eruption, which drop over large area. They cause health problems, disrupt services and agriculture, and the weight of ash (especially when wet) can cause roofs to collapse.
    <li>Gases released into the atmosphere.</ul>

Eruptions can be relatively rare events, and volcanoes can remain quiet for several hundreds of years between eruptions. For most volcanoes globally, there is little information to assess how frequently eruptions might occur, and how big they might be in an eruption. For some well-studied volcanoes this information is available through assessment of previous deposits. Ashfall modelling is gradually providing more data that shows potential depth of ash at multiple return periods, though a lack of eruption data introduces significant uncertainties to the outputs. 
Volcanic hazard levels are defined outside of ThinkHazard!, using a combination of historical eruption records: maximum recorded eruption size (Volcanic explosivity index) and last known eruption date).  Several global eruption databases record the coordinate location, dates, type and magnitude of past eruptions.  The Smithsonian Global Volcanic Program (GVP)  and LaMEVE  databases contain a volcanic eruption index (VEI)  which quantifies the eruptive magnitude of past events. These are the best global information from which we can classify volcanic hazard, however, they contain significant uncertainty. Volcanoes with no recorded eruption, or that has never erupted in living memory may pose a hazard. The most widely used measure of volcanic intensity is VEI. Volcanoes can display variable VEI in different eruptions, and VEI varies over time during the same eruption. The maximum eruption VEI per eruption are provided in the GVP and LaMEVE eruption databases. The maximum VEI at each volcano forms the basis of the intensity thresholds used in preprocessing. Not all volcanoes in these databases have an associated VEI value. Where this is the case, date of last eruption is used (section 7.2.3.1). Where VEI is available, VEI 3 is used as a threshold to define a non-explosive volcano (those with a VEI < 3), are rated as ‘Low’ hazard. Volcanoes with maximum VEI > 5 are rated High, and those with a maximum recorded VEI 3-5 are ‘Medium’. 
The above is done in combination with consideration of the eruptive history (dates of previous eruptions). The most available, but basic, measure of eruption frequency is date of last eruption. Many volcanoes do not have a complete history of all eruptions because the average time between eruptions is can be several hundred or thousand years (these tend to be the volcanoes with more powerful eruptions) so it is difficult to reliably and consistently compare frequency across all volcanoes in the GVP database. Conversely, some volcanoes erupt with surprising regularity – monthly or even daily – with much smaller eruption and little impact. Last eruption date is only a very approximate guide to frequency of eruption, and further work should be done in future to better define volcanic hazard level for ThinkHazard!. 
Considering the above, last known eruption data is used as a guide to eruption potential only if there is no VEI data for a volcano. If the last known eruption was over 10000 years ago, it is considered Low hazard; if the last eruption occurred within the last 2000 years ago, it assigned High hazard. Anything with a last know eruption in the intervening period is Medium.
The procedure is applied as follows:
<ul><li>For each volcano of the GVM database, location, date of last known eruption and the maximum VEI index is extracted from the database
<li>Hazard level is associated to the VEI index value (when available):
    <ul><li>If VEI≥5, then hazard level is high
	    <li>If 5>VEI≥3, then hazard level is medium
        <li>If VEI<3, then hazard level is low</ul>
<li>If the VEI index value is not available, hazard level is associated according to the date of last known eruption:
    <ul><li>If it was recorded an eruption in the last 2000 years (CE), then hazard level is high,
    <li>If it was recorded an eruption in the Holocene (last 10000 years), then hazard level is medium
    <li>If it was recorded an eruption in more ancient times, then hazard level is low
    <li>If no eruption of the volcano has been reported, then hazard level is very low</ul>
</ul>
        
To account for the fact that damage from a volcano does not occur only at the vent, but several tens of kilometers around the vent, the hazard level of each volcano is applied to a circular area around the volcano coordinate location.
The maximum extent of proximal hazards is approximately 100 kilometers from a volcanic vent. This distance does not account for topographic influences that constrain the flow of lahars and lava. The resulting raster map of hazard levels provides a crude assessment of proximal volcanic hazard (excluding impacts of ash and gas), see Figure 27. This map is uploaded to the ThinkHazard! database. The tool then associates the hazard level to administrative units following the normal procedure: intersection with administrative polygons and maximum of hazard level on a given unit.

### Results of classification
<div class="c-box-image"><img src="images/posts/hazardmethods/fig27.png" alt=" Hazard class at all locations within 100 km of a volcano. Red = high hazard, orange = medium, yellow = low. Very low and unknown hazard are not shown"/>
</div>

### Future probabilistic classification
When available, probabilistically simulated ashfall data can be imported as maps of ash depth at multiple return periods, enabling hazard levels to be defined as described in section 2.4. However, such analysis are available for only a few regions, and are not typically represented at the multiple return periods required for ThinkHazard!. Work may have to be commissioned to achieve good coverage of volcanic ash hazard levels in ThinkHazard!.
Probabilistic volcanic data are available as raster containing ash depth (mm) at each grid cell, or as maps of isopachs indicating the limits of ash depth distribution, for several return periods. Recommended ash depth thresholds for hazard levels are: 0.5 mm, 10 mm, and 50 mm. These values are selected based on differential impact. Ash thicknesses of 0.5 mm can impact transportation by reducing visibility and obscuring road markings. At 10 mm, minor damage to buildings and infrastructure may occur through ash infiltration requiring extensive clean-up and this thickness of ash may cause agricultural productivity loss (<50%) and health implications. At 50 mm, major agricultural productivity loss (>50%) and damage to buildings and infrastructure (i.e., potential roof collapse), ash infiltration to buildings and health implications would be expected (GVM, 2016). 
There is no industry standard frequency for presenting ash fall modeling. Frequency of eruption varies significantly for different volcanoes, but generally ash impacts are relevant presented at return periods greater than 100 years. A decision on recommended return period for probabilistic ash data would have to be taken on receipt of global ash modeling data, but it is expected that suitable return periods would include 100, 500, 1000, and 10000 years.

### Landslide Hazard Levels
<div class="c-box"><span class="box-title"><b>Classification Summary:</b></span>
  <p>Landslide susceptibility or hazard index is reclassified into four hazard levels. Presently, this is done differently for each hazard data source (see below). Investigations are underway to make this more consistent across multiple hazard sources.</p>
</div>

Large-scale landslide hazard maps generally present landslide frequency per grid cell, derived from GIS-based analysis of terrain conditions to produce a landslide susceptibility map, and the coincidence of landslide triggers. Landslide is a locally variable hazard, but the factors determining landslide susceptibility are well defined (e.g., Nadim et al., 2006). Terrain factors include slope, land or vegetation cover, soil type and geological conditions, and soil moisture. This is often presented as a ‘susceptibility index’, or when combined with triggering factors, (precipitation and seismic activity) this may be presented as a ‘hazard index’. In either case, hazard is generally classified into discrete categories describing the frequency which landslide may occur there. This is consistent with availability of regional and national landslide data too. Probabilistic landslide data are rare, and only available on a local basis, sometimes including analysis of landslide runout to establish potential impact. It is envisaged that ThinkHazard! Will rely on using national, regional, or global landslide hazard maps, which present frequency of landslides, rather than such high-resolution local datasets.
Two of the most prominent global landslide datasets are NASA SEDAC, which hosts the Global Landslide Hazard Distribution, v1 (CHRR, CIESIN and NGI, 2005), which presents landslide and avalanche hazard using an index of 6-10 (below 5 is considered negligible hazard). International Centre for Geohazards/NGI later produced a global landslide frequency map for the UNISDR GAR2013  (NGI, 2013), based on a similar method using global terrain and trigger data. This dataset presents expected annual probability per grid cell, and percentage of the grid cell of a potentially destructive landslide event. 
The available landslide hazard maps can be categorized into hazard level based on the frequency of occurrence, e.g., as used in the GAR13 data (table below), or based on the mapped hazard index, as supplied in SEDAC data. Given the variation in original data units and categories, it is necessary to apply a different processing method to each, while preserving a consistent conversion of landslide frequency into ThinkHazard! hazard levels. The categorization procedure applied to each of the available global datasets is described below:
NGI GAR13 data are supplied as two raster datasets, each indicating the annual frequency of landslide due to seismic trigger and Rainfall (precipitation) trigger. The two rasters were combined for the purposes of ThinkHazard!, with the maximum annual frequency per grid cell assigned to the resulting combined trigger raster. The resulting raster was classified into four hazard levels defined by NGI (2013).

Annual frequency and corresponding raster score for landslide, based on NGI (2013)
<table><tr><td>Hazard class</td><td>Annual frequency per km2 (1x10-4)</td><td>Annual frequency per km2</td><td>Raster score (Ann. Freq. * 1,000,000)</td></tr>
<tr><td>Negligible</td><td><1.8</td><td><0.00018</td><td><180</td></tr>
<tr><td>Low</td><td>1.8-3.2</td><td>0.00018-0.00032</td><td>180-320</td></tr>
<tr><td>Medium</td><td>3.2-7.5</td><td>0.00032-0.00075</td><td>320-750</td></tr>
<tr><td>High</td><td>>7.5</td><td>>0.00075</td><td>>750</td></tr></table>

SEDAC data is available as a single raster dataset, giving landslide hazard as a decile value of relative global landslide hazard per grid cell. The range 5-9, was adjusted to 6-10 for consistency with other datasets. The original data layer is reclassified in GIS, to produce a raster containing hazard level, as follows (partly based on the classification description given in Dilley et al. (2005): 6 = negligible (translated to very low for ThinkHazard!); 7 = Low; 8 = Medium; 9-10 = High.
After assigning a consistent integer value (1-4) to the processed hazard levels, the layers are imported to ThinkHazard!, where hazard level is mapped onto ADM2 units.

### Future classification
Implementation of new dataset produced by NASA in 2017 (Stanley and Kirschbaum, 2017) is under investigation. This is a global landslide susceptibility map was created by combining information from four principal sources of information for five explanatory variables: slope, distance to fault, geological classification, presence of roads, and forest loss. Susceptibility is classified into five categories: very low, low, moderate, high, and very high. The classes are defined were divided at susceptibility values of 0.11, 0.49, 0.671, and 0.75. Each category was twice as large as the next highest, e.g., the high category contains approximately twice the number of pixels as the very high category (3% of the global area). It has been currently proposed to combine the very high and high categories into ‘high’, and transfer the remaining categories as originally defined. 
Investigation is required into how this relates to landslide frequency, and in consistency with the already implemented layers. Additionally, initial testing shows a tendency towards all ADM0 units showing high hazard, which poses a problem for communicating the truly high hazard areas. Investigation will also consider whether an area threshold (similar to that applied to river and urban flood) could be used to avoid this.


