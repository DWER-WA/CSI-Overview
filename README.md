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
| **Spatial domain** | Southwest Western Australia |
| **Horizontal resolution** | ~4 km (convection-permitting) |
| **Regional climate model** | WRF (Weather Research and Forecasting) |
| **Driving data** | CMIP6 GCMs|
| **Emissions scenarios** | SSP1-2.6 (low), SSP2-4.5 (medium) SSP3-7.0 (high) |
| **Historical period** | 1960–2014 (model) |
| **Future period** | 2015–2100 |
| **Output format** | NetCDF-4 |

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
| `cli` | 1 | Total Cloud Ice Area Fraction | `cloud_area_fraction` | ✓ | ✓ |
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

To access CSI data from NCI's Gadi or via the [ARE interface](https://opus.nci.org.au/display/Help/ARE+User+Guide), you must first apply for access to the relevant NCI project via [my.nci.org.au](https://my.nci.org.au). Browse available files via the NCI Data Catalogue linked above.

### Non-NCI Users

Data may be accessed via the NCI THREDDS Data Server — links are available from the NCI Data Catalogue record above.

---

## Data Analysis

Worked examples, notebooks, and analysis tools for working with CSI data are available in the companion repository:

**https://github.com/DWER-WA/CSI-DataAnalysis**

---

## Data Organisation

CSI data at NCI follows a hierarchical directory structure:

```
<project>/
└── <domain>/
    └── <institution_id>/
        └── <driving_source_id>/
            └── <driving_experiment_id>/
                └── <driving_variant_label>/
                    └── <source_id>/
                        └── <version_realisation>/
                            └── <freq>/
                                └── <variable_id>/
                                    └── <version>/
                                        └── <netcdf_filename>.nc
```

Where:
- `<driving_experiment_id>` is `historical`, `ssp126`, or `ssp370`
- `<freq>` is `day` or `mon` (daily or monthly)
- `<variable_id>` follows CF/CMIP conventions (e.g. `tasmax`, `pr`)

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
