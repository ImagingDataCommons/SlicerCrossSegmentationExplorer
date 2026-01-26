# CrossSegmentationExplorer

Cross Segmentation Explorer is a 3D Slicer extension for the visual inspection and comparison of multiple segmentations on the same volume. The extension is designed for CT volumes and segmentations in DICOM SEG format. This extension has been tested exclusively on CT volumes.

---

# Getting Started 
## 1. Prepare Your Environment: How to Set Up 3DSlicer
1. Download the latest stable build of 3D Slicer from https://download.slicer.org and install it.
2. Open the Extension Manager by clicking “Install Extensions” on the left side of the welcome screen, or by clicking the blue button with the “E” and puzzle-piece icon in the toolbar.
<img width="1661" height="710" alt="SlicerWelcomeLayout" src="https://private-user-images.githubusercontent.com/129984042/540527283-a40d7518-edf0-4dfa-abd2-aff4bf15260c.png?jwt=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3Njk0NDYwODgsIm5iZiI6MTc2OTQ0NTc4OCwicGF0aCI6Ii8xMjk5ODQwNDIvNTQwNTI3MjgzLWE0MGQ3NTE4LWVkZjAtNGRmYS1hYmQyLWFmZjRiZjE1MjYwYy5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjYwMTI2JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI2MDEyNlQxNjQzMDhaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT02ODdjNzA0ZDNmYTM5ODFmZDQyNzlkZTIzZTVkMzk1MDZmZTEwMjNkZGE1MDMyYTk0Y2ZmNDM0Y2MwZDViNTJhJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.xe3wqe9XJx_ckJcBjtl3FsmrUDGcLon5JFgGCtQsxWE" />

3. Install the “QuantitativeReporting” extension. This will automatically install the DCMQI dependency as well. Restart 3D Slicer after the installation.
4. Clone this Git repository https://github.com/ImagingDataCommons/CrossSegmentationExplorer.git to your local machine.
5. After restarting Slicer, click the “Customize Slicer” icon (see Screenshot above).
6. Open the “Modules” tab, and on the right side under “Additional module paths,” click the arrow button with the two arrowheads and select “Add.”
7. Navigate to the cloned CrossSegmentationExplorer repository and select the subfolder "CrossSegmentationExplorer" that contains the CrossSegmentationExplorer module, then click “Open.”
8. Restart 3D Slicer again.
9. After the restart, the CrossSegmentationExplorer extension should appear in the module drop-down menu under “Segmentation.”
<img width="1798" height="1039" alt="ModuleDropDown" src="https://private-user-images.githubusercontent.com/129984042/540527541-7d80c72e-c550-4c40-b8b1-38f03698885b.png?jwt=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3Njk0NDYzNDUsIm5iZiI6MTc2OTQ0NjA0NSwicGF0aCI6Ii8xMjk5ODQwNDIvNTQwNTI3NTQxLTdkODBjNzJlLWM1NTAtNGM0MC1iOGIxLTM4ZjAzNjk4ODg1Yi5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjYwMTI2JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI2MDEyNlQxNjQ3MjVaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT03ZDU0ZWUzYmM0M2JhNjc3Mjk3NTJjMjdhN2JhYjVlOWE5YzU4NTBmNDBkMDA1ZjM4YWUwYmE4MDdkZjQ2NzJmJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.T5VdefyPBqX6O3Tcq04hlY76ueCjdaiJa4CbRYO5NwQ" />


## 2. Access Your Data: How and Where to Download Imaging Datasets
⚠️ **Supported Data Formats:** This module currently works only with DICOM volumes and DICOM SEG segmentation files. Other file formats are not supported at the moment.
### Using our published Zenodo Dataset (Recommended)
Download the dataset released with the paper “In search of truth: Evaluating concordance of AI-based anatomy segmentation models” from Zenodo (https://doi.org/10.5281/zenodo.17401359).
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
<img width="1618" height="710" alt="SlicerWelcomeScreenAddDicom" src="https://private-user-images.githubusercontent.com/129984042/540527344-4e4b4faa-80ca-4deb-9ff5-4d2418272a8f.png?jwt=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3Njk0NDYzNDUsIm5iZiI6MTc2OTQ0NjA0NSwicGF0aCI6Ii8xMjk5ODQwNDIvNTQwNTI3MzQ0LTRlNGI0ZmFhLTgwY2EtNGRlYi05ZmY1LTRkMjQxODI3MmE4Zi5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjYwMTI2JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI2MDEyNlQxNjQ3MjVaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT1lN2RhNWFlYzJkNjEyNGFlMTg4NzhjNTc2NWZiMzBiZDQ0ZDVjZmIwZTdiZGU4MzA4MTdlOTBkMDZlMDk3OWQ4JlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.3PFFd22g0Eh0-1yX0fNtAGhSwDGgH8XyJNsi5t_dJaQ" />

2. In the DICOM module, click “Import DICOM Files”.
<img width="1618" height="710" alt="DICOMDatabase" src="https://private-user-images.githubusercontent.com/129984042/540604327-81a6bea3-7178-4bab-87a6-df60d3ac872e.png?jwt=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3Njk0NDY1NjAsIm5iZiI6MTc2OTQ0NjI2MCwicGF0aCI6Ii8xMjk5ODQwNDIvNTQwNjA0MzI3LTgxYTZiZWEzLTcxNzgtNGJhYi04N2E2LWRmNjBkM2FjODcyZS5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjYwMTI2JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI2MDEyNlQxNjUxMDBaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT04NTNmNzg3YTEwN2RhMTJkYmUzOTkxM2U2NWYwYWI4YTMyYjI5NzFmMjAyY2IyYTk0ZGU4OWE2ZGU0OGUyOGI1JlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.yZYpfqcMV7N--J4AOTG--CYTWWvyKZGmn2ex_IRB334" />

3. Select the top-level folder that contains all DICOM files for your dataset (Slicer will automatically detect and organize all subfolders). Wait for Slicer to import the data. Depending on the number and size of the files, this may take some time.
4. After the import is complete, use the DICOM browser to load all data for a patient, only a specific study,or individual series/files. Once the intended data is selected, click “Load” to bring it into the Slicer workspace.

---

# CrossSegmentationExplorer Module

## Demo

<p align="center">
  <a href="https://www.youtube.com/watch?v=meSPWlvQCM8">
    <img
      src="https://private-user-images.githubusercontent.com/129984042/540530779-21a3932a-593b-4ab8-bae6-58e3ca2890d7.png?jwt=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3Njk0NDc2ODgsIm5iZiI6MTc2OTQ0NzM4OCwicGF0aCI6Ii8xMjk5ODQwNDIvNTQwNTMwNzc5LTIxYTM5MzJhLTU5M2ItNGFiOC1iYWU2LTU4ZTNjYTI4OTBkNy5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjYwMTI2JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI2MDEyNlQxNzA5NDhaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT01MTNkZmI2ZWUzZTY4NzM4MGUwNGNkNDc0MmNhYTBlMjQzYWJkMzRlYmI4OWQzOWM0YjFkMzQ0MTAwZGU5NjM0JlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.0VRxkd8ND4GeDnfuTwTnxUCC97EMSlVMykzSREma9Ag"
      style="max-width: 100%; width: 1100px;"
    />
  </a>
</p>



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
     <img width="1700" height="686" alt="SegmentationModelPopUpTable" src="https://private-user-images.githubusercontent.com/129984042/540607359-4ee44891-f4d5-4ed8-9eef-ce13ffb8c0f9.png?jwt=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3Njk0NDY4MzEsIm5iZiI6MTc2OTQ0NjUzMSwicGF0aCI6Ii8xMjk5ODQwNDIvNTQwNjA3MzU5LTRlZTQ0ODkxLWY0ZDUtNGVkOC05ZWVmLWNlMTNmZmI4YzBmOS5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjYwMTI2JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI2MDEyNlQxNjU1MzFaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT0yMGY2Y2Y0ZDM3NTVlNjg0MjJkNjA3NDYxZmVjZDhhNzJiYzhiMzBkMTZiOGNlYzY3MjEzYzU4MWVhZWY1ODg0JlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.ZzzESL8uvNa01WT04pOz7CpJW46D1ZlykZEP9-HfEas" />
     
3. *OPTIONAL:* **Modify the Layout**:
   - By default, three orthogonal 2D views (axial, sagittal, coronal) will be created for each selected segmentation or segmentation model, displaying the CT volume overlaid with the corresponding segmentation
   - In the “Enable 2D & 3D Views” section, you can also enable 3D views. When selected, one 3D view is created for each segmentation file or model, with the corresponding segmentations rendered in that view
   - Each view type (2D or 3D) can be toggled on or off independently. ⚠️ At least one view must be enabled to visualize the data.
   - Additionally, selecting the "Vertical/horizontal Layout" checkbox arranges the 2D views in a vertical layout instead of the default horizontal layout.
     
     *Vertical Layout*
     <img width="1104" height="596" alt="VerticalLayout" src="https://private-user-images.githubusercontent.com/129984042/540530026-c1b09d69-6651-492e-9389-201cd537ef5a.png?jwt=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3Njk0NDY4MzEsIm5iZiI6MTc2OTQ0NjUzMSwicGF0aCI6Ii8xMjk5ODQwNDIvNTQwNTMwMDI2LWMxYjA5ZDY5LTY2NTEtNDkyZS05Mzg5LTIwMWNkNTM3ZWY1YS5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjYwMTI2JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI2MDEyNlQxNjU1MzFaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT02NzZjMzEyNGU4NGIyNGY0OTQ0ODkwMzMxOWI2OGMxYWVjYTExZmY5NzEyZTY1NDJkNjQyMGJkNmEzN2ZiNTAwJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.bvz9A0aoxrseGDE2BPc0yRm-z1j0DhcT2O-WVPreuQo" />

     *Horizontal Layout*
     <img width="1103" height="596" alt="HorizontalLayout" src="https://private-user-images.githubusercontent.com/129984042/540530153-4b6d4976-8cdb-418d-aadb-00175768053c.png?jwt=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3Njk0NDY4MzEsIm5iZiI6MTc2OTQ0NjUzMSwicGF0aCI6Ii8xMjk5ODQwNDIvNTQwNTMwMTUzLTRiNmQ0OTc2LThjZGItNDE4ZC1hYWRiLTAwMTc1NzY4MDUzYy5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjYwMTI2JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI2MDEyNlQxNjU1MzFaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT0zYTZiOWQzZmI4ZGNkM2Y0ODc1OTg2ZWFiMTU3NjYxMDQxYjEzZWQwZmRhMzMzZWRiZGVhMGI0NjBmNGJlNTM5JlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.XTb-4eynTt6k3abB585I10AAJl8C7Qk7BgODm8Vu88Y" />


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
<img width="1816" height="861" alt="RibsGroup" src="https://private-user-images.githubusercontent.com/129984042/540530779-21a3932a-593b-4ab8-bae6-58e3ca2890d7.png?jwt=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3Njk0NDY4MzEsIm5iZiI6MTc2OTQ0NjUzMSwicGF0aCI6Ii8xMjk5ODQwNDIvNTQwNTMwNzc5LTIxYTM5MzJhLTU5M2ItNGFiOC1iYWU2LTU4ZTNjYTI4OTBkNy5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjYwMTI2JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI2MDEyNlQxNjU1MzFaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT05NWIxYWE0NjdmYjRjNjM0MmY4YjIyMDIzZGNiZTdhYWMzNDZiNDRmZGE2MGNmZjNjY2FkMzhhYTkwZTMwZDU5JlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.HbnwDMTns3tF9wgOYnwONYJkOvWjanS7nYKwjomkkGY" />


*Structure-wise comparison of a single rib segment with neighboring segments shown semi-transparent. Neighboring structures are computed separately for each segmentation or model, based on the available segmentations. As each segmentation may contain a different set of anatomical structures, neighboring segments can vary — for example, one model might display adjacent ribs, while another includes nearby organs such as the lungs.*  
 <img width="1816" height="861" alt="NeighboringSemiTransparent" src="https://private-user-images.githubusercontent.com/129984042/540530843-f391f6e8-4ca6-4eef-b2b2-7eb33b2caa37.png?jwt=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3Njk0NDY4MzEsIm5iZiI6MTc2OTQ0NjUzMSwicGF0aCI6Ii8xMjk5ODQwNDIvNTQwNTMwODQzLWYzOTFmNmU4LTRjYTYtNGVlZi1iMmIyLTdlYjMzYjJjYWEzNy5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjYwMTI2JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI2MDEyNlQxNjU1MzFaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT1hMGUxYTJjNDk2NTdjZTUyZjRhYWQ1NDAyZGQ1ZDJkM2U4Mjc5ZTA2NzZhZDQ2Zjc1ZWRmMjc5NzE5NmMyN2JkJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.5NOcT6g6UqgW-J5W_Jd5xPA2EAZ_EG6IFz1zzRu2IoI" />

