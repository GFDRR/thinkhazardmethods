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
<li>low: 1000-year return period
    
 <br><br>
 <center><b>Table 3</b> Example of rationale justifying the choice of return periods, for river flood hazard</center>
    
<table><tr><td><b>Name</td><td><b>Return period</td><td><b>Rationale</td></tr>
<tr><td>High</td><td>10 years</td><td>In many cases a River Flood event of once per year or once every five years already causes considerable damage. NOTE: This return period may not be available in all flood hazard assessments. Therefore, it is proposed to allow ThinkHazard! to use 25 years as an alternative.</td></tr>
<tr><td>Medium</td><td>50 years</td><td>An event that would, on average, be expected to occur once or twice in a lifetime.</td></tr>
<tr><td>Low</td><td>10,000 years</td><td>An event most people will not experience and will only be remembered by previous generations. 
NOTE: Often the 10,000 year return period will not be available. It is proposed to use the highest available return period (and longer than 50 years) for the ‘Low’ hazard class. This can typically be between 100 and 1,000 years.</td></tr>
<tr><td>Very low</td><td>Intensity not exceeded at the ‘low’ return period used.</td><td>No floods expected based on current climate, current models and data. However, some uncertainty remains.</td></tr></table>




