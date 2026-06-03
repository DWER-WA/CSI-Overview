# Western Australia Climate Science Initiative (WA CSI)

The Western Australia Climate Science Initiative (WA CSI) is a Western Australian Government program to produce high-resolution climate projections for the state. It builds on partnerships with NSW DCCEEW, Murdoch University, and the Pawsey Supercomputing Research Centre to deliver dynamically downscaled projections at 4 km resolution, based on CMIP6 global models and aligned with efforts like NARCliM2.0.

CSI develops detailed, WA-specific climate change projections to help government, industry, and communities understand and plan for future climate risks, extremes, and impacts. This GitHub repository contains support materials, documentation, evaluation details, or related resources for WA CSI climate projections.

This GitHub organisation hosts modelling workflows, data processing tools, evaluation materials, and visualisation scripts supporting transparent and reproducible climate science for Western Australia.

---

## Introduction

WA CSI develops detailed, WA-specific climate change projections to help government, industry, and communities understand and plan for future climate risks, extremes, and impacts.

Projections are produced using convection-permitting regional climate models (RCMs) run at 4 km resolution over Southwest Western Australia, driven by a selection of CMIP6 global climate models (GCMs) under two emissions scenarios: a low-emissions pathway (SSP1-2.6), medium-emissions pathway (SSP2-4.5) and a high-emissions pathway (SSP3-7.0).

For general information and frequently asked questions, see the official WA CSI page:  
**https://www.wa.gov.au/service/environment/environment-information-services/climate-science-initiative-frequently-asked-questions**

---

## Data Specifications

| Property | Details |
|---|---|
| **Timescale** | Daily and monthly |
| **Spatial domain** | Southwest Western Australia (SWWA): (109.62°,-37.07°)(124.35°,-27.49°) in rotated pole grid (south west and north east corner) |
| **Horizontal resolution** | ~4 km (convection-permitting) |
| **Regional climate model** | WRF (Weather Research and Forecasting) |
| **Driving data** | CMIP6 GCMs (ACCESS-ESM1-5, EC-Earth3-Veg, MPI-ESM1-2-HR, NorESM2-MM and UKESM1-0-LL|
| **Emissions scenarios** | SSP1-2.6 (low), SSP2-4.5 (medium) SSP3-7.0 (high) |
| **Historical period** | 1951–2014 (model) |
| **Future period** | 2015–2100 |
| **Output format** | NetCDF-4 |

---

## Model Ensemble

CSI uses five CMIP6 global climate models (GCMs) dynamically downscaled using two configurations of the Weather Research and Forecasting (WRF) model v4.12, producing a 10-member ensemble. The two RCM configurations (R3 and R5) differ only in their planetary boundary layer (PBL) scheme; R5 produces slightly warmer hindcasts and projections than R3.

GCM selection follows the methodology outlined in Di Virgilio et al. (2022): [https://doi.org/10.1029/2021EF002625](https://doi.org/10.1029/2021EF002625)

### Driving GCMs

| GCM (`driving_source_id`) | Variant (`driving_variant_label`) | GCM calendar | Atmosphere lat/lon grid (°) | Experiments | Time period |
|---|---|---|---|---|---|
| ACCESS-ESM1-5 | r6i1p1f1 | standard | 1.2 × 1.8 | ssp126, ssp245, ssp370, historical | 2015–2100 / 1951–2014 |
| EC-Earth3-Veg | r1i1p1f1 | standard | 0.7 × 0.7 | ssp126, ssp245, ssp370, historical | 2015–2100 / 1951–2014 |
| MPI-ESM1-2-HR | r1i1p1f1 | standard | ~0.9 | ssp126, ssp245, ssp370, historical | 2015–2100 / 1951–2014 |
| NorESM2-MM | r1i1p1f1 | 365_day | 0.9 × 0.9 | ssp126, ssp245, ssp370, historical | 2015–2100 / 1951–2014 |
| UKESM1-0-LL | r1i1p1f2 | 360_day | 1.3 × 1.9 | ssp126, ssp245, ssp370, historical | 2015–2100 / 1951–2014 |

> **Note:** The NorESM2-MM driving model uses a 365-day no-leap-year calendar, UKESM1-0-LL uses a 360-day calendar, and the remaining three GCMs use a regular leap-year calendar. This affects filename date conventions (see [Data Organisation](#data-organisation)).

### Regional Climate Models

Each GCM is downscaled with both RCM configurations, producing 10 ensemble members in total.

| RCM (`source_id`) | PBL scheme | Vertical levels |
|---|---|---|
| `CSI-WRF412R3` | MYNN2 | 45 |
| `CSI-WRF412R5` | ACM2 | 45 |

Both RCMs use the Thompson microphysics scheme, Betts-Miller-Janjic cumulus physics, RRTMG shortwave/longwave radiation, and Noah-MP land surface with dynamic vegetation.

### ERA5-driven evaluation runs

In addition to GCM-driven projections, ERA5 reanalysis-driven simulations are provided for the historical period to support model evaluation.

---

## Output Variables

CSI outputs the [CORDEX core variable list](https://is-enes-data.github.io/CORDEX_IS-ENES_Variables_v1.pdf) with the cloud area fraction (`clt`) in pending. Output frequencies are **daily** and **monthly** only.

| Variable | Units | Long name | CF Standard name | Monthly | Daily |
|---|---|---|---|:---:|:---:|
| `tas` | K | Near-Surface Air Temperature | `air_temperature` | ✓ | ✓ |
| `tasmax` | K | Daily Maximum Near-Surface Air Temperature | `air_temperature` | ✓ | ✓ |
| `tasmin` | K | Daily Minimum Near-Surface Air Temperature | `air_temperature` | ✓ | ✓ |
| `pr` | kg m⁻² s⁻¹ | Precipitation | `precipitation_flux` | ✓ | ✓ |
| `evspsbl` | kg m⁻² s⁻¹ | Evaporation Including Sublimation and Transpiration | `water_evapotranspiration_flux` | ✓ | ✓ |
| `huss` | 1 | Near-Surface Specific Humidity | `specific_humidity` | ✓ | ✓ |
| `hurs` | % | Near-Surface Relative Humidity | `relative_humidity` | ✓ | ✓ |
| `ps` | Pa | Surface Air Pressure | `surface_air_pressure` | ✓ | ✓ |
| `psl` | Pa | Sea Level Pressure | `air_pressure_at_mean_sea_level` | ✓ | ✓ |
| `sfcWind` | m s⁻¹ | Near-Surface Wind Speed | `wind_speed` | ✓ | ✓ |
| `uas` | m s⁻¹ | Eastward Near-Surface Wind | `eastward_wind` | ✓ | ✓ |
| `vas` | m s⁻¹ | Northward Near-Surface Wind | `northward_wind` | ✓ | ✓ |
| `rsds` | W m⁻² | Surface Downwelling Shortwave Radiation | `surface_downwelling_shortwave_flux_in_air` | ✓ | ✓ |
| `rlds` | W m⁻² | Surface Downwelling Longwave Radiation | `surface_downwelling_longwave_flux_in_air` | ✓ | ✓ |
| `orog` | m | Surface Altitude | `surface_altitude` | — | fx |
| `sftlf` | % | Percentage of the Grid Cell Occupied by Land | `land_area_fraction` | — | fx |

*fx = fixed field (time-invariant); ✓ = available; — = not applicable*

---

## Data Access

CSI projection data are archived at the National Computational Infrastructure (NCI) and can be accessed via the NCI Data Catalogue:

**DOI: https://doi.org/10.25914/3jys-sb70**  
**NCI Catalogue record: https://geonetwork.nci.org.au/geonetwork/srv/eng/catalog.search#/metadata/f7470_9949_4959_4127**

### NCI Users

To access CSI data from NCI's Gadi or via the [ARE interface](https://opus.nci.org.au/display/Help/ARE+User+Guide), apply for access to project `kr82` via [my.nci.org.au](https://my.nci.org.au). Data are located at:

```
/g/data/kr82/CSI/output-CMIP6/DD/
```

### Non-NCI Users

Data can be browsed and downloaded without an NCI account via the THREDDS Data Server:

**https://thredds.nci.org.au/thredds/catalog/kr82/CSI/output-CMIP6/DD/catalog.html**

---

## Data Analysis

Worked examples, notebooks, and analysis tools for working with CSI data are available in the companion repository:

**https://github.com/DWER-WA/CSI-DataAnalysis**

---

## Data Organisation

CSI data at NCI (project `kr82`) is organised following CORDEX-CMIP6 directory conventions. The base path on NCI Gadi is:

```
/g/data/kr82/CSI/output-CMIP6/DD/
```

The full directory structure is:

```
/g/data/kr82/CSI/output-CMIP6/DD/
└── <domain_id>/                       e.g. SWWA-04
    └── <institution_id>/              e.g. DWER-MU
        └── <driving_source_id>/       e.g. ACCESS-ESM1-5
            └── <driving_experiment_id>/   e.g. ssp370
                └── <driving_variant_label>/   e.g. r6i1p1f1
                    └── <source_id>/       e.g. CSI-WRF412R3
                        └── <version_realisation>/   e.g. v1-r1
                            └── <freq>/    e.g. day
                                └── <variable_id>/   e.g. tasmax
                                    └── <version>/   e.g. v20260127
                                        └── <netcdf_filename>.nc
```

### Directory component reference

| Component | Example(s) | Notes |
|---|---|---|
| `domain_id` | `SWWA-04` | Southwest Western Australia at 4 km resolution |
| `institution_id` | `DWER-MU` | Dept. of Water and Environmental Regulation & Murdoch University |
| `driving_source_id` | `ACCESS-ESM1-5`, `EC-Earth3-Veg`, `MPI-ESM1-2-HR`, `NorESM2-MM`, `UKESM1-0-LL` | Driving GCM |
| `driving_experiment_id` | `historical`, `ssp126`, `ssp245`, `ssp370` | Historical (1960–2014); SSP1-2.6, SSP2-4.5 and SSP3-7.0 (2015–2100) |
| `driving_variant_label` | `r6i1p1f1`, `r1i1p1f1`, `r1i1p1f2` | See model ensemble table above |
| `source_id` | `CSI-WRF412R3`, `CSI-WRF412R5` | The two WRF RCM configurations |
| `version_realisation` | `v1-r1` | Version and realisation of the simulation |
| `freq` | `day`, `mon` | Daily or monthly output |
| `variable_id` | `tasmax`, `pr`, `hurs`, etc. | CF/CMIP variable name — see variable table above |
| `version` | `v20260127` | Data version date (YYYYMMDD); use `latest` symlink for most recent |

### Example full path

```
/g/data/kr82/CSI/output-CMIP6/DD/SWWA-04/DWER-MU/ACCESS-ESM1-5/ssp370/r6i1p1f1/CSI-WRF412R3/v1-r1/day/tasmax/v20260127/
```

### THREDDS access

Data can also be browsed and accessed without an NCI account via the THREDDS Data Server:

```
https://thredds.nci.org.au/thredds/catalog/kr82/CSI/output-CMIP6/DD/catalog.html
```

---

## Known Issues

Known issues with specific model runs or variables will be documented here as they are identified. Users are encouraged to check this section and the linked evaluation paper before applying CSI data.

If you encounter an issue, please open a [GitHub Issue](https://github.com/DWER-WA/CSI-Overview/issues) or contact the team using the details below.

---

## How to Cite

When using WA CSI data, projections, or materials in publications, reports, or analyses, please cite both the data and the evaluation paper:

**Data citation:**
> Government of Western Australia, Department of Water and Environmental Regulation. *Climate Science Initiative (CSI) WA Climate Projections*. https://doi.org/10.25914/3jys-sb70

**Evaluation paper:**
> Kala et al. (2026). Design and Evaluation of the Western Australian Climate Science Initiative (CSIv1.0) CMIP6 and ERA5 driven convection permitting regional climate model simulations for southwest Western Australia. *Geoscientific Model Development Discussions*. DOI: TBC.

Always check the NCI Data Catalogue record and associated factsheets for the most up-to-date citation and licensing notes.

---

## Licensing

CSI data and materials are made available under the **Creative Commons Attribution 4.0 International (CC BY 4.0)** licence:  
https://creativecommons.org/licenses/by/4.0/

**Conditions of use:** CSI projections are research products that have not been fully operationally evaluated. Users are advised to review the known issues, consult the evaluation paper, and undertake appropriate assessment of the data before use in downstream applications.

---

## Acknowledgement
CSI is supported by:
- The Climate Adaptation Fund of the Western Australian Government
- The Climate and Atmospheric Science Branch, Science, Economics and Insights Division Department of Climate Change, Energy, the Environment and Water, NSW Government (DCCEEW), New South Wales and Australian Regional Climate Modelling (NARCliM) team
- The Pawsey Supercomputing Research Centre, Western Australia
- Murdoch University, Perth, Western Australia

---
## How to Cite
When using WA CSI data, projections, or materials in publications, reports, or analyses, cite as follows:
 - Kala et al. (2026) Design and Evaluation of the Western Australian Climate Science Initiative (CSIv1.0) CMIP6 and ERA5 driven convection permitting regional climate model simulations for southwest Western Australia, Geoscientific Model Development Discussions, DOI: (TBC) 
 - Government of Western Australia, Department of Water and Environmental Regulation, Climate Science Initiative and WA climate projections. (http://doi.org/10.25914/3jys-sb70).

## Contact and Feedback

For questions about data use, access, or to provide feedback on the projections:

- Open a [GitHub Issue](https://github.com/DWER-WA/CSI-Overview/issues) for technical questions relating to this repository
- Contact **climatescience@dwer.wa.gov.au** for general enquiries about WA CSI
