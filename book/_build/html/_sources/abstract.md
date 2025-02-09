# Abstract


This document provides the theoretical basis for the CIMR Ocean surface Wind speed Vector (OWV) retrieval algorithm.

The inputs to the algorithm are the CIMR  Top of the Atmosphere (TOA) four Stokes parameter measurements at the five spectral bands, corresponding to frequencies of 1.4, 6.9, 10.65, 18.7, and 36.5 GHz. The input data also include a number of auxilliary products and pre-computed tables of forward model emission and geophysical data. 
The output is CIMR (10 meters above) Ocean Surface Wind Speed vector and shall include: 

|  | channels used (GHz) | 
| :-: | :-: | 
| Wind 40 km x 40 km  Low Resolution (LR) | 1.4 6.9 10.65 18.7 36.5 | 
| Wind Vector 10 km x 10 km Moderate Resolution (MR) | 6.9 10.65 18.7 36.5 | 
| Wind Vector 10 km x 10 km All weather (AW) | 1.4 6.9 10.65 18.7 36.5 | 

- **Wind LR** uses channels resampled to match the 1.4 GHz footprint (Low Frequency)

- **Wind MR** uses channels resampled to match the 10.65 GHz footprint (Medium Frequency).

- **Wind AW** is a blend of wind MR in no rain, and a statisical algorithm developed to retrieve wind through rain. 

Wind AW is rich with information about wind speeds in and around storms, including tropical cyclones and polar lows. This is the pre-launch version of the ATBD. Changes made postlaunch will be included as addenda and updated periodically. 

