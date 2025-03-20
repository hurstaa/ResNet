# Continental United States Storage Reservoir Network (ResNet)
This repository contains the Jupyter Notebooks and input files necessary to recreate the DamNet database of routed US dams. The user needs to download the most recent versions of all of the databases, as well as the input files and most recent version of DamNet from Zenodo (DOI: 10.5281/zenodo.14057031). First run 01DamNet_FilteringandSnapping followed by 02DamNet_DamOrdering. The output will be a csv with an updated version of DamNet. If you would like any updated dam locations permanently added to future versions of the dataset, please email damnet@usbr.gov.

Background on why important

Description of input datasets:
Why NHDPlusv2? Future versions use something else if better becomes available.

Link to published paper:

Instructions:
1. Download yaml; map environment to jupyter notebooks
2. Download local version of github repo and all files. To work with code as written need to have input files in same folder as script. Can download versions here on github or else from Zenodo (link)
3. Run 01DamNet_FilteringandSnapping. Should output files to 02DamNet_DamOrdering folder
4. Once finished, run 02DamNet_DamOrdering. Output file is final updated DamNet

Potential user modifications:
If a user has better information on a dam's location, storage data, or completion year data, they can add it to the dam attributes file (xxx.csv). This allows moving incorrectly placed dams onto correct NHD flowline (new location must be on an NHD flowline that the user has confirmed has the correct representative drainage area and must be projected in NAD83 coordinate system). Better storage data information in xx units will overwrite the value in the current version of ResNet. Same for completion year.

If want information permanently added to future versions of ResNet or a new dam included, email ResNet@usbr.gov with the dam's NID and ShortID (if assigned in most recent version) and the coordinates, storage information with units, and/or completion year data. It is important to note that ResNet is a dataset of storage reservoirs, so if an entry does not have a storage value or is not on an NHDPlus v2 flowline, then the dam will be filtered out by the filtering algorithm and not included in the final dataset.
