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
