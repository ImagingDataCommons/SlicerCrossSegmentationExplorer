# CrossSegmentationExplorer

Cross Segmentation Explorer is a 3D Slicer extension for the visual inspection and comparison of multiple segmentations on the same volume. The extension is designed for CT volumes and segmentations in DICOM SEG format.

## Prepare Your Environment: How to Set Up 3DSlicer
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


## How to use

1. Achieve a new AI segmentation (for example by using the [TotalSegmentator](https://github.com/lassoan/SlicerTotalSegmentator) or [MONAIAuto3DSeg](https://github.com/lassoan/SlicerMONAIAuto3DSeg) extension)
    - As an alternative you can download a sample dataset from [Imaging Data Commons](https://github.com/ImagingDataCommons/idc-index):
        - Programatically
            - `pip install --upgrade idc-index`
            - `idc download-from-selection --study-instance-uid 1.2.840.113654.2.55.119867199987299072242360817545965112631 --download-dir .`
        - You can also download it using `SlicerIDCBrowser` by pasting the UID into the study field (see [forum topic](https://discourse.slicer.org/t/sliceridcbrowser-extension-released/32279/2))
        - Or the [IDC portal on the web](https://portal.imaging.datacommons.cancer.gov/explore/)
    - Load the downloaded data as DICOM (you will need the DCMQI extension but you have it if you already installed the IDCBrowser)
2. Open the CrossSegmentationExplorer module

---

## CrossSegmentationExplorer Module

https://github.com/user-attachments/assets/7f8a19b6-a4cc-49d2-b099-acd6008a5ced



3. Select the volume you want to review — After selecting the volume, the module lists the number of associated segmentations and provides the option to load them. Segmentations that are already loaded are detected and not reloaded.
4. Select one or more segmentations (The dropdown menu displays all loaded segmentations associated with the selected volume) OR select one or more segmentation models to initialize individual 3D views for each selected item
   - Segmentation models group one or more segmentations into a single model representation. This is useful when AI-based segmentation methods produce multiple output files.
   - Segmentations are automatically assigned to models based on keywords found in their names.
   - Models and associated keywords can be created, modified, or deleted by clicking the plus icon next to the segmentation dropdown. This opens a configuration table, where models
     can be edited or added. Keywords used for matching should be entered as comma-separated values.
     ![ModelKeywordTable](https://github.com/user-attachments/assets/2cd2b0d4-b198-4de8-b701-b89f93063287)

     *Add, delete, or modify segmentation model names and associated keywords in the model configuration pop-up table*
     
5. OPTIONAL: Modify the Layout:
   - By default, 3D views are enabled when segmentations are loaded.
   - In the Instantiate Views section, you can also enable 2D views. If selected, three orthogonal 2D views (axial, sagittal, coronal) will be created for each selected segmentation
     or segmentation model, displaying the CT volume overlaid with the corresponding segmentation.
   - Each view type (2D or 3D) can be toggled on or off independently.
     ⚠️ At least one view must be enabled to visualize the data.
   - Additionally, activating the "Instantiate Vertical Layout" checkbox arranges the 2D views in a vertical layout instead of the default horizontal layout.
     
     *Vertical Layout*
     ![Vertical Layout](https://github.com/user-attachments/assets/8e605484-964b-4329-a7e1-f36ba84d63d5)
     *Horizontal Layout*
     ![Horizontal Layout](https://github.com/user-attachments/assets/eb2d5a5f-5ded-415b-8ae1-6ec926d0b5f1)


---

Below the main controls, two collapsible sections — **Options** and **Segment-wise comparison across models** — provide additional functionality to support review and analysis workflows:

#### Options
Options allows you to adjust how the segmentations in the 2D views are displayed and how views behave:
- *Link Views:* Synchronize camera movements across all active 3D or 2D views.
- *Change Segmentation Representation to Outline:* Switches the segmentation display from filled regions to outlines.

#### Segment-wise comparison across models
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
![Ribs](https://github.com/user-attachments/assets/ed991c4a-f05a-43e5-b474-ac36acab640c)

*Structure-wise comparison of a single rib segment with neighboring segments shown semi-transparent. Neighboring structures are computed separately for each segmentation or model, based on the available segmentations. As each segmentation may contain a different set of anatomical structures, neighboring segments can vary — for example, one model might display adjacent ribs, while another includes nearby organs such as the lungs.*  
![SemiTransparent](https://github.com/user-attachments/assets/b7ee7c8e-76e1-4d37-bceb-4a77fe51cbc9)

 
