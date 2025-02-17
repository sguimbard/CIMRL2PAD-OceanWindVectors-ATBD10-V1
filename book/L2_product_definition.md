# Level-2 product definition

The Level-2b OWV product is obtained through application of the OWV retrieval algorithm, given the Level-1C TBs. The product is provided in non rainy conditions and surface wind speed less than 17 m/s for both low spatial 40 km x 40 km resolution ($xdim_{grid}^{LR},ydim_{grid}^{LR}$) and moderate spatial resolution (10 km x 10 km) grids ($xdim_{grid}^{MR},ydim_{grid}^{MR}$). There is also one OWV retrieval  for all weather conditions. The product is provided in netCDF format and contains the variables listed in {numref}`L2OWVdef`.

```{table} Level-2 OWV product definition
:name: L2OWVdef
|     name |  description |  Units | dimensions |
 | ---------| ---------------------| ---------------------|---------------------| 
 | time_LR     | seconds of observation since YYYY-MM-DD 00:00:00 UTC. | seconds | $[xdim_{grid}^{LR},ydim_{grid}^{LR}]$ |
 | lon_LR | Low Resolution longitude. range: $[0^{\circ}, 360^{\circ}]$ | degrees East | $[xdim_{grid}^{LR},ydim_{grid}^{LR}]$ |
 | lat_LR | Low Resolution latitude. range: $[90^{\circ}S, 90^{\circ}N]$ | degrees North | $[xdim_{grid}^{LR},ydim_{grid}^{LR}]$ |
 | time_MR     | seconds of observation since YYYY-MM-DD 00:00:00 UTC. | seconds | $[xdim_{grid},ydim_{grid}]$ |
 | lon_MR | Medium Resolution longitude. range: $[0^{\circ}, 360^{\circ}]$ | degrees East | $[xdim_{grid}^{MR},ydim_{grid}^{MR}]$ |
 | lat_MR | Medium Resolution latitude. range: $[90^{\circ}S, 90^{\circ}N]$ | degrees North | $[xdim_{grid}^{MR},ydim_{grid}^{MR}]$ |
 | sea_surface_wind_speed_LR | Low Resolution sea surface wind speed at 40 x 40 km | m/s | $[xdim_{grid}^{LR},ydim_{grid}^{LR}]$ |
 | sea_surface_wind_direction_LR | Low Resolution sea surface wind direction at 40 x 40 km | meteorological convention. $0^{\circ}$: wind coming out of N, +90$^{\circ}$ : wind coming out of E, etc. range: $[0^{\circ},+360^{\circ}]$. | $[xdim_{grid}^{LR},ydim_{grid}^{LR}]$ | latitude. range: $[90^{\circ}S, 90^{\circ}N]$ | degrees North | $[xdim_{grid}^{LR},ydim_{grid}^{LR}]$ |
 | sea_surface_wind_speed_LR uncertainty | Low Resolution sea surface wind speed uncertainty | m/s | $[xdim_{grid}^{LR},ydim_{grid}^{LR}]$ |
 | sea_surface_wind_speed_LR quality level | Flag indicating the quality level of the LR OWS retrieval | n/a | $[xdim_{grid}^{LR},ydim_{grid}^{LR}]$ |
 | sea_surface_wind_speed_MR | Medium Resolution sea surface wind speed at 10 x 10 km | m/s | $[xdim_{grid}^{MR},ydim_{grid}^{MR}]$ |
 | sea_surface_wind_direction_MR | Medium Resolution sea surface wind direction at 10 x 10 km | meteorological convention. $0^{\circ}$: wind coming out of N, +90$^{\circ}$ : wind coming out of E, etc. range: $[0^{\circ},+360^{\circ}]$. | $[xdim_{grid}^{MR},ydim_{grid}^{MR}]$ | latitude. range: $[90^{\circ}S, 90^{\circ}N]$ | degrees North | $[xdim_{grid}^{MR},ydim_{grid}^{MR}]$ |
  | sea_surface_wind_speed_MR uncertainty | Medium Resolution sea surface wind speed uncertainty | m/s | $[xdim_{grid}^{MR},ydim_{grid}^{MR}]$ |
 | sea_surface_wind_speed_MR quality level | Flag indicating the quality level of the MR OWS retrieval | n/a | $[xdim_{grid}^{MR},ydim_{grid}^{MR}]$ |
| sea_surface_wind_speed_AW | All weather sea surface wind speed at 10 x 10 km | m/s | $[xdim_{grid}^{MR},ydim_{grid}^{MR}]$ |
 | sea_surface_wind_direction_AW | All weather  sea surface wind direction at 10 x 10 km | meteorological convention. $0^{\circ}$: wind coming out of N, +90$^{\circ}$ : wind coming out of E, etc. range: $[0^{\circ},+360^{\circ}]$. | $[xdim_{grid}^{MR},ydim_{grid}^{MR}]$ |
 | sea_surface_wind_speed_AW uncertainty | All Weather sea surface wind speed uncertainty | m/s | $[xdim_{grid}^{MR},ydim_{grid}^{MR}]$ |
 | sea_surface_wind_speed_AW quality level | Flag indicating the quality level of the AW OWS retrieval | n/a | $[xdim_{grid}^{MR},ydim_{grid}^{MR}]$ |
 ```