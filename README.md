# CrossSegmentationExplorer

Cross Segmentation Explorer is a 3D Slicer extension for the visual inspection and comparison of multiple segmentations on the same volume. The extension is designed for CT volumes and segmentations in DICOM SEG format. This extension has been tested exclusively on CT volumes.

---

# Getting Started 
## 1. Prepare Your Environment: How to Set Up 3DSlicer
1. Download the latest stable build of 3D Slicer from https://download.slicer.org and install it.
2. Open the Extension Manager by clicking “Install Extensions” on the left side of the welcome screen, or by clicking the blue button with the “E” and puzzle-piece icon in the toolbar.
<img width="1661" height="710" alt="SlicerWelcomeLayout" src="https://github.com/user-attachments/assets/a78082ad-52fc-4b2c-8d77-2927335a40e3" />

3. Install the “QuantitativeReporting” extension. This will automatically install the DCMQI dependency as well. Restart 3D Slicer after the installation.
4. Clone this Git repository https://github.com/ImagingDataCommons/CrossSegmentationExplorer.git to your local machine.
5. After restarting Slicer, click the “Customize Slicer” icon (see Screenshot above).
6. Open the “Modules” tab, and on the right side under “Additional module paths,” click the arrow button with the two arrowheads and select “Add.”
7. Navigate to the cloned CrossSegmentationExplorer repository and select the subfolder "CrossSegmentationExplorer" that contains the CrossSegmentationExplorer module, then click “Open.”
8. Restart 3D Slicer again.
9. After the restart, the CrossSegmentationExplorer extension should appear in the module drop-down menu under “Segmentation.”
<img width="1798" height="1039" alt="ModuleDropDown" src="https://github.com/user-attachments/assets/44964b42-678b-41a2-9641-10215bd65dbc" />


## 2. Access Your Data: How and Where to Download Imaging Datasets
⚠️ **Supported Data Formats:** This module currently works only with DICOM volumes and DICOM SEG segmentation files. Other file formats are not supported at the moment.
### Using our published Zenodo Dataset (Recommended)
Download the dataset released with the paper “In search of truth: Evaluating concordance of AI-based anatomy segmentation models” from Zenodo (DOI: 10.5281/zenodo.17860591).
This dataset includes 18 CT volumes from the NLST Dataset and corresponding segmentations suitable for immediate use with the module.
### Downloading Data from the Imaging Data Commons (IDC)
- Through the IDC web portal: https://portal.imaging.datacommons.cancer.gov
- Via the SlicerIDCBrowser extension by pasting a Study Instance UID into the study field (see [forum topic](https://discourse.slicer.org/t/sliceridcbrowser-extension-released/32279/2))
- Programmatically using:
  ```bash
  pip install --upgrade idc-index
  idc download-from-selection --study-instance-uid <UID> --download-dir .
  
### Using Your Own Data
You can also use your own imaging studies with this module. If no segmentation is available, you can generate one directly inside Slicer using AI-based segmentation extensions such as **SlicerMOOSE**, **MONAIAuto3DSeg**, or **TotalSegmentator**. These extensions produce DICOM SEG files that are compatible with this module.

## 3. Importing Your DICOM Data: How to Load Studies into 3D Slicer
1. On the 3D Slicer Welcome screen, click “Add DICOM Data” to open the DICOM module.
<img width="1618" height="710" alt="SlicerWelcomeScreenAddDicom" src="https://github.com/user-attachments/assets/bd50efe9-49e2-4e7a-ae86-3f5072e2b3b4" />

2. In the DICOM module, click “Import DICOM Files”.
<img width="1618" height="710" alt="DICOMDatabase" src="https://github.com/user-attachments/assets/b0d80092-a50d-4c01-a604-09469dedc528" />

3. Select the top-level folder that contains all DICOM files for your dataset (Slicer will automatically detect and organize all subfolders). Wait for Slicer to import the data. Depending on the number and size of the files, this may take some time.
4. After the import is complete, use the DICOM browser to load all data for a patient, only a specific study,or individual series/files. Once the intended data is selected, click “Load” to bring it into the Slicer workspace.

---

# CrossSegmentationExplorer Module

https://github.com/user-attachments/assets/7f8a19b6-a4cc-49d2-b099-acd6008a5ced


## Segmentation Visualization
1. Select the volume you want to review. After selecting the volume, the module lists the number of associated segmentations and provides the option to load them. Segmentations that are already loaded are detected and not reloaded.

⚠️ **Known Performance Problems:** Selecting a volume takes very long at the moment. This delay is caused by the computation of the number of associated DICOM SEG segmentations, which is currently slow. We are aware of this issue. If needed, you can temporarily disable this by commenting out the lines 727 and 728 in the module source code:

```python
# referencedSegmentations = self.getAssociatedSegmentationFileNumber()
# self.ui.lableSegdicomRef.setText(str(referencedSegmentations) + " DICOM SEG series referencing this volume found")
```

2. Select one or more segmentation files OR segmentation models to automatically display three orthogonal 2D views (axial, sagittal, and coronal) for each selected item
   - The first dropdown menu displays all loaded segmentations associated with the selected volume and allows you to select the segmentation file
   - The second dropdown menu is to select segmentation models. Segmentation models group one or more segmentations into a single model representation. This is useful when AI-based segmentation methods produce multiple output files.Segmentations are automatically assigned to models based on keywords found in their series description.
   - Models and associated keywords can be created, modified, or deleted by clicking the plus icon next to the segmentation dropdown. This opens a configuration table, where models
     can be edited or added. Keywords used for matching should be entered as comma-separated values.
     <img width="1700" height="686" alt="SegmentationModelPopUpTable" src="https://github.com/user-attachments/assets/6f5e133c-edc2-4b2e-be66-d9902ead92bd" />
     
3. *OPTIONAL:* **Modify the Layout**:
   - By default, three orthogonal 2D views (axial, sagittal, coronal) will be created for each selected segmentation or segmentation model, displaying the CT volume overlaid with the corresponding segmentation
   - In the “Enable 2D & 3D Views” section, you can also enable 3D views. When selected, one 3D view is created for each segmentation file or model, with the corresponding segmentations rendered in that view
   - Each view type (2D or 3D) can be toggled on or off independently. ⚠️ At least one view must be enabled to visualize the data.
   - Additionally, selecting the "Vertical/horizontal Layout" checkbox arranges the 2D views in a vertical layout instead of the default horizontal layout.
     
     *Vertical Layout*
     <img width="1104" height="596" alt="VerticalLayout" src="https://github.com/user-attachments/assets/570417b8-4e15-4ae1-8be8-336a120f2ecb" />

     *Horizontal Layout*
     <img width="1103" height="596" alt="HorizontalLayout" src="https://github.com/user-attachments/assets/ad3b9c8c-8880-4cbe-98d3-1364aad86845" />


Below the main controls, two collapsible sections — **Options** and **Segment-wise comparison across models** — provide additional functionality to support review and analysis workflows:

#### Options
Options allows you to adjust how the segmentations in the 2D views are displayed and how views behave:
- *Link Views:* Synchronize camera movements across all active 3D or 2D views.
- *Change Segmentation Representation to Outline:* Switches the segmentation display from filled regions to outlines.

## Segment-wise comparison across models
The Segment-wise comparison across models panel enables detailed,  review across the individual segments available in the loaded segmentations.

**Key Features:**
- *Select Segmentation Group:* Choose an anatomical group (e.g., "Ribs") or select "All" to include all available segments. The table will display only the segments that
  belong to the selected group, along with the number of segmentations in which each segment is present.
  Segmentation groups can be adjusted/changed similarly to segmentation models:
  - Click the "+" button to open a configuration pop-up.
  - Each group is defined by a set of keywords. Segments whose names contain one of the keywords will be assigned to that group.
  - The group "All" is always available and contains all segments, while "Other" includes all segments that do not match any defined keyword group.
- *Segment Navigation:* Use the Previous and Next buttons to step through the segments one by one. Each selected segment is displayed simultaneously in all views, allowing for side
  by-side comparison across segmentations or models.
- *Show Neighboring Segments:* When the "Show neighboring segments semi-transparent" option is enabled, spatially adjacent structures are shown in semi-transparent mode.

*Example of the "Ribs" segmentation group: all segments with names containing keywords like "rib" are automatically grouped and displayed in the views when selected.*
<img width="1816" height="861" alt="RibsGroup" src="https://github.com/user-attachments/assets/60150f16-afd7-406e-a7d9-c013932cb310" />


*Structure-wise comparison of a single rib segment with neighboring segments shown semi-transparent. Neighboring structures are computed separately for each segmentation or model, based on the available segmentations. As each segmentation may contain a different set of anatomical structures, neighboring segments can vary — for example, one model might display adjacent ribs, while another includes nearby organs such as the lungs.*  
 <img width="1816" height="861" alt="NeighboringSemiTransparent" src="https://github.com/user-attachments/assets/8d9ffb0e-b92f-4275-a18e-db86b23fa0e6" />

