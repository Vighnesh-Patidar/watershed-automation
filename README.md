# Watershed Delineation with ArcGIS (Jupyter Notebook)

This Jupyter Notebook automates the process of watershed delineation using ArcGIS, ArcPy, and Conda. It follows these steps:

1. **Download DEM** (already implemented)
2. **Fill Sinks** in the DEM raster
3. **Compute Flow Direction**
4. **Calculate Flow Accumulation**
5. **Generate a Binary Stream Network** (threshold-based)
6. **Prompt User to Save Outlet Points**
7. **Delineate Watershed** based on user-defined outlet points

## Requirements

- **ArcGIS Pro** (with the Spatial Analyst extension)
- **Jupyter Notebook** (with ArcPy kernel)
- **Python** (managed via Conda)
- **ArcPy** (installed with ArcGIS Pro)

## Installation

### Step 1: Set Up Conda Environment
Run the following in a terminal (Anaconda Prompt or Bash):

```bash
conda env create -f environment.yml
conda activate arcgis-watershed
python -m ipykernel install --user --name=arcgis-watershed --display-name "Python (ArcPy)"
```

### Step 2: Open the Jupyter Notebook
```bash
jupyter notebook
```
- Open `watershed_delineation.ipynb`
- Select the **Python (ArcPy)** kernel

## Output Files
- `filled_dem.tif` – DEM with sinks filled
- `flow_direction.tif` – Flow direction raster
- `flow_accumulation.tif` – Flow accumulation raster
- `binary_stream.tif` – Thresholded stream network
- `watershed.tif` – Final watershed raster

## Conda Environment File (`environment.yml`)
Since ArcPy is only available via **Esri’s Conda channel**, the environment setup is as follows:

```yaml
name: arcgis-watershed
channels:
  - esri
  - conda-forge
  - defaults
dependencies:
  - python=3.9
  - jupyter
  - ipykernel
  - arcpy
  - numpy
```

## Requirements File (`requirements.txt`)
For users who prefer `pip`, though ArcPy must be installed via Conda.

```txt
numpy
jupyter
```
> **Note:** ArcPy must still be installed through Conda.

## Conda Environment Initiator for Jupyter (`init_conda_jupyter.sh`)
A shell script to set up the Conda environment and ensure it's registered in Jupyter.

```bash
#!/bin/bash

echo "Setting up ArcGIS watershed delineation environment..."

# Initialize Conda if not already initialized
source ~/anaconda3/etc/profile.d/conda.sh 2>/dev/null || source ~/miniconda3/etc/profile.d/conda.sh 2>/dev/null

# Create the Conda environment
conda env create -f environment.yml

# Activate the environment
conda activate arcgis-watershed

# Add the environment to Jupyter
python -m ipykernel install --user --name=arcgis-watershed --display-name "Python (ArcPy)"

echo "Environment activated. Open Jupyter Notebook and select 'Python (ArcPy)' kernel."
```

To run:
```bash
chmod +x init_conda_jupyter.sh
./init_conda_jupyter.sh
```

