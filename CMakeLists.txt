cmake_minimum_required(VERSION 3.16.3...3.19.7 FATAL_ERROR)

project(CrossSegmentationExplorer)

#-----------------------------------------------------------------------------
# Extension meta-information
set(EXTENSION_HOMEPAGE "https://github.com/ImagingDataCommons/CrossSegmentationExplorer")
set(EXTENSION_CONTRIBUTORS "Lena Giebeler")
set(EXTENSION_DESCRIPTION "Tools for the visual inspection and comparison of multiple segmentations on the same volume.")
set(EXTENSION_ICONURL "https://raw.githubusercontent.com/ImagingDataCommons/CrossSegmentationExplorer/main/CrossSegmentationExplorer/Resources/Icons/logo.png")
set(EXTENSION_SCREENSHOTURLS "https://raw.githubusercontent.com/ImagingDataCommons/CrossSegmentationExplorer/main/CrossSegmentationExplorer/Resources/Screenshot/RibsGroup.png")
set(EXTENSION_DEPENDS "QuantitativeReporting")
set(EXTENSION_CATEGORY "Segmentation")

#-----------------------------------------------------------------------------
# Extension dependencies
find_package(Slicer REQUIRED)
include(${Slicer_USE_FILE})

#-----------------------------------------------------------------------------
# Extension modules
add_subdirectory(CrossSegmentationExplorer)
## NEXT_MODULE

#-----------------------------------------------------------------------------
include(${Slicer_EXTENSION_GENERATE_CONFIG})
include(${Slicer_EXTENSION_CPACK})
