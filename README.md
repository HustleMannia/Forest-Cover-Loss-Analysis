# Forest-Cover-Loss-Analysis
orest cover loss analysis involves studying the reduction in the area of forests over time due to natural or human-induced factors. This analysis is crucial for understanding environmental impacts, biodiversity loss, and climate change. Key steps in forest cover loss analysis typically include: 


Team member 
1. Kshitij Gujar
2. Diya chauhan
3. Shrey patel
4. Dev Vyas
5. Charmi Gondaliya


       Libraries are used in this project 
       1. pandas 
       2. Nampy 
       3. seashore 

       Forest cover loss Analysis 

## Contributors
1. Kshitij Gujar(KU2407U323)-Python coding
2. Diya chauhan(KU2407U278)-Manage all the files
3. Shrey patel(KU2407U377)-Manage all the datasets
4. Dev vyas(KU2407U271)-Code execution and code screenshots
5. Charmi Gondaliya(KU2407U268)-Support in all the departments

  

## Table of Contents
1. [Introduction]
2. [Objective]
3. [Tools and Libraries Used]
4. [Data Sources]
5. [Installation]
6. [Usage]
7. [Analysis and Insights]
8. [Visualizations]
9. [Challenges Faced]
10. [Contributors]
11. [License]

---

## Introduction
This project explores Forest cover loss  within India and globally. Using data-driven analysis, we aim to understand key trends, factors of Forest Cover loss , and the socio-economic impact. The project involves data preprocessing, statistical analysis, and visualization of Forst cover loss 

## Objective
The objective is to identify and visualize Forest cover loss , uncover key insights, and present a clear understanding of patterns in population movement over time. 


# Data Sources
- (Include the datasets or public data repositories used for the project)
- Mention sources such as census data, Forest cover loss  reports, or any open datasets.

## Installation
1. Clone the repository:

   git clone https://github.com/[The_AI_aces]/forest_cover_loss_analysis.git 

2. Navigate to the project directory:

   cd forest_cover_Analysis

3. Install the required libraries:

   pip install -r requirements.txt


## Usage
1. Load the Jupyter notebooks or Python scripts from the `src/` folder.
2. Execute the analysis scripts as described in the documentation.
3. View generated visualizations in the `visuals/` folder.

## Analysis and Insights
- Provide a summary of key findings, such as:
  - To analysis sesonal forest cover analysis 
  - Seasonal forest cover analysis  
  

## Visualizations
- Include sample visualizations like:
  - Heatmaps Seasonal forest cover analysis 
  - Comparative bar charts for Seasonal forest cover analysis   

## Challenges Faced
- Data cleaning issues (e.g., missing or incomplete data) 
- Handling large datasets
- Visualizing complex Forest cover  loss analysis 


# Import necessary libraries
import numpy as np
import matplotlib.pyplot as plt
import rasterio
from rasterio.plot import show

# List of years with corresponding GeoTIFF file paths
years = [2020, 2021, 2022]  # Example years
file_paths = [f"forest_{year}.tif" for year in years]  # Replace with actual file paths

# Initialize storage for deforested areas
deforested_areas = []

# Function to load GeoTIFF data
def load_raster(file_path):
    with rasterio.open(file_path) as src:
        data = src.read(1)  # Read the first band
        meta = src.meta  # Metadata for resolution
    return data, meta

# Process data for each pair of consecutive years
for i in range(len(file_paths) - 1):
    # Load raster data for the current year and next year
    current_data, meta = load_raster(file_paths[i])
    next_data, _ = load_raster(file_paths[i + 1])

    # Calculate forest change (deforestation)
    forest_change = next_data - current_data

    # Calculate deforested area (pixels with negative change)
    pixel_resolution = meta['transform'][0]  # Pixel size in meters
    deforested_area = np.sum(forest_change < 0) * pixel_resolution**2  # Area in square meters
    deforested_areas.append(deforested_area)

    # Visualize the forest change
    plt.figure(figsize=(10, 6))
    show(forest_change, cmap='RdYlGn', title=f"Forest Change ({years[i]}-{years[i+1]})")
    plt.colorbar(label="Change in Forest Cover")
    plt.show()

    # Print the calculated deforested area
    print(f"Deforested Area from {years[i]} to {years[i+1]}: {deforested_area} square meters")

# Plot deforestation trend over years
plt.figure(figsize=(8, 5))
plt.plot(years[:-1], deforested_areas, marker='o', linestyle='-', color='red')
plt.title("Yearly Deforestation Trends")
plt.xlabel("Year")
plt.ylabel("Deforested Area (sq meters)")
plt.grid(True)
plt.show()

print("Analysis Complete!")
