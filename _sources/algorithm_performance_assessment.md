# Algorithm Performance Assessment using SCEPS

To assess the performance of the previously described OWV retrieval algorithm, we used the SCEPS prototype simulator to generate a very large test card (~6000 km × 4000 km), with 1 km resolution including strong SSS gradients due to the Amazon River plume, and strong surface wind speed gradients with the presence of two hurricanes ({numref}`Figure36`).

As described in RD.2, the simulator consists of a single statically-linked Linux executable program, **cimrProject**, which produces a Level 1b antenna temperature product from input scene brightness information. The program takes as input an EO-CFI orbit definition file (Team, 2022), a file containing the scene brightness temperature in the form of a *test card*, complete GRASP-generated antenna patterns provided by industry, and a file that specifies the sample times at which to produce antenna temperatures. 

The scene brightness includes both the isotropic and anisotropic complete modified Stokes vector ($T_h$, $T_p$, $U$, $V$) in the surface polarization basis. The isotropic part can vary with incidence angle, while, for practical reasons in our analyses, the anisotropic part is assumed to be independent of incidence angle.

```{figure} Figure35.png
--- 
name: Figure35
---
Schematic of the retrieval algorithm assessment using SCEPS.
```

A schematic of the overall retrieval algorithm assessment using SCEPS is provided in {numref}`Figure35`. The assessment is based upon these successive steps:

1. The scene is first described by geophysical fields, including: SSS, SST, OWV at ~1 km spatial resolution and then interpolated (in space and time) atmospheric vertical parameters from ERA5.

2. The TOA brightness temperatures are then evaluated for all CIMR frequencies and polarization using the previously described RTM for an ensemble of incidence angles. The azimuthal harmonic contributions to total TOA temperature are also evaluated separately.

3. The computation of (noisy) simulated CIMR antenna temperature from the scene brightness temperature field involves several aspects:
   - 3.1 Calculation of orbit and viewing geometry,
   - 3.2 Calculation of the scene brightness Stokes vector,
   - 3.3 Integration of the scene brightness over the antenna patterns (both near and far from the feed boresights) for each horn.
   - 3.4 Addition of NEDT noise to the antenna temperatures,
   - 3.5 Calculation and application of the Antenna Pattern Correction (APC) matrices for all feeds, to reduce/remove cross-pol contamination. For these tests, this APC has the polarization basis rotation *built-in*;
   - 3.6 Production of a preliminary version of the Level 1b product.

4. Resampled brightness temperature are then computed by applying the Backus-Gilbert method to express in the surface polarization basis:
   - SCEPS uses elliptical power patterns (on Earth) to compute the BG inner products.
   - Fore and aft sampled can be combined or kept separated in fore and aft images.
   - The Target grid is the original test card at 1 km resolution and the target patterns are all circular Gaussians with FWHM for L, C, X, Ku, and Ka band defined as follows: 60, 30, 30, 8, and 8 km.
   - A single application of BG yields weights that can be applied to all antenna pattern contributions.
   - Maps of error variance amplification factors are computed from the BG weights.

5. The noisy simulated resampled CIMR L1b antenna temperature from the scene brightness temperature field are then used for simulation of the future CIMR remapped *'measured L1B Tbs'*.

---

## Geophysical Data Used to Describe the Ocean Scene

The synthetic wind field used to model the scene is a merge between ERA5 re-analyses used as the background wind field, and more local and high-resolution surface winds from Sentinel-1/2 SAR data around two hurricanes. The SSS is from the MERCATOR model. The SST is from ERA5 re-analyses, which were also used to simulate the atmospheric vertical profiles. The test scene includes several coasts to analyze the land-contamination.

```{figure} Figure36.png
--- 
name: Figure36
---
Input geophysical data used to simulate the test card: (top left): SSS from Mercator; (top right): ERA5 SST and (bottom) merged ERA5 & SAR images (over the two hurricanes) surface wind vectors
```


## Simulated TOA Tbs over the Scene

Using these geophysical data as input, we generated TOA L- to Ka-band TOA Tbs using the previously described RTM at an ensemble of EIA with values of 0°, 20°, 40°, 50°, 55°, 60°, 70°, 80° including azimuthal harmonics for the full Stokes vector. Note: In the Forward Model simulations, we assumed the anisotropic roughness effects to be similar at all EIA values. ERA5 vertical profiles for Cloud Liquid, Ice Water Content, air temperature, humidity were used to evaluate the atmospheric contributions at each frequency. Land Tbs > 300K are from the SCEPS project (courtesy Carlos Jimenez). Example of such Tb fields are shown in {numref}`Figure37`.

```{figure} Figure37.png
--- 
name: Figure37
---
(Top Left) L-band H-pol; (Top right) L-band V-pol; (2nd panel from Top Left) C-band H-pol; (2nd panel from Top right) C-band V-pol; (3rd panel from Top Left) X-band H-pol; (3rd panel from Top right) X-band V-pol; (4th panel from Top Left) Ku-band H-pol; (4th panel from Top right) Ku-band V-pol; (Bottom panel, left) Ka-band H-pol; (Bottom panel, right) Ka-band H-pol; based on the Radiative forward model (EIA = 52° for L-band and EIA = 55° for X-Ka band).
```

As described in previous sections, the roughness-induced emission $\Delta T_p$ can be decomposed into isotropic and anisotropic emission components using a second-order azimuthal harmonic expansion as a function of $\tilde{\varphi}$, the relative azimuth between the radiometer look direction and the wind direction. 

The Stokes vector of the total brightness temperature emitted by the sea surface at location $(x_1, x_2)$ and at an EIA of $\theta_s$ thus reads:

$$
T_h(x_1, x_2, \theta_s) = T_{hso} + T_{ho}(U_{10}) + T_{hc1}(U_{10}) \cos(\tilde{\varphi}) + T_{hc2}(U_{10}) \cos(2\tilde{\varphi})
$$

$$
T_v(x_1, x_2, \theta_s) = T_{vso} + T_{vo}(U_{10}) + T_{vc1}(U_{10}) \cos(\tilde{\varphi}) + T_{vc2}(U_{10}) \cos(2\tilde{\varphi})
$$

$$
U(x_1, x_2, \theta_s) = U_{hs1}(U_{10}) \sin(\tilde{\varphi}) + U_{hs2}(U_{10}) \sin(2\tilde{\varphi})
$$

$$
V(x_1, x_2, \theta_s) = V_{hs1}(U_{10}) \sin(\tilde{\varphi}) + V_{hs2}(U_{10}) \sin(2\tilde{\varphi})
$$

---

As found, only the horizontal and vertical polarization exhibit isotropic contributions (0ᵗʰ order azimuthal harmonics), namely: $T_{ho}(U_{10})$ and $T_{vo}(U_{10})$. The amplitude of these isotropic components is significantly larger than the first-order azimuthal harmonics: $(T_{hc1}(U_{10}), T_{vc1}(U_{10}), U_{hs1}(U_{10}), V_{hs1}(U_{10}))$ and the second-order azimuthal harmonics: $(T_{hc2}(U_{10}), T_{vc2}(U_{10}), U_{hs2}(U_{10}), V_{hs2}(U_{10}))$. Note that the third $U$ and fourth $V$ Stokes vector components are non-zero only because of anisotropic features of the sea surface roughness.

For each frequency, SCEPS integrates the harmonic contributions (*see {numref}`Figure38`): 

$$
T_{hc1}(U_{10}), T_{vc1}(U_{10}), U_{hs1}(U_{10}), V_{hs1}(U_{10}), T_{hc2}(U_{10}), T_{vc2}(U_{10}), U_{hs2}(U_{10}), V_{hs2}(U_{10})
$$

to total antenna temperature separately and stores them in an extended L1B netCDF file.

```{figure} Figure38.png
--- 
name: Figure38
---
Example of the TOA scene azimuthal harmonics simulated from the surface wind field in {numref}`Figure36` for L-band, C-band, and X-band. For each frequency panels show ($T_h$, $T_v$, $U$, $V$).
```

Here, we specified wind direction-relative harmonics together with the wind direction at each grid point. Note that the harmonics other than 0 cannot vary with incidence angle and are provided as a single value at each horizontal grid point.

---

## Simulated Instrument Tbs Over the Scene

The computation of (noisy) simulated CIMR antenna temperature from the scene brightness temperature field then involves several aspects:

1. Calculation of orbit and viewing geometry, 
2. Calculation of the scene brightness Stokes vector for an ensemble of incidence angles, and of the wind-relative azimuthal harmonics components, 
3. Integration of the scene brightness over the antenna patterns (both near and far from the feed boresights), 
4. Addition of NEDT noise to the antenna temperatures, 
5. Calculation and application of the antenna pattern correction matrices for all feeds, 
6. Production of a preliminary version of the Level 1B product, 
7. Resampling of the TOA Tbs using Backus-Gilbert for all bands except at L-band for which a weighting average is applied, 
8. An OZA adjustment is then simply computed by interpolating the test card Tbs (without harmonics) to the reference and actual OZA for each sample/measurement using those values directly without integrating over the antenna pattern. Then, the resampler resamples the interpolated test card Tbs at the OZA values as well as the unadjusted antenna Tbs separately so as to keep track of the adjustment. The OZA correction is then applied after resampling as a simple addition of the resampled adjustment.

---

Details about each step of the SCEPS simulator can be found in [RD.2]. The simulator includes an orbit propagator to simulate the orbiting satellite positions in time and an antenna geometry routine to simulate the antenna scanning geometry and integrate the brightness fields over the antenna power patterns. 

Noting that most of the power originates near the feed boresight, the integration domain is divided into an inner and an outer domain. These domains are defined for each feed (see {numref}`Figure39`): The inner domain includes the boresight and extends out to an ellipse corresponding to an azimuthally averaged power 40 dB below the peak (at the feed boresight), where the azimuthal average is computed in the tilted direction cosine coordinate system. The outer domain covers the rest of the Front Half-Space (FHS) of antenna (containing boresight) in either the tilted or un-tilted coordinate system.

```{figure} Figure39.png
--- 
name: Figure39
---
Inner (left) and outer (right) integration grids in untilted director cosine (u, v) coordinates for L. Only the directivities down to -40 dB and -60 dB below the peak are shown for the inner and outer grids, respectively. The color indicates the antenna pattern power relative to peak.
```

The CIMR instrument consists of 25 feeds, with one at L-band, 4 at C/X bands, and 8 at Ku/Ka bands. {numref}`Figure40` shows the measurement (full integration time) footprints for a portion of three successive scans for the L-, C-band, X-band, and Ku-band horns. The figure illustrates the extent of overlap between successive footprints both along and across the scan near the swath center. Although overlap can be increased (at the expense of increased noise) along the scan by using individual samples, the across-scan overlap cannot be changed. To obtain a resolution consistent with the antenna pattern footprint size, distance between neighboring measurements should not exceed half the Half-Power Beam Width (by the Whittaker–Nyquist–Shannon sampling theorem).

As discussed in [RD.2], this condition is not satisfied across scan in L and Ku bands, but is satisfied in C and X bands. For Ku-band, there is no overlap in the half-power footprints across scan, which may be a limiting factor in the resolution of images obtained from resampled antenna temperatures.

The figure illustrates the extent of overlap between successive footprints both along and across scan near the swath center. Although overlap can be increased (at the expense of increased noise) along scan by using individual samples, the across-scan overlap cannot be changed.

```{figure} Figure40.png
--- 
name: Figure40
---
Projection of the L-band, C-band, X-band, and Ku-band feed half-power footprints and boresight locations onto the ground at two closely separated times for three successive scans.
```

---

In SCEPS, the total antenna temperature integral over all space is separated into several parts, with different integration methods for each:

- Inner domain: Extending from each feed boresight out to a circle (in tilted director cosine coordinates) corresponding to an isotropic directivity of -40 dB relative to the maximum at feed center (HBS).
- Outer domain: Extending from the boundary of the inner domain out to the Earth limb in the untilted frame (OUT).
- Contribution from distributed foreign sources: Cold sky and galactic radiation in nominal instrument pointing (sky).
- Contribution from localized sources: Bright spots in the test card scene (bs).
- Contribution from the direct sun and moon: Without reflection from the Earth.

---

In SCEPS, the default reflector rotation rate is set to the fixed value of 7.8 rpm (clockwise looking towards the instrument along the spin axis from behind the reflector), and the radiometer integration times are set to the values shown in {numref}`tablerecparam`. 

SCEPS can be configured to produce antenna temperatures for only the full measurements or for all samples. In the present simulation, there are five samples per measurement.

---

```{table} Receiver characteristics. Both the antenna temperature and the effective receiver noise temperature ($T_{rn}$) corresponding to the NEDT values are taken to be 150 K in SCEPS. There are five samples per measurement for all bands.
:name: tablerecparam
| Band Name | Number of Feeds | Center Frequency (GHz) | Maximum Bandwidth (MHz) | Sample Integration Time (ms) | Measurement NEDT at $T_a$ = $T_{rn}$ = 150 K |
|---------------|---------------------|----------------------------|-----------------------------|----------------------------------|------------------------------------------|
| L             | 1                   | 1.4135                     | 50.0                        | 11.12                            | 0.3                                      |
| C             | 4                   | 6.875                      | 825.0                       | 2.80                             | 0.2                                      |
| X             | 4                   | 10.65                      | 100.0                       | 2.74                             | 0.3                                      |
| Ku            | 8                   | 18.7                       | 200.0                       | 1.00                             | 0.4                                      |
| Ka            | 8                   | 36.5                       | 1000.0                      | 0.74                             | 0.7                                      |
```

---

The reflector rotation rate is sufficiently fast that the antenna patterns move substantially during the measurement integration times, and this must be accounted for when SCEPS is configured to compute antenna temperatures for the full measurements. To do so, SCEPS extends the antenna pattern integration to include integration over the integration time of the receiver.

---

The simulated noisy instrument $T_B$ are then resampled using Backus-Gilbert with a footprint of FWHM = 15 km for C- and X-band and FWHM = 8 km for Ku- and Ka-bands. For L-band, one uses a weighted average of the original scene $T_Bs$ based on a Gaussian window of FWHM = 30 km. Examples of simulated TOA brightness temperatures integrated over CIMR antenna patterns for Aft view of two successive ascending passes intercepting the scene are shown in {numref}`Figure41`.

---

Note that instrument measurements are simulated from scene $T_p$ using SCEPS with several options:

$\Rightarrow$ L1B TOA + NEDT (constant over the antenna pattern),

$\Rightarrow$ L1B TOA without NEDT.

$\Rightarrow$ L1B TOA integrated over inner antenna patterns (HBS): Boresight to -40 dB,

$\Rightarrow$ L1B TOA integrated over full antenna patterns (TOT): 0 dB to -60 dB,

$\Rightarrow$ L1B TOA $T_p$ are then remapped into L1C TOA $T_p$ using Backus-Gilbert interpolation (all frequencies except L-band) or using « gaussian weighted-average » for L-band (do not respect Nyquist sampling)

$\Rightarrow$ L1C TOA $T_p$ are then generated for both Aft and Fore views and for 2 ascending passes intercepting the scene.


```{figure} Figure41.png
--- 
name: Figure41
---
Simulated TOA brightness temperatures integrated over CIMR antenna patterns for Aft view of two successive ascending passes intercepting the scene (left) V-pol; (right) H-pol. From Top to bottom: L-band; C-band, X-band, Ku-band and Ka-band.
```

## Step 1: Ocean Surface Wind and SST Retrievals

The two-step OWV retrieval has been implemented and applied over the scene, following:

- **Step 1:** Retrieval of ocean surface wind speed modulus $U_{10}^{ret}$ (and of the SST $T_s^{ret}$) from the 16 input linearly polarized Tbs at resampled C-, X-, Ku-, and Ka-band channel data, namely $T_{th}^{TOA}$ and $T_{tv}^{TOA}$, for aft and fore views.

- **Step 2:** Retrieval of ocean surface wind direction from the 8 input C- and X-band channels 3rd and 4th Stokes parameters $U^{TOA}$ and $V^{TOA}$ for aft and fore views, as well as the surface wind speed $U_{10}^{ret}$ and SST $T_s^{ret}$ retrieved at the previous step.

---

To retrieve the surface wind speed vector modulus, we use a Bayesian inversion approach in which the posterior distribution of the retrieved wind speed, and of the SST: $\mathcal{p}$ is taken to be the product of the likelihood function $\mathcal{L}$ and prior distribution functions $P$ and $P'$ for wind speed and SST, respectively:

$$
\mathcal{p}(\tilde{u}_{10}|T_p; \tilde{T}_s|T_p, \sigma_u, u_{10p}, \phi_{wp}, \sigma_T, T_{sp}) = \mathcal{L}(\tilde{u}_{10}, \tilde{T}_s, T_p, \phi_{wp}) \cdot P(\tilde{u}_{10}|\sigma_u, u_{10p}) \cdot P'(\tilde{T}_s|\sigma_T, T_{sp}) \quad (Eq.R1)
$$

Where:

- $\mathcal{p}$ is the posterior distribution of the retrieved wind speed,
- $\mathcal{L}$ is a likelihood function,
- $T_p$ are the input CIMR TOA Tbs:

$$
T_p = [T_{h,C}^{TOA,fore}, T_{v,C}^{TOA,fore}, T_{h,C}^{TOA,aft}, T_{v,C}^{TOA,aft}, T_{h,X}^{TOA,fore}, T_{v,X}^{TOA,fore}, T_{h,X}^{TOA,aft}, T_{v,X}^{TOA,aft}, \ldots, T_{h,Ku}^{TOA,fore}, T_{v,Ku}^{TOA,fore}, T_{h,Ku}^{TOA,aft}, T_{v,Ku}^{TOA,aft}, T_{h,Ka}^{TOA,fore}, T_{v,Ka}^{TOA,fore}, T_{h,Ka}^{TOA,aft}, T_{v,Ka}^{TOA,aft}]
$$

- $P$ is the prior distribution of wind speed,
- $P'$ is the prior distribution of SST,
- $\sigma_u$ is the standard deviation of the prior wind speed,
- $\sigma_T$ is the standard deviation of the prior SST,
- $T_{sp}$ is the prior SST,
- $u_{10p}$ is the prior wind speed, and
- $\phi_{wp}$ is the prior wind direction.

---

We set here $P = P' = 1$, to give zero impacts of priors on the end retrievals. In addition, we further assumed that $u_{10p} = 7 \, m/s$, and $T_{sp} = 15^\circ C$ are constant and uniform for all the scene. 

The likelihood function $\mathcal{L}$ is computed using the previously described RTM, here represented by the geophysical model function $G$, and which can be evaluated using **(Eq.166)** and the input CIMR TOA Tbs $T_p$:

$$
\mathcal{L}(\tilde{u}_{10}, \tilde{T}_s, T_p, \phi_{wp}) = \prod_{i=1}^{n} \exp \left( -\frac{(T_p^i - G(\tilde{u}_{10}, \tilde{T}_s, \phi_{wp}))^2}{2\sigma_{p,i}^2} \right) \quad (Eq.R2)
$$

Where $\sigma_{p,i}$ is the standard deviation of the CIMR TOA Tbs. It can be first taken to be the respective NEDT of each channel and can be re-evaluated post-launch using a large collected Tb TOA dataset.

The nominal Bayesian wind speed and SST solution are then taken to be the Maximum Likelihood Estimate (mode of the posterior distribution), following:

$$
(U_{10}^{ret}, T_s^{ret}) = arg_{max(u_{10}, T_s)} \mathcal{p}(\tilde{u}_{10}|T_p; \tilde{T}_s|T_p, \sigma_u, u_{10p}, \phi_{wp}, \sigma_T, T_{sp}) \quad (Eq.R3)
$$


This non-linear problem is solved iteratively using a Levenberg-Marquardt (1963) algorithm to find the local maxima.

Examples of Ocean Surface wind $U_{10}^{ret}$ speed retrieved over the scene is shown in {numref}`Figure42`. In these retrieval simulations, the instrument Tbs were derived by integrating the scene over the full antenna patterns (HBS + outer patterns). **SCEPS** provides the option to add NEDT noise to the antenna temperatures: we perform retrieval simulations with and without NEDT.

---
```{figure} Figure42.png
--- 
name: Figure42
---
Retrieved Ocean wind speed modulus using aft-views with full antenna pattern integration and NEDT added to antenna temperatures. (Right) Retrieved Ocean wind speed modulus using fore-views with full antenna pattern integration and no NEDT added to antenna temperatures.
```

We next focus on comparing the input surface wind speed to the retrieved ones. 
Here, we consider only the most complete simulations combining aft and fore views (weighted average), adding NEDT on the antenna Tbs, and integrating over the full antenna patterns.

---
```{figure} Figure43.png
--- 
name: Figure43
---
Input surface wind speed; (Top right) retrieved surface wind speed combining both Aft and Fore views. (Bottom) Map of the differences between retrieved and input wind speed.
```


As illustrated in {numref}`Figure43`, the difference between the retrieved wind speed and the input wind speed ($\Delta WS$) exhibits around zero values in general except in two domains: 

- Along the coasts where the $\Delta WS$ shows high values greater than **1 m/s**.
- Around the eye of the hurricane, where **negative** $\Delta WS$ values are observed.

---
```{figure} Figure44.png
--- 
name: Figure44
---
Distribution of the $\Delta WS$ considering the full retrieval domain shown in **Figure 43**.
```

The distribution of $\Delta WS$ is shown in {numref}`Figure44` and reveals:

- A **high RMSD = 8.6 m/s**.
- A **skewed and biased mean retrieval** over the scene with **mean $\Delta WS$ = +2 m/s**, mainly because of the impact of land-contamination on the antenna Tbs.

To illustrate this point further (see {numref}`Figure45`), we **bin-averaged** the $\Delta WS$ as a function of the distance to the nearest coasts. 

- The **median bias** and **STD** are around **0** until the distance to the nearest coasts reaches a value below **~40 km** and increases as distance to coasts diminishes toward zero. 
- **Very near the coast**, the **median $\Delta WS$** reaches around **+30 m/s** and **STD($\Delta WS$) ~25 m/s**, which reveal a relatively **strong impact of land** on the Tbs.

Given that the **FWHM** for C- and X-band resampled Tbs is **~15 km**, the land-contamination is therefore coming from **emission from the outer domain** of the antenna patterns.


```{figure} Figure45.png
--- 
name: Figure45
---
Median (top) and STD (bottom) of the $\Delta WS$ evaluated per bins of distance to nearest coasts (bin width 5 km).
```

When filtering data with distance to nearest coasts less than or equal to **40 km** (see {numref}`Figure46`), the statistics of $\Delta WS$ evolve toward expected values with:

- **Median (and mean) $\Delta WS$ ~ 0 m/s** 
- **STD($\Delta WS$) ~ 0.1 m/s**

showing that most of the ‘bad-quality’ retrievals are found in the **40 km coastal band**.

---
```{figure} Figure46.png
--- 
name: Figure46
---
(Left) Map of the $\Delta WS$ after filtering the data with distance to nearest coasts less than or equal to 40 km. (Right) Distribution of the $\Delta WS$ considering the retrieval domain filtered for distance to nearest coasts less than or equal to 40 km.
```

Although the median and STD of the differences between the input and retrieved wind are strongly reduced after filtering the pixels within 40 km from the coasts, as seen in {numref}`Figure46`, $\Delta WS$ is still larger within a coastal band farther than 40 km, and locally, the error increases around the eye of the hurricane. This might come from:

1. Unresolved spatial structure in the veering winds around the eye, and/or
2. Uncertainties in the wind direction (here with a first guess assumed to be ERA5 wind direction), which would translate into errors in the anisotropic components of the modeled Tbs.

```{figure} Figure47.png
--- 
name: Figure47
---
(Top Left) input ERA5 SST; (Top right) retrieved SST combining both Aft and Fore views. (Bottom) Map of the differences between retrieved and input SSTs.
```

```{figure} Figure48.png
--- 
name: Figure48
---
Median (top) and STD (bottom) of the $\Delta SST$ evaluated per bins of distance to nearest coasts (bin width 5 km).
```


As illustrated in {numref}`Figure46` to {numref}`Figure49`, a similar pattern of high land-contamination is found in the retrieved SSTs within ~40 km from nearest coasts. After removing the data within that band, an overall unbiased retrieval is found with an RMSD of ~0.1°C with respect to the input data when combining both aft and fore views in the input data used for retrieval, as well as adding the proper NEDT to each used channel. Outside of the coastal band, as for the retrieved wind speed modulus, the largest errors in the retrieved SSTs are found in the hurricane center region.
While this error is obviously related to azimuthal-harmonic components (see {numref}`Figure38`), the exact source for that error (polarization mixing?) yet remains unidentified and would require further investigation.

```{figure} Figure49.png
--- 
name: Figure49
---
(Left) Map of the $\Delta SST$ after filtering the data with distance to nearest coasts less than or equal to 40 km. (Right) Distribution of the $\Delta SST$ considering the retrieval domain filtered for distance to nearest coasts less than or equal to 40 km.
```


## Step 2: Ocean Wind Direction Inversion Algorithm

In a second step, the algorithm aims at retrieving the wind direction, $\phi_{w}^{ret}$ only, using as input 8 datasets corresponding to C- and X-band channels 3rd and 4th Stokes parameters for both aft and fore views:

$$
T_p = [U_C^{TOA,fore}, V_C^{TOA,fore}, U_C^{TOA,aft}, V_C^{TOA,aft}, U_X^{TOA,fore}, V_X^{TOA,fore}, U_X^{TOA,aft}, V_X^{TOA,aft}]
$$

The algorithm also uses as input the surface wind speed $U_{10}^{ret}$ and temperature $T_s^{ret}$, retrieved from Step 1.

To retrieve the surface wind speed vector direction, we use a Bayesian inversion approach in which the posterior distribution of the retrieved wind direction $\tilde{\phi}_w$, denoted $\mathcal{P}'$, is taken to be the product of the likelihood function $\mathcal{L}'$ and prior distribution functions $P''$ for wind direction:

$$
\mathcal{P}'(\tilde{\phi}_w|T_p, \sigma_u, U_{10}^{ret}, T_s^{ret}, \sigma_T) = \mathcal{L}'(\tilde{\phi}_w, U_{10}^{ret}, T_s^{ret}, T_p, \phi_{wp}) \cdot P''(\tilde{\phi}_w|\phi_{wp}, U_{10}^{ret})
$$  (eqR4)

For the prior distribution of wind direction, we assumed a Gaussian distribution.

$$
P''(\tilde{\phi}_w|\phi_{wp}, U_{10}^{ret}) = \frac{1}{2\pi \sigma_{\phi}^2} \exp \left( -\frac{[\tilde{\phi}_w - \phi_{wp}]^2}{2\sigma_{\phi}^2} \right)
$$

Where the prior wind direction $\phi_{wp}$ is given by ERA5 and where we tested several values for the prior standard deviation of $\sigma_{\phi} = 20^\circ, 30^\circ, 40^\circ, 60^\circ$.


The likelihood function $\mathcal{L}'$ is computed using the RTM, here represented by the geophysical model function $G$ and which can be evaluated using (Eq.166) and the input SCEPS simulated CIMR TOA 3rd and 4th Stokes Tbs $T_p$:

$$
\mathcal{L}'(\tilde{\phi}_w, U_{10}^{ret}, T_s^{ret}, T_p, \phi_{wp}) = \prod_{i=1}^{n} \exp \left( -\frac{(T_{p,i} - G(\tilde{\phi}_w, U_{10}^{ret}, T_s^{ret}))^2}{2\sigma_{p,i}^2} \right)
$$

Where $\sigma_{p,i}$ is the standard deviation of the CIMR TOA 3rd and 4th Stokes parameters.

The nominal Bayesian wind direction solution is then taken to be the Maximum Likelihood Estimate (mode of the posterior distribution), following:

$$
\phi_w^{ret} = \arg \max_{\phi} \, \mathcal{P}'(\tilde{\phi}_w|T_p, \sigma_u, U_{10}^{ret}, T_s^{ret}, \sigma_T)
$$

We apply the conjugate gradient technique using a modified Levenberg-Marquardt (1963) algorithm to find the local maxima. The wind speed vector solution to this constrained minimization problem is the final L2B retrieval.

```{figure} Figure50.png
--- 
name: Figure50
---
Example of wind speed and direction retrievals (red arrows) and input ERA5 winds (green arrows) after full antenna pattern integration, NEDT added, combining Aft and Fore views, and assuming a standard deviation for the prior wind direction of 60°
```

Examples of wind speed and direction retrievals (as compared to the prior ERA5 wind direction), using as input the simulated instrument’s 3rd and 4th Stokes parameters after full antenna pattern integration, NEDT added, combining Aft and Fore views, and assuming a standard deviation for the prior wind direction of 60°, are shown in {numref}`Figure50` to {numref}`Figure52`.


```{figure} Figure51.png
--- 
name: Figure51
---
Zoom on the south-west located hurricane IRMA region. Same legend as in {numref}`Figure50`.
```

```{figure} Figure52.png
--- 
name: Figure52
---
Zoom on the coasts North of the Amazon River mouth. Same legend as in {numref}`Figure50`.
```

As shown, and expected, the quality of the wind direction retrieval strongly degrades in the near-coast region (distance to nearest coasts less than or equal to 40 km) and some larger errors are apparent at low winds. Maps of the input and retrieved wind direction, as well as their differences, are shown in {numref}`Figure53` and {numref}`Figure54` after filtering data at grid points where the distance to nearest coasts is less than or equal to 40 km.

While the retrieved wind direction is noisy, the retrieved wind direction patterns are in general very coherent with the input ones. As evidenced, larger uncertainties in the retrieved wind direction are observed:

1. For lower wind speeds (see {numref}`Figure54`, right panel), as expected given the small amplitudes (< 0.5 K) of the azimuthal harmonics of the 3rd and 4th Stokes parameters for $U_{10} < 5 \, m/s$ with respect to the antenna Tbs NEDT in C and X-bands (0.2 - 0.3 K).

2. Larger uncertainties are also observed in regions where the relative wind direction exhibits transitions around ±180°. This can be potentially attributed to larger ambiguities in the wind direction because U and V = 0 at all wind speeds and frequencies at such values of the relative azimuth angle (see for example Figure 27 to Figure 31).

```{figure} Figure53.png
--- 
name: Figure53
---
Maps of (Left) Input Wind Direction and (Right) Retrieved Wind Direction
```

After filtering for data at grid points where the distance to nearest coasts is less than or equal to 40 km and where the relative wind direction angle reaches ±180°, we found an RMSD between the input and retrieved wind direction of ~19° on average over the scene, increasing to 35° for conditions where $U_{10} < 5$ m/s.

```{figure} Figure54.png
--- 
name: Figure54
---
Maps of (Left) Differences $\Delta \phi$ between the input wind direction (ERA5 prior) and the retrieved wind direction. (Right) Retrieved Wind Speed
```

## Performance Assessment Summary

An initial performance assessment of the CIMR prototype Level-2 OWV retrieval algorithm was performed using a large-scale reference scenario (Test card scenes). We used the SCEPS prototype simulator to generate a very large tropical-to-mid latitude test card (~6000 km × 4000 km), with 1 km resolution including strong SSS gradients due to the Amazon River plume, and strong surface wind speed gradients with the presence of two hurricanes.

The computation of (noisy) simulated CIMR antenna temperature from the scene brightness temperature field involves:

- Calculation of orbit and viewing geometry,
- Calculation of the scene brightness Stokes vector for an ensemble of incidence angles,
- Calculation of the wind-relative azimuthal harmonics components,
- Integration of the scene brightness over the antenna patterns (both near and far from the feed boresights),
- Addition of NEDT noise to the antenna temperatures,
- Calculation and application of the antenna pattern correction matrices for all feeds,
- Resampling of the TOA Tbs using Backus-Gilbert for all bands except at L-band for which a weighting average is applied,
- Finally, an OZA correction is then applied after resampling.

The two-step OWV retrieval algorithm was then applied by minimizing the differences between simulated CIMR antenna Tbs and Tbs from the RTM model.

As found, the Ocean Wind Speed (and SST) retrievals exhibit an RMSD of ~0.1 m/s with zero bias with respect to the input OWVs as long as the data are acquired at a distance of at least more than 40 km from the nearest coasts.

The land-contamination is the first error source for these TOA Tbs resampled at the C- and X-band resolution (using a FWHM window of 15 km in the BG resampling):

- It is coming from earth emissivity contributions from both inner and outer antenna patterns.
- When filtering data with distance to nearest coasts greater than or equal to 40 km, the statistics of $ \Delta WS $ evolves toward expected values with a median (and mean) $ \Delta WS \sim 0$ m/s and STD$(\Delta WS) \sim 0.1$ m/s, showing that most of the ‘bad-quality’ retrievals are found in the 40 km coastal band.

Locally, retrieved SWS error is also found to increase around the eye of the hurricanes. This might come from:

- Unresolved spatial structure in the veering winds around the eye, and/or
- Uncertainties in the wind direction (here with a first guess assumed to be ERA5 wind direction), which would translate into errors in the anisotropic components of the modeled Tbs.

Similar patterns of high land-contamination are found in the retrieved SSTs within ~40 km from nearest coasts. After removing the data within that band:

- An overall unbiased SST retrieval is found with an RMSD of ~0.1°C with respect to the input data when combining both aft and fore views in the input TOA Tb data used for retrieval, as well as adding the proper NEDT to each used channel.

Outside of the coastal bands, as for the retrieved wind speed modulus, the largest errors in the retrieved SSTs are found in the hurricane center region. While this error is obviously related to azimuthal-harmonic components, the exact source for that error (polarization mixing?) yet remains unidentified and would require further investigation.

As found for OWV and SST, the quality of the wind direction retrieval strongly degrades in the near-coast region (distance to nearest coasts less than or equal to 40 km), and some larger errors are apparent at low winds. While the retrieved wind direction is noisy, the retrieved wind direction patterns are in general very coherent with the input ones.

As evidenced, larger uncertainties in the retrieved wind direction are observed:

1. For lower wind speed, as expected given the relatively small amplitudes ($<0.5$K) of the azimuthal harmonics of the third and fourth Stokes parameters for $ U_{10} < 5 $ m/s with respect to the antenna Tbs NEDT in C and X-bands (0.2–0.3 K).

2. Larger uncertainties are also observed in regions where the relative wind direction exhibits transitions around $ \pm 180^\circ $. This can be potentially attributed to larger ambiguities in the wind direction because $U$ and $V = 0$ at all wind speeds and frequencies at such value of the relative azimuth angle.

The combination of aft and fore views helps minimize such uncertainties, but they are not totally suppressed. After filtering for data at grid points where the distance to nearest coasts is less than or equal to 40 km and where the relative wind direction angle reaches $ \pm 180^\circ $, we found an RMSD between the input and retrieved wind direction of $ \sim 19^\circ $ on average over the scene, increasing to $35^\circ$ for conditions where $U_{10} < 5$ m/s.