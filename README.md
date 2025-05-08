
# Solar Geomagnetic Storm Prediction

This project estimates the geomagnetic storm index (Dst) using a physical model based on satellite data (OMNI dataset) and linear regression with least squares fitting. The goal is to predict geomagnetic activity on Earth with one hour of anticipation using solar wind parameters.

---

## Overview

The project uses space weather data to model and forecast the geomagnetic storm index Dst (Disturbance storm time index). The OMNI dataset provides the necessary parameters from satellites such as:

- **Bz (nT):** North-South component of the interplanetary magnetic field.
- **Speed (km/s):** Solar wind speed.
- **Pressure (nPa):** Dynamic pressure of the solar wind.
- **Dst (nT):** Index of geomagnetic storm intensity (the value to predict).

---

## Physics Basis

The prediction model is built on a simplified physical representation:

### **Rectified Electric Field Ey:**

\[
E_y = V \cdot B_z \quad 	ext{if } B_z < 0, 	ext{ else } 0
\]

This equation assumes that the main geoeffective component is southward Bz. When Bz is negative, solar wind energy is transferred more efficiently to the Earth's magnetosphere.

---

## Mathematical Model

The core predictive model applies **least squares linear regression** using:

\[
Dst(t+1) = lpha \cdot Dst(t) + eta \cdot E_y(t) + \gamma \cdot P(t)
\]

Where:
- \( Dst(t) \): Current Dst
- \( E_y(t) \): Rectified electric field
- \( P(t) \): Solar wind pressure

The coefficients Î±, Î², and Î³ are calculated for each event using linear algebra:

\[
X = (A^T A)^{-1} A^T Y
\]

Where:
- A = matrix with [Dst, Ey, Pressure]
- Y = future Dst

---

## Dataset

- `omni.txt`: Hourly OMNI data with solar wind parameters.
- `tormentas.txt`: CSV with time intervals of geomagnetic storms.
- Data is parsed using `pandas` and dates are filtered for each storm window.

---

## Outputs

- `coefficients.csv`: Coefficients Î±, Î², Î³ for each storm.
- **Visualizations:**
  - Histogram distributions of Î±, Î², Î³.
  - Comparison of predicted vs real Dst values.

---

## Technologies

- Python
- NumPy, Pandas, Matplotlib, Seaborn
- Jupyter Notebook
- Data Source: [NASA OMNIWeb](https://omniweb.gsfc.nasa.gov/)

---