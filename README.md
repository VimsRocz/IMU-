# IMU-
IMU data processing and initialization tools (Python)

## Installation

Install dependencies with:

```bash
pip install -r requirements.txt
```

## Notes

`GNSS_IMU_Fusion.py` now detects a low-motion interval in the IMU data to
estimate the initial accelerometer and gyroscope biases. The magnitude of the
static accelerometer vector is used to compute a simple scale factor so that the
measured gravity is close to 9.81 m/s². This improves the attitude
initialisation when the first samples are not perfectly static or the sensor
scale is slightly off.

## Running all methods

Use `run_all_methods.py` to execute the fusion script with TRIAD, Davenport and SVD sequentially:

```bash
python run_all_methods.py --imu-file IMU_X001.dat --gnss-file GNSS_X001.csv
```

## Running all data sets

To process every IMU/GNSS pair defined in `run_all_datasets.py`, simply run:

```bash
python run_all_datasets.py
```

After all runs complete you can compare the datasets side by side:

```bash
python plot_compare_all.py
```
This creates one `all_datasets_<method>_comparison.pdf` per method in
`results/`.

## Automated figure generation

The module `auto_plots.py` contains helper routines for creating the standard
set of plots and a summary table of metrics for each batch run.  Integrate
these helpers into your own batch script to automatically export the six
"must‑have" figures (tasks 3–5 and validation plots) and a CSV/LaTeX table of
RMSE and innovation statistics.

## Tests

Run the unit tests with `pytest`:

```bash
pytest -q
```
