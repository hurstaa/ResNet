# Continental United States Storage Reservoir Network (ResNet)
This repository contains the Jupyter Notebooks and input files necessary to recreate the ResNet database of routed US dams. The user needs to download the most recent versions of all of the databases, as well as the input files and most recent version of ResNet from this repository or Zenodo (DOI: 10.5281/zenodo.14057031). First run 01ResNet_FilteringandSnapping followed by 02ResNet_DamOrdering. SOMETHING ABOUT STEP 3!!! The output will be a csv with an updated version of ResNet. If you would like any updated dam locations permanently added to future versions of the dataset, please email resnet@usbr.gov.

For more background information on why certain choices were made in our filtering and snapping algorithms, please refer to our journal article.
Journal article: 

## Background
ResNet is a national database of dams impounding storage reservoirs in the continental United States routed from upstream to downstream to create a linked network on the National Hydrography Dataset (NHD). This network enables basin-wide analyses of sediment trapping and disruptions to sediment and water transport. Further, reservoirs are associated with major downstream river mouths and deltas, improving the ability to quantify impacts to specific rivers and deltas. ResNet was created by combining an automated workflow with iterative, manual quality control to ensure that dams with water storage snapped to a flowline representative of their drainage area, rather than a flow diversion. The final product allows users to create watershed-scale reservoir networks, track sediment trapping and water storage potential, and track the reduction in sediment-contributing drainage area through time within small watersheds or for entire regions. A linked network of reservoirs also allows for better water management, flood analysis, and water and hydropower supply studies. From manual quality-checks, we created a dam attributes input file for the automated dam routing code. The dam attributes file may be utilized by future users to further revise dam and reservoir placement for specific studies as needed. Thus, ResNet will function as a living dataset. 

Global and national dam datasets over CONUS typically only focus on large storage reservoirs, often linked to global flowline datasets. This precludes the ability to use these datasets to quantify the effects of small, headwater reservoirs on sediment trapping and flow disruption. This is largely due to the fact that global flowline datasets are at too coarse of a resolution to route flow at small dams. We therefore link all dams reported in the National Inventory of Dams (NID; https://nid.sec.usace.army.mil/#/downloads) to National Hydrography Dataset Version 2 (NHDPlusV2) flowline data to route flow through United States dams. NHDPlus High Resolution contained many quality control issues that prevented accurate flow routing, so we chose to use the older and coarser version 2. ResNet only includes dams that are located on NHD flowlines and report storage values.

As future releases of any of the input datasets become available, the code can be re-run to automatically update ResNet with more recent data. We anticipate updating the code for future versions of ResNet to incorporate higher resolution flow datasets (i.e. 3DHP) as they become available.

## Input Datasets:
1. National Inventory of Dams (NID): The NID database was created in the 1970s to meet requirements detailed in the National Dam Inspection Act, PL 9236722. Since 1975, the database has grown from approximately 45,000 to over 92,000 dams and continues to grow, incorporating dams meeting the criteria of (1) high hazard potential to human life, (2) significant hazard potential to facilities or infrastructure, and (3) size requirements, typically including dams and reservoirs in excess of 7.5 m in height and 18,500 m3 of water storage capacity. We have noticed that in some instances, NID changes the ID of dams through time or reuses NID IDs for dams that have been removed. Future versions of ResNet will aim to address this so that each dam has references to past NID IDs as well. This will facilitate comparing to datasets developed prior to 2024 and future datasets developed from NID.
2. Removed Dams Database (cite): incorporates dams that have been removed and may have been in prior versions of NID.
3. GeoDAR (cite): cross-referenced with NID by this study to update NID dam locations where available, as GeoDAR is spatially validated.
4. Global Reservoir and Dam (GRanD; cite): locations manually verified by this study and cross-referenced with NID. Ascertains that large CONUS dams are placed on the correct flowline.
5. Dam attribute file: allows users to update a dam's location if incorrect in other datasets or update storage and other attribute data. Within this file, we incorporate all of the U.S. Bureau of Reclamation (Reclamation) and U.S. Army Corps of Engineer (USACE) dams into ResNet because these dams are of interest to ongoing agency studies. We additionally incorporate 143 major river mouths and 36 coastal deltas16 to allow users to track reservoir storage and dam emplacement above river mouths and deltas. This file also allows users to incorporate additional information on dam storage or completion year. The file includes an attribute called ‘IsSite’ that allows the user to flag sites of interest for tracking upstream dam emplacement changes to the watershed. Within this file, we incorporated 4 iCOLD dams with storage capacity and 293 iCOLD dams with completion year data where there were gaps in the other datasets.
6. NHDPlusV2 (cite): Flowline network for the entire US containing individual flowlines with unique attributes that route flow. We primarily use the COMID, which is the unique identifier assigned to the flowline, the Hydrosequence, which is a separate unique identifier related to the flowpath, and the Downstream Hydrosequence, which indicates the downstream flowpath. We assigned a 'CountryOut' field that indicates which border the stream outlets at. See publication for more details on NHDPlusV2 vs NHDPlusHR.

### Adding a dam to the dam attribute file:
If a user has better information on a dam's location, storage data, or completion year data, they can add it to the dam attributes file (resnet_attributes.csv). This allows moving incorrectly placed dams onto the correct NHD flowline (new location must be on an NHD flowline that the user has confirmed has the correct representative drainage area and must be projected in North American Datum 1983 coordinate system). Better storage data information in xx units will overwrite the value in the current version of ResNet. The same is true for completion year. If your dam is already in the dam attribute file, do not duplicate it. Instead, update the entry for that dam. 

To permanently add a dam to ResNet or update its attributes, email ResNet@usbr.gov with the dam's NID and ShortID (if assigned in most recent version) and the coordinates, storage information with units, and/or completion year data. It is important to note that ResNet is a dataset of storage reservoirs, so if an entry does not have a storage value or is not on an NHDPlusV2 flowline, then the dam will be filtered out by the filtering algorithm and not included in the final dataset.


## How to run the code:
1. Download ArcGIS Pro. You will need an ArcGIS Pro installation on your computer to run this code.
2. Download a local version of this GitHub repository and all files. To work with code as written, you need to have the input files in same folder as script with the same sub-folders. If you download from GitHub, you will automatically download all of the needed input files EXCEPT for the flowlines. You will need to download those from Zenodo (link; NHDFlowline_Network_NHDPlus_Countries.zip) and unzip within the Inputs folder. This zip file should have a geodatabase and a .csv in it. You can download the versions of datasets here on github or else from Zenodo (link). If you want more updated versions than those used to create version 1 of ResNet, you will need to download directly from the source listed above.
3. Find the environment.yml file in the main download folder with the environment that already has packages needed to run this code (https://www.anaconda.com/docs/tools/working-with-conda/environments#example-version-matching-inputs).
4. Create a new environment with the .yml file. 'environment.yml' is the path to the .yml file:
   ![image](https://github.com/user-attachments/assets/8a96b734-5238-416d-91ec-b0a8341b6110)

5. Map the .yml environment to where you run jupyter notebooks using this script in Anaconda Prompt. your_env_name is the name you gave your environment in step 3:    
   ![image](https://github.com/user-attachments/assets/c1723e8c-d8ce-4370-ae99-d567490794b8)
6. This assumes you have jupyter notebooks installed. Run jupyter notebook through the prompt and change the kernel to the new environment once you open the script. You should add the folder download for ResNet to the file path.
7. Run 01ResNet_FilteringandSnapping. This automates the data filtering, dataset combining, and flowline snapping algorithms using pandas and ArcGIS Pro.
8. Run 02ResNet_DamOrdering. Output file is final updated ResNet routed. Appears in the Outputs folder as ResNet_{today's date}.csv.
9. Run 03 !!!!!!!!!!!!!!!!!!!!!!!!!!

## How to use the 'IsSite' feature:
Adding a dam to the dam attributes file and marking 'IsSite' = 1 will flag that dam as a site in the dam ordering code. This then tags every dam upstream of that site with a SiteTag of that dam's ShortID (numerical identifier). This is useful to understand how many dams are upstream of a site and how those dams impact the drainage area and flow connectivity for the dam. 
