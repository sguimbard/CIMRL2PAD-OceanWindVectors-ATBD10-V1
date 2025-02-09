# Algorithm Input and Output Data Definition (IODD)



### Input data

```{table} Input Data
:name: InpData
|Quantity                    | Description                      |  Sources      |        
| :-: | :-: | :-: |
|L1c TB at L-band |  L1B Brightness Temperatures at 1.4 GHz (V, H, 3$^{rd}$ Stokes, 4th Stokes)          | CIMR L1 ground segment   |
|L1c TB at C-band |  L1B Brightness Temperatures at 6.9 GHz (V, H, 3$^{rd}$ Stokes, 4th Stokes)          | CIMR L1 ground segment   |
|L1c TB at X-band |  L1B Brightness Temperatures at 10.65 GHz (V, H, 3$^{rd}$ Stokes, 4th Stokes)          | CIMR L1 ground segment   |
|L1c TB at Ku-band |  L1B Brightness Temperatures at 18.7 GHz (V, H, 3$^{rd}$ Stokes, 4th Stokes)          | CIMR L1 ground segment   |
|L1c TB at Ka-band |  L1B Brightness Temperatures at 36.5 GHz (V, H, 3$^{rd}$ Stokes, 4th Stokes)          | CIMR L1 ground segment   |
| Level-2b SST product | Sea Surface Temperature (optional) | CIMR L2 ground segment   |
| Level-2b SSS product | Sea Surface Salinity (optional) | CIMR L2 ground segment   |
| Level-2b SIC product | Sea Ice concentration (optional) | CIMR L2 ground segment   |
```



### Output data
```{table} Output Data
:name: OutData
|     name |  description |  Units | dimensions |
 | ---------| ---------------------| ---------------------|---------------------| 
 | time_LR     | seconds of observation since YYYY-MM-DD 00:00:00 UTC. | seconds | $[xdim_{grid}^{LR},ydim_{grid}^{LR}]$ |
 | lon_LR | Low Resolution longitude. range: $[0^{\circ}, 360^{\circ}]$ | degrees East | $[xdim_{grid}^{LR},ydim_{grid}^{LR}]$ |
 | lat_LR | Low Resolution latitude. range: $[90^{\circ}S, 90^{\circ}N]$ | degrees North | $[xdim_{grid}^{LR},ydim_{grid}^{LR}]$ |
 | time_MR     | seconds of observation since YYYY-MM-DD 00:00:00 UTC. | seconds | $[xdim_{grid},ydim_{grid}]$ |
 | lon_MR | Medium Resolution longitude. range: $[0^{\circ}, 360^{\circ}]$ | degrees East | $[xdim_{grid}^{MR},ydim_{grid}^{MR}]$ |
 | lat_MR | Medium Resolution latitude. range: $[90^{\circ}S, 90^{\circ}N]$ | degrees North | $[xdim_{grid}^{MR},ydim_{grid}^{MR}]$ |
 | sea_surface_wind_speed_LR | Low Resolution sea surface wind speed at 40 x 40 km | m/s | $[xdim_{grid}^{LR},ydim_{grid}^{LR}]$ |
 | sea_surface_wind_direction_LR | Low Resolution sea surface wind direction at 40 x 40 km | meteorological convention. $0^{\circ}$: wind coming out of N, +90$^{\circ}$ : wind coming out of E, etc. range: $[0^{\circ},+360^{\circ}]$. | $[look,xdim_{grid},ydim_{grid}]$ | latitude. range: $[90^{\circ}S, 90^{\circ}N]$ | degrees North | $[xdim_{grid}^{LR},ydim_{grid}^{LR}]$ |
 | sea_surface_wind_speed_LR uncertainty | Low Resolution sea surface wind speed uncertainty | m/s | $[xdim_{grid}^{LR},ydim_{grid}^{LR}]$ |
 | sea_surface_wind_speed_LR quality level | Flag indicating the quality level of the LR OWS retrieval | n/a | $[xdim_{grid}^{LR},ydim_{grid}^{LR}]$ |
 | sea_surface_wind_speed_MR | Medium Resolution sea surface wind speed at 10 x 10 km | m/s | $[xdim_{grid}^{MR},ydim_{grid}^{MR}]$ |
 | sea_surface_wind_direction_MR | Medium Resolution sea surface wind direction at 10 x 10 km | meteorological convention. $0^{\circ}$: wind coming out of N, +90$^{\circ}$ : wind coming out of E, etc. range: $[0^{\circ},+360^{\circ}]$. | $[look,xdim_{grid},ydim_{grid}]$ | latitude. range: $[90^{\circ}S, 90^{\circ}N]$ | degrees North | $[xdim_{grid}^{MR},ydim_{grid}^{MR}]$ |
  | sea_surface_wind_speed_MR uncertainty | Medium Resolution sea surface wind speed uncertainty | m/s | $[xdim_{grid}^{MR},ydim_{grid}^{MR}]$ |
 | sea_surface_wind_speed_MR quality level | Flag indicating the quality level of the MR OWS retrieval | n/a | $[xdim_{grid}^{MR},ydim_{grid}^{MR}]$ |
| sea_surface_wind_speed_AW | All weather sea surface wind speed at 10 x 10 km | m/s | $[xdim_{grid}^{MR},ydim_{grid}^{MR}]$ |
 | sea_surface_wind_direction_AW | All weather  sea surface wind direction at 10 x 10 km | meteorological convention. $0^{\circ}$: wind coming out of N, +90$^{\circ}$ : wind coming out of E, etc. range: $[0^{\circ},+360^{\circ}]$. | $[xdim_{grid}^{MR},ydim_{grid}^{MR}]$ |
 | sea_surface_wind_speed_AW uncertainty | All Weather sea surface wind speed uncertainty | m/s | $[xdim_{grid}^{MR},ydim_{grid}^{MR}]$ |
 | sea_surface_wind_speed_AW quality level | Flag indicating the quality level of the AW OWS retrieval | n/a | $[xdim_{grid}^{MR},ydim_{grid}^{MR}]$ |
 ```

### Auxiliary data

Auxiliary Data Required for Forward Model

```{table} Auxilliary Data
:name: AuxData
|Quantity                    | Required For                      |  Sources              |        
| :-: | :-: | :-: |
|sea surface salinity        | spec. emission                    | WOA, CMEMS, ISAS      |
|sea surface temperature     | spec. emission                    | CIMR, ECMWF           |
|surface pressure            | atmos. model                      | ECMWF,                |
|2-m temperature             | atmos. model                      | ECMWF,                |
|columnar vapor              | atmos. model                      | ECMWF,                |
|10-m NE wind speed          | glint, rough sfc. emission        | CIMR,ECMWF, Metop-SG|
|10-m wind direction         | rough sfc. emission               | CIMR,ECMWF, Metop-SG  |
|mispointing angles          | geometry initialization           | CIMR L1 ground segment   |
|best fit plane angles       | geometry initialization           | CIMR L1 ground segment    |
|time correlations           | EO-CFI initialization             | CIMR L1 ground segment|
|solar flux                  | TEC alt. correction, sun glint    |  RSGA files   |
|ORBSCT file                 | EO-CFI                            |  RSGA files   |
|wind GMF                    | wind speed inversion              | internal file        |
|LSC correction              | land sea contamination correction | internal file        |
| distance to nearsest coasts | LSC flagging                     | CIMR L1 ground segment |
```


### Ancillary data

Subsection text

