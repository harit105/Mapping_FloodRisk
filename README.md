# Mapping Flood Risk

This project visualizes flood risk in Manila using Folium, a Python library for creating interactive maps.

## Prerequisites

- Python 3.x
- Jupyter Notebook
- Required Python packages: `folium`, `pandas`, `numpy`

## Installation

1. Clone the repository:
    ```sh
    git clone <repository-url>
    cd <repository-directory>
    ```

2. Install the required packages:
    ```sh
    pip install folium pandas numpy
    ```

## Usage

1. Open the Jupyter Notebook:
    ```sh
    jupyter notebook MappingFloodRisk.ipynb
    ```

2. Run the notebook cells to generate the flood risk map.

## Code Overview

### MappingFloodRisk.ipynb

This notebook contains the following key sections:

- **Initialize Map**: Creates a Folium map centered on Manila.
    ```python
    map_flood_risk = folium.Map(location=manila_coords, zoom_start=12)
    ```

- **Add Markers**: Iterates over the cleaned data and adds circle markers to the map based on latitude, longitude, and risk color.
    ```python
    for index, row in data_clean.iterrows():
        folium.CircleMarker(
            location=[row['lat'], row['lon']],
            radius=5,
            color=row['risk_color'],
            fill=True,
            fill_color=row['risk_color'],
            fill_opacity=0.7
        ).add_to(map_flood_risk)
    ```

- **Create Legend**: Adds a legend to the map to explain the risk color coding.
    ```python
    legend_html = '''
    <div style="position: fixed; 
                bottom: 50px; left: 50px; width: 150px; height: 150px; 
                border:2px solid grey; z-index:9999; font-size:14px;
                background-color:white; opacity: 0.8;">
        &nbsp;<b>Flood Risk Score</b><br>
        &nbsp;<i class="fa fa-circle" style="color:green"></i>&nbsp;Low (0.0 - 0.2)<br>
        &nbsp;<i class="fa fa-circle" style="color:yellow"></i>&nbsp;Moderate (0.2 - 0.4)<br>
        &nbsp;<i class="fa fa-circle" style="color:orange"></i>&nbsp;High (0.4 - 0.6)<br>
        &nbsp;<i class="fa fa-circle" style="color:red"></i>&nbsp;Very High (0.6 - 0.8)<br>
        &nbsp;<i class="fa fa-circle" style="color:darkred"></i>&nbsp;Severe (0.8 - 1.0)
    </div>
    '''
    map_flood_risk.get_root().html.add_child(folium.Element(legend_html))
    ```

- **Save and Display Map**: Saves the map to an HTML file and displays it.
    ```python
    map_flood_risk.save('/Users/haritshah/Desktop/Dataset/flood_risk.html')
    map_flood_risk
    ```

## Data

The data used in this project should be cleaned and stored in a DataFrame named `data_clean` with the following columns:
- `lat`: Latitude of the location
- `lon`: Longitude of the location
- `risk_color`: Color representing the flood risk level

## License

This project is licensed under the MIT License.
