# Architecture and technical workflow
## Open source architecture

ThinkHazard! uses open-source code, available at https://github.com/GFDRR/thinkhazard. The code can be replicated and amended to develop versions specific to an organization or sector. Potential amendments include including different hazards, or showing a subset of the present hazards. Recommendations may be tailored to a specific use (e.g., with a focus on managing risks in the agricultural sector). Additionally, the underlying method may be adjusted, for example by changing the classification of hazard levels; if the intended focus of the tool related to minimum building standards, it may be appropriate to revise the intensity threshold at which damage can be expected to occur. It is also possible to link the user interface to a different set of layers and resources on a different GeoNode.

Database structure
ThinkHazard! uses two dedicated databases, populated with data harvested from a GeoNode. The processing database is used for data administration/preview, and the public database is used for visualization of information in the user interface.

Tasks performed using the processing database include: 1) harvesting and processing of hazard data from GeoNode; 2) modification of recommendations (content, order, hazard level link) via the administrator interface. A preview interface is available, for administrators to verify any updates to information (i.e., correct data and recommendations) before publication to the public database.

The public database is a copy of the processing database at a given time. To maintain performance of the user interface, data shown in the user interface are retrieved from the pre-calculated hazard levels stored in this database, rather than using on-the-fly data retrieval
and processing. The public database is dropped and replaced by a new version each time the administrator decides to publish the data. At the same time, an archive of the database is stored in case of any future requests of data before the latest version. This archive is accessible to administrators only. The current database version number is presented on the About page. An update to the public database is required when:
1. Changes have been made to recommendations, contact information, or climate change statements
2. New data is available on the GeoNode, or changes have been made to existing data layers (including change of data content, or metadata).
Updates can only be made by administrators, using prescribed commands.

<div class="c-box-image">
  <img src="images/posts/workflow/workflow.png" alt="General architecture of the tool and back office workflow"/>
</div>  
 
 
##	Technical workflow – hazard classification
Hazard levels are not classified ‘on-the-fly’ (i.e., as a user requests them) because the processing time required would slow down the user search. Instead, classified hazard level is stored for each hazard against each ADM2, ADM1, and ADM0 Unit in the database. The user interface pulls data from that database upon a user requesting data in the user interface. This enables very fast operation of the user interface, but does require administrators to update the tool database when new data are available.
The technical workflow (contained in the ThinkHazard! processing code) identifies all hazard layers on GeoNode that are identified in metadata as being for use in ThinkHazard!. These layers are downloaded to the processing database, before being assessed for ‘completeness’. Completeness includes: 1) a valid hazard set must contain a data layer for each return period frequency threshold that is used in the classification; 2) data layers in a hazard set must all have matching spatial extent, origin, and resolution. The following hazard classification is then conducted:

<ol type="I">
    <li>All complete and previously unprocessed hazard sets are identified. These are datasets that have changed since the last execution of this process. Datasets that have already been processed are already in the production database, and are not reanalyzed.
    <li>For each hazard set:
    <ol type="a"><li>All ADM2 units that intersect the data set bounding box are selected.
        <li>The hazard classification is conducted one ADM2 unit at a time. Calculations are made on individual ADM2 units to avoid memory problems.
        <li>For each selected ADM2 unit:
        <ol type="1"><li>An extent corresponding to the current ADM2 (vector polygon) is read from the raster hazard dataset matching the return period used for the currently analyzed hazard level. 
            <li>If there are hazard intensity values in the selected extent, the ADM2 unit vector is converted to a raster with resolution to match the hazard raster. If there are no values, a value of ‘No Data’ is stored in the processing database for this ADM2 unit.
            <li>This raster includes all pixels that intersect fully or partially, the ADM2 unit polygon (so that hazard pixels along the ADM2 unit boundary are accounted for). This raster is applied as a mask on the hazard dataset raster.
            <li>If the data set is a pre-processed layer:
            <ul><li>The maximum hazard intensity value in the masked area of the data set is selected.
                <li>This value is compared against the hazard intensity thresholds.
                <li>The corresponding hazard level is stored for the ADM2 unit, in the processing database.</ul>
            <li>If the data set is not pre-processed (i.e. is probabilistic), the following process is performed with the thresholds corresponding to each hazard level (in the order of High, Medium, and Low):
            <ul><li>The maximum hazard intensity value in the masked area of the data set is selected.
                <li>This value is compared against the hazard intensity threshold for the High hazard level, on the return period data layer corresponding to the High Hazard frequency threshold.
                <li>If the intensity threshold is exceeded, High hazard level is stored for the ADM2 unit, in the processing database. 
                <li>If the High hazard threshold is not exceeded, the process is performed on the Medium hazard threshold and data. If Medium hazard threshold is exceeded, Medium hazard level is stored for the ADM2 unit.
                <li>If the Medium hazard threshold is not exceeded, the process is performed on the Low hazard threshold and data. If Low hazard threshold is exceeded, Low hazard level is stored for the ADM2 unit.
                <li>If none of the three hazard levels are exceeded and there are intensity values, the value ‘Very Low’ is stored.</ol>
            <li> A decision is made on which dataset to present in ThinkHazard! (i.e. which values to store in the public database), if there has been more than one dataset available to classify hazard levels. 
                <ol type="a"><li>Outputs of the above process are prioritized according to:
                    <ul><li>Data quality
                        <li>Geographic status (local or global)
                        <li>Date of last update</ul>
                    <li>The dataset with highest priority is identified, and the hazard level for each hazard and ADM2 unit are passed through to the public database and take the first one for each ADM2 entity
                    <li>Aggregation of ADM2 hazard level to ADM1 and ADM0 is performed:
                    <ul><li>Aggregation to ADM1 is conducted by identifying the maximum hazard levels in all its ADM2 'child' units
                        <li>Aggregation to ADM0 is conducted by identifying the maximum hazard levels in all its ADM1 'child' units 
                        <li>For each ADM Unit (2, 1, 0) and hazard, hazard level is stored in the database</ul></ol></ol></ol>
