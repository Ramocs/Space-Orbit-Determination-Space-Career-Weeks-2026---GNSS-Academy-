# Multi-Satellite Orbit Propagation and Visualization

## Project Overview

This project was developed during the **Space Career Week 2026**, organized by **GNSS Academy**.

The objective is to develop a Python-based tool capable of processing satellite orbital data, propagating multiple satellite orbits over a common time window, and visualizing their motion around the Earth.

Starting from General Perturbations (GP) orbital data, the program reconstructs the Keplerian orbital elements, propagates satellite positions using a two-body model, and generates both graphical and geospatial outputs.

The project combines fundamental astrodynamics concepts with practical Python programming and data visualization techniques.

## Objectives

The main objectives of the project are:

- Import and process satellite orbital data in JSON format.
- Convert GP mean elements into the orbital parameters required for propagation.
- Propagate multiple satellite orbits over a common UTC time window.
- Calculate satellite position, altitude, and orbital velocity.
- Account for Earth's rotation to obtain Earth-fixed coordinates.
- Visualize satellite ground tracks and velocity evolution.
- Export orbital trajectories in KML format for visualization in Google Earth.

## Methodology

### 1. Orbital Data Acquisition and Processing

The program reads satellite orbital records provided in JSON format, containing parameters such as:

- Satellite name and NORAD catalogue ID.
- Epoch.
- Mean motion.
- Eccentricity.
- Inclination.
- Right Ascension of the Ascending Node (RAAN).
- Argument of Pericentre.
- Mean Anomaly.

The mean motion is converted from revolutions per day to radians per second. Using Kepler's third law, the semi-major axis is calculated.

Angular quantities are converted from degrees to radians, providing a consistent set of orbital elements for the propagation model.

### 2. Orbital Propagation

Satellite trajectories are computed using a **two-body Keplerian propagation model**.

For each satellite and each time step, the program:

1. Computes the mean anomaly at the current time.
2. Solves Kepler's equation using the Newton–Raphson method.
3. Calculates the eccentric anomaly and true anomaly.
4. Determines the satellite position in an Earth-centred inertial-like reference frame.
5. Applies Earth's rotation using Greenwich Mean Sidereal Time (GMST).
6. Converts the resulting position into geocentric latitude, longitude, and altitude.
7. Computes orbital velocity using the vis-viva equation.

All satellites are propagated over the same 24-hour UTC interval, using a time step of 5 seconds.

### 3. Orbit Analysis

The program generates an orbital summary for each satellite, including:

- Orbital period.
- Perigee and apogee altitude.
- Eccentricity.
- Inclination.
- Minimum and maximum orbital speed.

Additional physical consistency checks are implemented to verify the numerical solution of Kepler's equation and selected orbital characteristics.

### 4. Data Visualization

Matplotlib is used to generate two main graphical outputs:

- **Ground tracks:** satellite trajectories plotted over a world map, using longitude and latitude coordinates.
- **Velocity time histories:** orbital speed evolution over the propagation window, with a separate plot for each satellite.

### 5. Google Earth Integration

The computed trajectories are exported into KML files, enabling their visualization in Google Earth.

Two different representations are generated:

- `orbit_tracks_ecef.kml`: Earth-fixed three-dimensional orbital trajectories.
- `orbit_animation.kml`: time-dependent ground-track animation, compatible with the Google Earth time slider.

This provides an intuitive way to inspect satellite motion and compare the trajectories of different spacecraft.

## Numerical Model and Assumptions

The propagation is based on the classical two-body gravitational model, using:

- Earth's gravitational parameter: 398600.4418 km³/s².
- Earth radius: 6378.137 km, approximated as a sphere.
- Keplerian orbital propagation.
- Greenwich Mean Sidereal Time for Earth's rotation.
- Vis-viva equation for orbital velocity.

The model neglects perturbations such as atmospheric drag and Earth's non-spherical gravitational field (J2).

Consequently, the results are intended for educational and analytical purposes rather than precision orbit prediction.

## Main Deliverables

The notebook automatically generates the following outputs:

| File | Description |
|---|---|
| `ground_tracks.png` | Satellite ground-track visualization |
| `velocity_timeseries.png` | Orbital velocity evolution |
| `orbit_tracks_ecef.kml` | Earth-fixed orbital trajectories |
| `orbit_animation.kml` | Animated satellite ground tracks |
| `orbit_report.txt` | Orbital elements and propagation summary |
| `satellite_orbit_outputs.zip` | Archive containing all generated deliverables |

## Technologies and Tools

- **Python**
- NumPy-style numerical operations using Python's standard mathematical library
- Matplotlib – data visualization
- JSON – orbital data processing
- XML / KML – geospatial data generation
- Google Earth – trajectory visualization
- Google Colab – execution environment

## How to Run

The notebook is designed to run in Google Colab.

1. Open `Space_Orbit_GNSS_Academy.ipynb` in Google Colab.
2. Upload the `orbit_workshop_inputs.zip` archive into the `/content` directory using the Colab Files panel.
3. Run all notebook cells.
4. The program automatically extracts the required input files, processes the orbital data, propagates the satellite trajectories, and generates the output files.
5. The final ZIP archive is downloaded automatically.

The input archive must contain:

- `orbital_elements.json`
- `data_manifest.json`
- `world_map.txt`

## Acknowledgements

Developed during the **Space Career Week 2026**, organized by **GNSS Academy**.

This project provided practical experience in orbital mechanics, satellite trajectory propagation, geospatial data processing, and scientific programming.

