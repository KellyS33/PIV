# PIV
This manual provides a step-by-step guide to using scripts designed for **Particle Image Velocimetry** (PIV) to derive pressure from a spheroid growing in an enclosed environment. The workflow ensures accurate processing of medical imaging data and includes:

1. 8-bit Conversion (8bit_converter.py): Converts all image types to .tif/.tiff format for compatibility.

2. Image Registration (image_registration.py): Aligns a moving image with a reference image and crops the result.

3. Point Selection (Select_Same_points_in_image_pairs.py): Allows users to manually select corresponding points on images.

4. Correction Maker (displacement_correction.py & displacement_correction_badcontrast.py): Adjusts displacements based on contour thresholds.

5. Pressure Derivation (derivation_pressure.py): Calculates pressure using corrected displacement data and simulation-based datasets.

# 1. 8-bit Conversion (8bit_converter.py)
**Purpose**

Converts images of various types into .tif or .tiff format for compatibility with the pipeline. 

Skip this step if images are already in .tif/.tiff format.

**Usage Instructions**

1. Ensure ImageJ/Fiji is installed.

2. Open ImageJ/Fiji and run 8bit_converter.py.

3. Specify the input folder containing images and the output folder for .tif/.tiff files.

**Example Input**

Input Folder: ./input_images

Output Folder: ./output_images

**Output**

Converted .tif/.tiff files saved in the output folder.

# 2. Image Registration (image_registration.py)
**Purpose**

Aligns the moving image with the reference image and crops the result for consistent analysis.

**Usage Instructions**

1. Run image_registration.py.

2. Input the paths to the reference image and the image to be aligned (separated by a comma).

3. Specify the output file path (including the file name).

4. Input the crop size for the image (recommended value: 0.1).

**Example Input**

Reference Image: ./input_images/ref_image.tif

Moving Image: ./input_images/moving_image.tif

Output File: ./output_images/aligned_image.tif

Crop Size: 0.1

**Output**

Aligned and cropped image saved at the specified output file path.

# 3. Point Selection (Select_Same_points_in_image_pairs.py)
**Purpose**

Allows users to manually select corresponding points on the reference and aligned images.

**Usage Instructions**

1. Run Select_Same_points_in_image_pairs.py.

2. Input the paths to the reference image, aligned image, and the output Excel file.

3. Select points on the reference image first, followed by the aligned image.

4. Use right-click to remove any selected points.

**Example Input**

Reference Image: ./output_images/ref_image.tif

Aligned Image: ./output_images/aligned_image.tif

Output Excel: ./output_data/selected_points.xlsx

**Output**

Excel file containing selected points saved at the specified output path.

**Example Image for points**

<img width="550" alt="image" src="https://github.com/user-attachments/assets/3f4be27e-984f-4de5-8da8-3859800f439d" />

# 4. Correction Maker
**Scripts**

displacement_correction.py (for high-contrast images).

displacement_correction_badcontrast.py (for low-contrast images).

**Purpose**

Applies contour-based corrections to adjust selected points and ensure proper displacement calculations.

**Usage Instructions**

1. Run the appropriate script based on image contrast.

2. Input the paths to the aligned reference image, the Excel file from the previous step, and the output Excel file.

3. Adjust threshold and angle parameters as prompted to achieve the best fit.

**Example Input**

Aligned Reference Image: ./output_images/aligned_image.tif

Input Excel: ./output_data/selected_points.xlsx

Output Excel: ./output_data/corrected_points.xlsx

Threshold: 0.9

Angle: 20

**Output**

Corrected Excel file with adjusted points. Graph of radius vs. angle.

**Example Image**

<img width="497" alt="image" src="https://github.com/user-attachments/assets/7317a5cb-3153-4c1a-a328-b7bd61abcb7d" />

<img width="360" alt="image" src="https://github.com/user-attachments/assets/96907bf4-0e15-49d6-88d1-879dc2485afd" />


# 5. Pressure Derivation (derivation_pressure.py)

**Purpose**

Calculates pressure values based on corrected displacement data and simulation-based datasets.

**Usage Instructions**

1. Run derivation_pressure.py.

2. Input the paths to the corrected Excel file and the simulation database folder.

3. Specify the output Excel file.

**Example Input**

Corrected Excel: ./output_data/corrected_points.xlsx

Simulation Database: ./simulation_data/

Output Excel: ./output_data/pressure_results.xlsx

**Output**

Excel file containing pressure values and visual plots.


# Integration Notes
Each script is modular and can be used independently or as part of the pipeline.
Test each script with sample data before applying to real datasets.
Use version control to track script modifications.
For further assistance, refer to inline comments within each script or contact the development team.
