# Repurposing the DART Network to Study the Deep Ocean

This undergraduate research project asks whether New Zealand's tsunami early-warning sensors can double as deep-ocean thermometers.

**Stack:** Python · pandas · matplotlib · argopy · REST API (GeoNet) · Jupyter

📄 **Full report:** [`research_report.pdf`](research_report.pdf)

## Purpose

Deep-ocean data is scarce due to the vastness of the ocean and the high cost of implmenting new instruments. This project aims to improve its availability by **repurposing existing infrastructure**.

GeoNet's **DART** tsunami-warning network has 12 bottom pressure recorders on the sea floor around New Zealand. Each contains a sensor that monitors the temperature of its internal components. This project investigates whether this data can be repurposed as a measurement for the surrounding deep-water temperature, which would create new historical datasets for fixed-location deep-ocean temperatures at no cost.

## Discovery

Each day's temperature shows a clear **sinusoidal pattern** mixed with hourly spikes. These spikes appear in consistent strength and periods, and are likely a result of some functionailty related to the instruments. The sinusoidal pattern is present each day, but with varying strength. The sinoidal shape leads me to believe this is a natural pattern caused by the Earth's rotation and gravitational pull from the moon/sun, something similar to tidal forcing. This sinusoidal pattern is the most promising potential area for future study.

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="figures/daily_cycle_dark.png">
  <img src="figures/daily_cycle_light.png" alt="Line chart of NZE sensor 40 temperature on 1 January 2020 (UTC). The 3-minute readings spike at the start of every hour. Their 1-hour average forms a smooth wave, rising from 1.2293 °C at midnight to about 1.2298 °C around 07:00–09:00, falling to about 1.2292 °C near 16:00, then climbing back to about 1.2299 °C by 23:00.">
</picture>

Questions for further studies:

- Does the the pattern strength vary over a yearly cycle with the gravitational strength from the **Sun's**, peaking in early January when Earth is closest to the Sun?
- Does the pattern strength change over a monthly cycle as the **Moon's** gravitational pull varies, do they peak with full and new moons?
- How does the strength of the pattern compare between sensors and stations, does the pattern vary across **locations**?

## Limitations

- **Wrong absolute values:** Each sensor has a different base temperature measurement, including sensors at the same station location.
- **Event mode:** Preassure spikes causes the sampling rate to increase resulting in greater heat for a fixed period.
- **Sub-hourly data:** Lot of noisy data on a sub-hourly timescale from the base functionality of the instrument.
- **Data avaliability** Temperature data is stored localy on the sensor and is only avaliable after maintaince, which is about every two years.

## Approach

- Wrote a small client for the GeoNet API that pulls temperature, pressure and water-height records for all 12 stations and their sensors.
- Detected and isolated periods when the device switched to rapid "event mode" sampling, and measured their effect on the temperature.
- Checked reliability against Deep Argo floats, a trusted independent source, using `argopy`.
- Compared sensors within and across stations, and searched for natural patterns at daily, monthly and yearly timescales.

## Acknowledgements

Supervised by Melissa Bowen. DART data from [GeoNet / GNS Science](https://doi.org/10.21420/8TCZ-TV02); Argo data from the [International Argo Program](https://doi.org/10.17882/42182).
