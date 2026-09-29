# Repurposing the DART Network to Study the Deep Ocean

This undergraduate research project asks whether New Zealand's tsunami early-warning sensors can double as deep-ocean thermometers.

**Stack:** Python · pandas · matplotlib · argopy · REST API (GeoNet) · Jupyter

📄 **Full report:** [`research_report.pdf`](research_report.pdf)

## Purpose

Deep-ocean data is scarce because putting instruments on the sea floor is costly and difficult. This project aims to improve its availability by **repurposing existing infrastructure**.

GeoNet's **DART** tsunami-warning network has 12 bottom pressure recorders on the sea floor around New Zealand, some nearly 6,000 m down. Each contains a sensor that monitors the temperature of its internal components. This project investigates whether that data can be repurposed as a measure of the surrounding deep-water temperature, which would create new historical datasets for fixed-location deep-ocean temperatures with no cost.

## Discovery: a daily sinusoidal cycle

Each day's temperature shows a **clear sinusoidal pattern** mixed with hourly spikes. The spikes are consistent strength and likely caused by the some instrument related functionally. The sinusoidal pattern is present each day, but with varying strength. The sinoidal shape leads me to believe this is a natural pattern caused by the Earth's rotation and gravitational pull from the moon/sun, something similar to tidal forcing. This is the area, with the most promising potential for future study.

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="figures/daily_cycle_dark.png">
  <img src="figures/daily_cycle_light.png" alt="Line chart of NZE sensor 40 temperature on 1 January 2020 (UTC). The 3-minute readings spike at the start of every hour. Their 1-hour average forms a smooth wave, rising from 1.2293 °C at midnight to about 1.2298 °C around 07:00–09:00, falling to about 1.2292 °C near 16:00, then climbing back to about 1.2299 °C by 23:00.">
</picture>

Questions for further studies:

- Does the the pattern strength over a yearly cycle as the **Sun's** gravitational pull varies, peaking in early January when Earth is closest to the Sun?
- Does the pattern strength change over a monthly cycle as the **Moon's** gravitational pull varies, peaking during full and new moons?
- How does the strength of the pattern compare between sensors and stations, does the pattern vary across **locations or instruments**?

## Limitations

- **Wrong absolute values:** the sensor measures inside the housing, not the water, and reads about 0.1 °C warmer than nearby Deep Argo floats.
- **Changes at each servicing:** every redeployment shifts the baseline unpredictably (up to about 1.5 °C), so each deployment would need its own calibration.
- **Device heating:** event mode and deployment start-up both heat the sensor, and the effect lingers after they end.
- **No sub-hourly data:** an hourly spike from the instrument itself makes readings below hourly resolution unreliable.
- **Delayed data:** temperature isn't transmitted. It only becomes available when the unit is serviced, about every two years.

## Approach

- Wrote a small client for the GeoNet API that pulls temperature, pressure and water-height records for all 12 stations and their sensors.
- Detected and isolated periods when the device switched to rapid "event mode" sampling, and measured their effect on the temperature.
- Checked reliability against Deep Argo floats, a trusted independent source, using `argopy`.
- Compared sensors within and across stations, and searched for patterns at daily, monthly and yearly timescales.

## Run it

```bash
pip install -r requirements.txt    # Python 3.11+
jupyter notebook src/main.ipynb    # fetches data live from GeoNet and Argo
```

## Acknowledgements

Supervised by Melissa Bowen. DART data from [GeoNet / GNS Science](https://doi.org/10.21420/8TCZ-TV02); Argo data from the [International Argo Program](https://doi.org/10.17882/42182).
