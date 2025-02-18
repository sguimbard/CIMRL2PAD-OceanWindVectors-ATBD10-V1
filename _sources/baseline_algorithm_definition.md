# Baseline Algorithm Definition

## Contributions to CIMR Top of the Atmosphere brightness temperature

The present algorithm aims at retrieving the Ocean Wind Vector by finding the best-fit solution to minimize the difference between the CIMR L-, C-, X-, Ku-, Ka-band Top of the Atmosphere brightness temperature Stokes vector data and a forward radiative transfer model. 

```{figure} Figure8rev.png
---
name: Figure8
---
Major signals received by a Space borne microwave radiometer
```

As illustrated in {numref}`Figure8`, several geophysical parameters contribute significantly to $T_{B}$ measured by satellite sensors at antenna level (e.g., see {cite:p}`yueh2001error`; {cite:p}`Font2004`, {cite:p}`Reul2020`): these include sea surface salinity and temperature, sea surface roughness and foam, atmospheric water vapor, cloud liquid water, oxygen, ionospheric Total Electronic Content, sea surface scattered sky and sun radiations. To properly retrieve surface properties such as the ocean wind vector from the radiometer data, these contributions need to be accurately known and used in corrections of measured, or forward model simulations, of antenna $T_{B}$. 

They include:
* the direct and sea surface reflected/scattered solar and sky emission ({cite:p}`Wentz1978`;{cite:p}`LeVine2005a`; {cite:p}`Reul2007`; {cite:p}`Reul2008b`; {cite:p}`tenerelli2008earth`; {cite:p}`dinnat2008impact`), 
* the Faraday rotation in the ionosphere ({cite:p}`yueh2000estimates`; {cite:p}`le2002effect`; {cite:p}`Meissner2006`;{cite:p}`vergely2014new`),
* the impact of the atmosphere ({cite:p}`liebe1992atmospheric`; {cite:p}`skou2005band`; {cite:p}`wentz2016atmospheric`), 
* the effect of sea surface roughness on emissivity ({cite:p}`meissner2014emission`;{cite:p}`Yueh1999`;{cite:p}`meissner2012emissivity`;{cite:p}`meissner2018salinity`; {cite:p}`yin2016roughness`; {cite:p}`yueh2010passive`; {cite:p}`yueh2014aquarius`), and,
* the effect of the portion of the energy received due to land or sea ice in the CIMR antenna pattern when the main lobe is over water but close to land-sea or ice-sea transition (e.g., see {cite:p}`Reul2020`,{cite:p}`meissner2021SeaIce`)

The upwelling brightness temperatures above the atmosphere but below the ionosphere (before Faraday rotation) is referred hereafter to as the "Top of Atmosphere" brightness temperature and denoted $T_{tp}^{TOA}$ (with superscript "TOA") for upwelling signal in polarization $p$. Considering all components of the scene brightness temperature at all CIMR chanel frequencies, the complete model solution for $T_{tp}^{TOA}$, in the surface polarization basis, is:


$$
\left(\begin{matrix}
T_{th}^{TOA} \\ 
T_{tv}^{TOA} \\
U^{TOA} \\
V^{TOA}
\end{matrix}\right)=
\left(\begin{matrix}
T_{atm}^{up}+(\tau_d \tau_v \tau_w \tau_I \tau_R)[T_{surf,h}^{tot}+R_{surf,h}^{tot}\cdot T_{atm}^{dw}+T_{sch}+T_{ssh}] \\
T_{atm}^{up}+(\tau_d \tau_v \tau_w \tau_I \tau_R)[T_{surf,v}^{tot}+R_{surf,v}^{tot}\cdot T_{atm}^{dw}+T_{scv}+T_{ssv}] \\
(\tau_d \tau_v \tau_w \tau_I \tau_R) T_{erU} \\
(\tau_d \tau_v \tau_w \tau_I \tau_R ) T_{erV} \\
\end{matrix}\right)
$$ (eq1)

where the only contribution to the third and fourth Stokes parameters at Top of the Atmosphere and in the surface polarization basis comes from the rough surface emission components, and in which:

| Notation | Definition | 
| :-: | :-: |
| $T_{atm}^{up}$ | Unpolarized upwelling brightness temperature of atmospheric 1-way emission [K]|
|$\tau_d$ | 1-way atmospheric transmittance associated with molecular oxygen absorption [nd]|
|$\tau_v$|	1-way atmospheric transmittance associated with water vapor absorption [nd]|
|$\tau_w$|	1-way atmospheric transmittance associated with cloud water absorption [nd]|
|$\tau_I$|	1-way atmospheric transmittance associated with ice water absorption [nd]|
|$\tau_R$|	1-way atmospheric transmittance associated with rain absorption [nd]|
|$T_{surf,p}^{tot}$| p-pol brightness temperature of the total sea surface emission (specular+rough+foam) [K] |
|$R_{surf,p}^{tot}$|	reflectivity of the total sea surface (specular+rough+foam) in p-pol|
| $T_{atm}^{dw}$ | Unpolarized downwelling brightness temperature of atmospheric 1-way emission [K]|
|$T_{erU}$|	Third Stokes brightness temperature of rough surface emission (surface pol. Basis) [K]|
|$T_{erV}$|	Fourth Stokes brightness temperature of rough surface emission (surface pol. Basis) [K]|
|$T_{scp}$|	p-pol brightness temperature of scattered celestial sky radiation (surface pol. Basis) [K]|
|$T_{ssp}$|	p-pol brightness temperature of scattered solar radiation (sunglint) (surface pol. Basis) [K]|

The brightness temperature of the total sea surface emission, $T_{surf,p}^{tot}$ can be decomposed as follows:

$$
T_{surf,p}^{tot}=T_s\cdot e_{surf,p}^{tot}=T_s\cdot\left[(1-F_f)\cdot(e_{sp}+e_{rp})+F_f\cdot e_{foam,p}\right]=T_s\cdot(e_{esp}+\Delta e_{rp})
$$ (eq2)

where:

| Notation | Definition | 
| :-: | :-: |
|$T_s$|	Sea Surface Temperature [K]|
|$e_{surf,p}^{tot}$| p (h or v)-pol total sea surface emission (specular+rough+foam)|
|$F_f$|	Fractionnal area of sea surface covered by foam |
|$e_{sp}$|	p-pol specular emission (surface pol. Basis)|
|$\Delta e_{rp}$|	p-pol rough surface emission (surface pol. Basis)|
|$e_{foam,p}$| p-pol foam-covered surface emission (surface pol. Basis)|

and where we split the total sea surface brightness temperature $T_{surf,p}^{tot}$ into three components: 

* the brightness temperature from the perfectly flat sea surface ($T_{sp}=T_s\cdot e_{sp}$), 
* the brightness temperature contrast induced by the rough and foamy sea surface ($T_{rp}=T_s\cdot\Delta e_{rp}$). 

Note that the total surface reflectivity is related to the total surface emissivity by $R_{surf,p}^{tot}=1-e_{surf,p}^{tot}$.

Considering all components of the scene brightness temperature, the complete model solution for the upwelling brightness temperatures above the atmosphere but below the ionosphere (before Faraday rotation) in the surface polarization basis, is, therefore in p-polarization:

$$
T_{tp}^{TOA}=T_{atm}^{up}+(\tau_d \tau_v \tau_w \tau_I \tau_R)[T_s\cdot[e_{sp}+\Delta e_{rp}]+R_{surf,p}^{tot} \cdot T_{atm}^{dw}+T_{scp}+T_{ssp}]
$$ (eq3)


## Level-2 end to end algorithm functional flow diagram


```{figure} SketchL1BtoL1C.png
--- 
name: SketchL1BtoL1C
---
Level-1B to Level-1C $T_B$ algorithm functional flow diagram. 

```

The inputs to the L2B OVW algorithm are the Level 1C $T_B$ at the five CIMR frequencies, in H-, V-, 3rd, and, 4th Stokes for the fore and aft views. As summarized in {numref}`SketchL1BtoL1C`, we assume here that the $T_B$s data are corrected for antenna spill-over and emissivity, sky and sun direct and earth reflected/scattered radiation,Faraday rotation across the ionosphere, and that they are provided with a proper rotation of the Stokes parameter from the antenna polarization basis to the surface polarization basis (L1B processor). In fine, we will use as input the Leve1b data after proper resampling (so-called Level1c).

It is understood that the corrections for (1) the sky and sun direct and earth reflected/scattered radiation, (2) the model for the rotation of the Stokes parameter due to Faraday rotation across the ionosphere and polarisation basis changes, as well as (3) the L1B resampling approach all shall be applied through the Level 1 algorithms and not in the present L2B OWV algorithm. 

In addition, it is not clear at which level (1) or (2) the land- and ice-ocean transitions effects shall be corrected for on the $T_b$s (so called land sea contammination). Given that these effects require antenna-pattern related information, it shall better be applied in the Level 1 algorithms.

Other input data are the CIMR L2B SST and SSS products, properly resampled on the C- and X-band acquisitions.


```{figure} SketchL1CtoL2OWV.png
--- 
name: Sketch1
---
Level-2 OWV end to end algorithm functional flow diagram. Here $SST^p$, $SSS^p$, $U_{10}^p$, and $\Phi_w^p$ are *a priori values* for the SST, SSS, 10 meter height surface wind speed and direction, respectively. 

```


The principle of the proposed OWV retrieval algorithms rely on a forward radiative transfer modelling of the top of the atmosphere brightness $T_{tp}^{TOA}$ from first guess geophysical values (SSS, SST, $U_{10}$, etc...),and, the retrieval of the surface wind speed and direction (OWV) from a minimization of the differences between the observed and modelled $T_{tp}^{TOA}$. The Level-2 end to end algorithm functional flow diagram is shown in {numref}`Sketch1`. The radiative transfer forward model which is needed is based on the following components:

- a sea-water dielectric constant model valid from 1.4 GHz to 36.5 GHz,
- a perfectly flat, or specular, sea surface emission model,
- a surface roughness and foam-induced correction model valid from 1.4 GHz to 36.5 GHz,
- a Radiative Transfer Model for Atmospheric corrections valid from 1.4 GHz to 36.5 GHz,
- a scattering model to correct for sea surface scattered Solar and celestial radiation, particularly at L-band, and, 
- a correction for geometric rotation from surface polarization basis to antenna polarization basis,
- a model to correct for Faraday rotation in the ionosphere.

We review the first four parts of the forward model components and corrections that belong to the Level 2 algoirthm in the following subsections.

## Models for the Dielectric Constant of seawater 

### Mathematical Description at 1.4 Ghz
 
The {cite:p}`zhou2021seawater`'s Debye model for the seawater dielectric constant is used in the present algorithm for the L-band channels (1.4 GHz), will be refered to as "GW2020", and can be expressed by:

$$
ε_{sw}(f, S, T)=\displaystyle ε_{\infty}+\frac{(ε_{s-dw}(T)R_{sw-dw}(S,T)-ε_{\infty})}{1+i \omega \tau(T)}-i\frac{\sigma(f,S,T)}{\omega ε_0}
$$ (eqdiel1)

where $f$ is the electromagnetic frequency ([Hz]), $T$ and $S$ are the temperature ([degree celsius]) and salinity ([pss]) of seawater, respectively; $ε_0$ is the dielectric constant of free space; $ε_{s-dw}(T)$ is the static dielectric constant of distilled water, given by:

$$
ε_{s-dw}(T)=88.0516-4.01796\times10^{-1}\cdot T-5.1027\times10^{-5}\cdot T^2+2.55892\times10^{-5}\cdot T^3
$$ (eqdiel2)

and $\tau(T)$ is the relaxation time of distilled water:

$$
\tau(T)=1.75030\times10^{-11}-6.12993\times10^{-13}\cdot T +1.24504\times10^{-14}\cdot T^2-1.14927\times10^{-16}\cdot T^3
$$ (eqdiel3)

$R_{sw-dw}(S,T)$ is an additional factor in the static dielectric constant of seawater due to the presence of ions, given by: 

$$
R_{sw-dw}(S,T)=\displaystyle 1-S\cdot ( 3.97185\times10^{-3}-2.49205\times10^{-5}\cdot T-4.27558\times10^{-5}\cdot S +3.92825\times10^{-7}\cdot S\cdot T+4.15350\times10^{-7}\cdot S^2)
$$ (eqdiel4)

Note that $\sigma(f,S,T)$ needs to be nulled at $S=0$ since the conductivity of distilled water is close to 0. The expression of 
$\sigma(f,S,T)$ given in {cite:p}`zhou2021seawater` is:

$$
\sigma(f,S,T)=\sigma(f,S,0)\cdot R_{\sigma}(f,S,T)
$$ (eqdiel5)

where for f=1.4 GHz,

$$
\sigma(f,S,0)=9.50470\times10^{-2}\cdot S -4.30858\times10^{-4}\cdot S^2+2.16182\times10^{-6}\cdot S^3
$$ (eqdiel6)

and

$$R_{\sigma}(f,S,T)=1+T\cdot(3.76017\times10^{-2} + 6.32830\times10^{-5}\cdot T +4.83420\times10^{-7}\cdot T^2 − 3.97484\times10^{-4}\cdot S+6.26522\times10^{-6}\cdot S^2)
$$ (eqdiel7)

### Mathematical Description at f=6.9, 10.65, 18.7, and 36.5 GHz

The model function developed by {cite:p}`meissner2004complex` (denoted MW hereafter) fits the dielectric constant data to a double Debye relaxation polynomial that performs best at higher frequencies. The seawater dielectric data were obtained by inverting $T_B$ measurements from the Special Sensor Microwave Imager (SSM/I) at frequencies higher than 19 GHz; measurements from {cite:p}`ho1974measurements` were used to derive the model at the lower frequencies. The MW model function was recently updated by providing small adjustments to the Debye parameters based on including results for the C-band and X-band channels of WindSat and AMSR ({cite:p}`meissner2012emissivity`;{cite:p}`meissner2014emission`). The MW model is used in the WindSat, AMSR-E, AMSR2 wind speed retrieval algorithms ({cite:p}`meissner2012emissivity`), and in the Aquarius and SMAP SSS retrieval algorithms ({cite:p}`meissner2018salinity`).

The model for $ε_{sw}(f, S, T)$, the dielectric constant of water, depends on the radiation frequency $f$, the water temperature $T$ and the salinity $S$ of the sample.

The dielectric constant model $ε_{pw}$ for pure water is used to derive the vertically integrated liquid cloud water absorption and for salty water in the surface emission Forward model. Following {cite:p}`meissner2014emission`, the dielectric constant of water is fitted using a double relaxation law. The general form reads:


$$
 \varepsilon_{sw}(f, S, T)= \displaystyle\frac{\varepsilon_{S}(T,S)-\varepsilon_{1}(T,S)}{1+i f/\nu_1(T,S)}+\displaystyle\frac{\varepsilon_{1}(T,S)-\varepsilon_{\infty}(T,S)}{1+i f/\nu_2(T,S)}+\varepsilon_{\infty}(T,S)-i\frac{\sigma(T,S)}{(2\pi\epsilon_o)f}
$$ (eqdiel8)
 
where:
 
- $i=\sqrt{(-1)}$, 
- $f$ is the radiation frequency [in GHz],
-	the temperature $T$ is in °C and the salinity $S$ in pss
-	$\varepsilon_S(T,S)$ is the static (zero frequency) dielectric constant
-	$\varepsilon_{\infty}(T,S)$ is the dielectric constant at infinite frequencies
-	$\varepsilon_1(T,S)$ is the intermediate frequency dielectric constant.
-	$\nu_1(T,S)$ and $\nu_2(T,S)$ are the first and second Debye relaxation frequencies [in GHz], respectively
-	$\sigma(T,S)$ is the conductivity of water in [S/m]
-	$\epsilon_o$=8.854 $\cdot 10^{(-12)}$ [F/m] is the vacuum electric permittivity

#### Dielectric Constant of Pure Water

In this subsection, we will consider pure water where $S$=0 and $\sigma(T,S=0)$=0. The dielectric constant for pure water then reads:

$$
\varepsilon_{pw}(f,S=0,T)= \displaystyle\frac{\varepsilon_{S}(T,S=0)-\varepsilon_{1}(T,S=0)}{1+i f/\nu_1(T,S=0)}+\displaystyle\frac{\varepsilon_{1}(T,S=0)-\varepsilon_{\infty}(T,S=0)}{1+i f/\nu_2(T,S=0)}+\varepsilon_{\infty}(T,S=0)
$$ (eqdiel9)
 
The static dielectric constant for pure water $\varepsilon_{S}(T,S=0)$ is given by:
 
$$
 \varepsilon_{S}(T,S=0)=\displaystyle\frac{3.70886\cdot 10^4-8.2168\cdot 10^1 T}{4.21854\cdot10^2+T}
$$ (eqdiel10)
 
For the temperature dependence of the 4 fit parameters $\varepsilon_{1}$, $\varepsilon_{\infty}$, $\nu_1$ and $\nu_2$, we use: 

$$
\varepsilon_{S}(T,S=0)=\displaystyle a_o+a_1 T+a_2 T^2
$$ (eqdiel11)
 
$$
\nu_{1}(T,S=0)=\displaystyle\frac{45+T}{a_3+a_4 T+a_5 T^2}
$$ (eqdiel12)
 
$$
\varepsilon_{\infty}(T,S=0)=\displaystyle a_6+a_7 T
$$ (eqdiel13)
 
$$
\nu_{2}(T,S=0)=\displaystyle\frac{45+T}{a_8+a_9 T+a_{10} T^2}
$$ (eqdiel14)
 
The $a_i$ parameters for the fits are given by (Table III in {cite:p}`meissner2014emission`):
 
 | Coefficient | Value |
 | :-: | :-: |
 | $a_o$ |5.723 |  
 | $a_1$ | 2.2379 $\cdot 10^{-2}$ |
 | $a_2$ |-7.1237 $\cdot 10^{-4}$ |
 | $a_3$ |5.0478 |
 | $a_4$ |-7.0315 $\cdot 10^{-2}$|
 | $a_5$ |6.0059 $\cdot\ 10^{-4}$|
 | $a_6$ |3.6143|
 | $a_7$ |2.8841 $\cdot 10^{-2}$|
 | $a_8$ |1.3652 $\cdot 10^{-1}$|
 | $a_9$ |1.4825 $\cdot 10^{-3}$|
 | $a_{10}$ |2.4166 $\cdot 10^{-4}$|
 
#### Dielectric Constant of Sea Water at f=6.9, 10.65, 18.7, and 36.5 GHz
 
For sea water, a model for the conductivity of sea water $\sigma(T,S)$ is needed:
 
$$
\sigma(T,S)=\sigma(T,S=35)\cdot R_{15} (S)\cdot\displaystyle\frac{R_{\tau}(S)}{R_{15}(S)}
$$ (eqdiel15)

Where with the units: $T$ [°C], $S$ [pss], and $\sigma$ [S/m]:

$$
\sigma(T,S=35)=2.903602+8.607\cdot 10^{-2}\cdot T+4.738817\cdot 10^{-2}\cdot T^2- 2.991\cdot 10^{-6}\cdot T^3+4.3047\cdot 10^{-9}\cdot T^4
$$ (eqdiel16)

$$
R_{15}(S)=S\cdot\displaystyle\frac{(37.5109+5.45216\cdot S+1.4409\cdot 10^{-2}\cdot S^2)}{(1004.75+182.283\cdot S+S^2)}
$$ (eqdiel17)
 
$$
\displaystyle\frac{R_{\tau}(S)}{R_{15}(S)}=1+\displaystyle\frac{\alpha_o(S)(T-15)}{(\alpha_1(S)+T)}
$$ (eqdiel18)
 
where:
 
$$
\alpha_o(S)=\frac{(6.9431+3.2841\cdot S-9.9486\cdot 10^{-2}\cdot S^2)}{(84.850+69.024\cdot S+S^2)}
$$ (eqdiel20)
 
 
$$
\alpha_1(S)=49.843-0.2276\cdot S+0.198\cdot 10^{-2}\cdot S^2
$$ (eqdiel21)
 
For the remaining five subfunctions in the seawater dielectric constant model of [Equation 13](eqdiel8), we use the following expressions:
 
 
$$
\varepsilon_S (T,S)=\varepsilon_S(T,S=0)\cdot \exp{[b_o S+b_1 S^2+b_2 TS]}
$$ (eqdiel22)
 
$$
\nu_1 (T,S)=\nu_1 (T,S=0)\cdot [1+S\cdot (d_o+d_1 T+d_2 T^2+d_3 T^3+d_4 T^4)]
$$ (eqdiel23)
 
$$
\varepsilon_1 (T,S)=\varepsilon_1(T,S=0)\cdot \exp{[b_6 S+b_7 S^2+b_8 TS]}
$$ (eqdiel24)
 
$$
\nu_2 (T,S)=\nu_2 (T,S=0)\cdot [1+S\cdot (b_9+b_{10} T)]
$$ (eqdiel25)
 
$$
\varepsilon_{\infty} (T,S)=\varepsilon_{\infty} (T,S=0)\cdot [1+S\cdot (b_{11}+b_{12} T)]
$$ (eqdiel26)
 
We followed the changed made in {cite:p}`meissner2012emissivity`, with respect {cite:p}`meissner2004complex` algorithm with the parameters of the fits given by:

 
 | Coefficient | Value |
 | :-: | :-: |
 | $b_o$ |-3.3333 $\cdot 10^{-3}$|
 | $b_1$ | 4.74868 $\cdot 10^{-6}$ |
 | $b_2$ | 0 |
 | $b_6$ |-6.28908 $\cdot 10^{-3}$|
 | $b_7$ |1.76032 $\cdot 10^{-4}$|
 | $b_8$ |-9.22144 $\cdot 10^{-5}$|
 | $b_9$ |-1.99723 $\cdot 10^{-2}$|
 | $b_{10}$ |1.81176 $\cdot 10^{-4}$|
 | $b_{11}$ |-2.04265 $\cdot 10^{-3}$|
 | $b_{12}$ |1.57883 $\cdot 10^{-4}$|
 | $d_o$ |0.23232 $\cdot 10^{-2}$|
 | $d_1$ |-0.79208 $\cdot 10^{-4}$ |
 | $d_2$ | 0.36764 $\cdot 10^{-5}$|
 | $d_3$ |0.35594 $\cdot 10^{-6}$|
 | $d_4$ |0.89795 $\cdot 10^{-8}$|
 
 
 
### Functionnal flow diagram

```{figure} FFD_dielec.png
--- 
name: FFD_dielec
---
Dielectric Constant model Flow Diagram. Input data are Temperature $T$ [°C], salinity $S$ [pss], and, radiometer electromagnetic frequency $f$ [Hz]. Output are the real and imaginary parts of $ε_{sw}(f, S, T)$ at frequencies $f$=1.4, 6.9, 10.7, 18.7 and 36.5 GHz.
```


## Perfectly flat or 'specular' sea surface emission


```{figure} Flat_Sea_Rad.png
--- 
name: Flat_Sea_Rad
---
Front view of the PALS radiometer instrument measuring the brightness temperature emitted by a perfectly flat surface of a saltwater pond. L-band radiometric measurements were made over a salinity range between 25 and 40 pss and a temperature range of 8.5°C to 32°C (from {cite:p}`Wilson2004`). 
```


### Mathematical Description

The dependence of the microwave brigthness temperature emitted by the sea surface $T_{B}$ on SSS is contained in the emissivity, $e$: $T_{B} = T \times e$, where $\it{T}$ is the sea surface temperature. The emissivity $e$ is a quantity that depends on physical and chemical properties of the water (e.g. salinity and temperature),observational conditions (incidence angle, electromagnetic frequency, polarization), as well as on the sea surface roughness. 

For a perfectly flat ocean surface the scattered electric and magnetic fields may be expressed in terms of the incident fields. The reflected electric field components $(E_{h}^{'},E_{v}^{'})$ are related to the incident components $(E_{h},E_{v})$ by the diagonal matrix equation:

$$
\begin{pmatrix}
E_{h}^{'}(\theta_s,\phi_s) \\ 
E_{v}^{'}(\theta_s,\phi_s)
\end{pmatrix}=
\begin{pmatrix}
R_{hh}^{(0)} & 0 \\ 
0 & R_{vv}^{(0)}  
\end{pmatrix}
\begin{pmatrix}
E_{h}(\theta_s,\phi_s-180°) \\ 
E_{v}(\theta_s,\phi_s-180°)
\end{pmatrix}
$$	(eq14)

where $(\theta_s,\phi_s)$ is the specular reflection direction for radiation incident from direction $(\theta_s,\phi_s-180°$). The superscripts on the reflection coefficients indicate that they correpond to zero order expansion in surface slope, i.e., the flat surface reflection. The flat surface reflection coefficients on the preceeding matrix are given by the Fresnel equations:

$$
R_{hh}^{(0)} (S,T_s,\theta_s)=\displaystyle\frac{\cos\theta_s-\sqrt{ε_{sw}(S,T_s)-\sin^2⁡\theta}}{\cos\theta_s+\sqrt{ε_{sw}(S,T_s)-\sin^2⁡θ_s}}
$$ (eq15)

$$
R_{vv}^{(0)} (S,T_s,\theta_s)=\displaystyle\frac{ε_{sw}(S,T_s) \cos\theta_s-\sqrt{ε_{sw}(S,T_s)-\sin^2⁡{\theta_s}}}{ε_{sw}(S,T_s) \cos{\theta_s}+\sqrt{ε_{sw}(S,T_s)-\sin^2{\theta_s}}}
$$ (eq16) 

where $ε_{sw}( S, T_s)$ is the dielectric constant of seawater which is a function of the surface salinity $S$ in practical salinity units (psu) and the temperature $T_s$ in kelvin. The Fresnel reflection matrix equation is:

$$
T'=
\begin{pmatrix}
T_{h}^{'} \\ 
T_{v}^{'} \\
U^{'} \\
V^{'}
\end{pmatrix}=M^{(0)}T=
\begin{pmatrix}
|R_{hh}^{(0)}|^2 \delta^2 & 0 & 0 & 0 \\ 
0 & |R_{vv}^{(0)}|^2 \delta^2 & 0 & 0 \\
0 & 0 & \Re (R_{hh}^{(0)}(R_{vv}^{(0)})^{\ast})  & \Im{(R_{hh}^{(0)}(R_{vv}^{(0)})^{\ast})} \\
0 & 0 & -\Im (R_{hh}^{(0)}(R_{vv}^{(0)})^{\ast}) & \Re{(R_{hh}^{(0)}(R_{vv}^{(0)})^{\ast})}
\end{pmatrix}
\begin{pmatrix}
T_{h} \\ 
T_{v} \\
U \\
V
\end{pmatrix}
$$ (eq17)

where $\delta$ is the Kroneker delta, $\Re$ and $\Im$ are the real and imaginary part, respectively. For a perfectly flat ocean surface with salinity, $\it{S}$, temperature, $\it{T_s}$, and observed at incidence angle $\theta$, the emissivity at polarization, $\it{p}$ (horizontal or vertical), and electromagnetic frequency, $f$, (note that we quote the center of a microwave frequency bandwidth associated with a given radiometer) is given by {cite:t}`peake1959interaction`:

$$
e_{sp}^{(0)} (f,S,T_s,\theta_s)=1-|R_{pp}^{(0)} (ε_{sw},\theta_s)|^2
$$ (eq18)

where $R_{pp}^{(0)}$ is the Fresnel reflection coefficient given above in [Equation](#eq15) and [Equation](#eq16). The specular brightness temperature emitted by the sea surface in horizontal polarization is then

$$
T_{esh} (S,T_s,\theta_s)=T_{esh} (ε_{sw}(S,T_s),T_s,\theta_s)=T_{s}\cdot e_{sh,f}^{(0)}(S,T_s,\theta_s)=T_{s}\cdot[1-|R_{hh}^{(0)} (ε_{sw},\theta_s)|^2]
$$ (eq19)

and in vertical polarization:

$$
T_{esv} (S,T_s,\theta_s)=T_{esv} (ε_{sw}(S,T_s),T_s,\theta_s)=T_{s}\cdot e_{sv,f}^{(0)}(S,T_s,\theta_s)=T_{s}\cdot[1-|R_{vv}^{(0)} (ε_{sw},\theta_s)|^2]
$$ (eq20)

where $e_{sp,f}^{(0)}$ is the specular emissivity at polarization $p$ and frequency $f$.

### Functionnal flow diagram


```{figure} FFD_fresnel.png
--- 
name: FFD_flatsea
---
Specular Sea Surface Emission model Flow Diagram. Input data are the real and imaginary parts of the sea water dielectric constant $ε_{sw}$, the radiometer incidence angle $\theta_s$ and the sea surface temperature $T$. Output data are the specular brightness temperature $T_{esv}^{(0)}$ and $T_{esh}^{(0)}$ in vertical and horizontal polarisation, respectively.
```


## Rough sea surface emission

### Physics of the problem 

At a given microwave frequency *f*, the total surface emissivity at polarization $p$, $E_{p,f}$ can be modeled with a specular part $e_{sp}^{(0)}$ and a part caused by ocean roughness $\Delta e_{rp}^{rough}$:

$$
E_{p,f}^{surf}(T_s,S,f,p,\theta_s,\phi_s,U_{10},\phi_w)=e_{sp}^{(0)}(\theta_s,S,T_s,f)+\Delta e_{rp}^{rough}(\theta_s,S,T_s,f,U_{10},\phi_r,\phi_w)
$$ (eq:rough1)

where the emission change caused by ocean roughness $\Delta e_{rp}^{rough}$ is a function of the radiometer frequency $f$, incidence angle $\theta_s$ and azimuth $\phi_r$, the surface temperature $T_s$, salinity $S$, 10-meter height wind speed $U_{10}$, and the downwind direction $\phi_w$. Here the linearly polarized electric field components normal to the propagation direction, $E_h$ and $E_v$, are defined with respect to polarization basis vectors at the target given by ${\bf\hat{h}}$ and ${\bf\hat{v}}$. These basis vectors, in turn, are defined such that the surface emission propagation direction unit vector ${\bf\hat{k}}={\bf\hat{v}}\times{\bf\hat{h}}$. Under this *forward scattering alignment* (FSA) polarization basis convention,the relative azimuth angle $\phi_s$ that appears in the rough surface emission contribution is defined as $\phi_s=\phi_r - \phi_w$, which is the difference between the radiometer azimuth $\phi_r$ (measured counterclockwise from due east and from the perspective of an observer looking towards the radiometer from the target) and the downwind direction (towards which the wind is blowing, positive counterclockwise from due east). In the literature, azimuthal harmonics are typically presented as a function of $\phi_w - \tilde\phi_r$ where $\tilde\phi_r=\phi_r + 180^\circ$ is the radiometer look direction, although frequently the convention is not clearly stated.

Wind-induced surface waves are the primary contributor to ocean surface roughness, with internal waves, wind-current interactions, and ship wakes to be important but secondary contributors ({cite:p}`Gasiewski1994`). Wind-induced waves can be divided into two primary scales ({cite:p}`yueh1997`): 

1. The **large-scale waves** cause the local surface incidence angle to differ from the effective earth incidence
angle, and mix vertical and horizontal polarizations ({cite:p}`Gasiewski1994`), and,
 
2. The **small-scale gravity-capillary** waves riding on top the large-scale gravity waves ({cite:p}`john:zhang99`): the small-scale waves modify the specular surface reflection (or emission) through the bistatic scattering of the radiation incident upon the ocean surface. 

In addition, although **foam generated by breaking waves and wind streaks** typically covers only a few percent of the sea surface, it has a profound effect on the average microwave brightness of the ocean surface ({cite:p}`droppleman1970`). For surface wind speeds greater than 15 m/s, foam-induced effects may provide as much as half of the total sea surface signature to an orbiting microwave radiometer ({cite:p}`https://doi.org/10.1029/96JC03760`), due to its near-blackbody behavior. As wind speed increases, ocean foam coverage also increases, resulting in a large discrepancy between forward model (e.g., two-scale) emissivity calculations made with and without consideration of foam coverage. The quasi-blackbody models used for both foam emissivity and coverage are in themselves of limited accuracy due to the paucity of in situ observations for both foam coverage and emissivity that have been able to be made in conjunction with brightness temperatures from passive microwave instruments

Different mechanisms responsible for the rough sea surface emissivity in the microwave domain exhibit several anisotropic features, which, in turn, lead to a **wind directional dependence** of the observed brightness temperatures. 
The probability density function of the sea surface slope is skewed in the along wind axis and has a larger along wind variance than crosswind variance ({cite:p}`Cox1954`). Furthermore, the RMS height of the small gravity-capillary waves, which are riding on top of the large gravity waves, exhibits a noticeable anisotropy. The gravity-capillary waves traveling in the along-wind direction have larger amplitudes than those traveling in the crosswind direction ({cite:p}`Mitsuyasu1982`). Both effects cause an up-crosswind asymmetry of the emitted radiation. In addition, up-downwind asymmetries occur. The gravity-capillary waves and sea foam are not uniformly distributed over the underlying structure of large-scale waves. Aircraft radiometer measurements ({cite:p}`4579491`) show that the forward plunging side of a breaking wave is emitting warmer microwave emissions than its backside. Furthermore, the small-scale gravity-capillary waves have the tendency to cluster on the downwind side of the large-scale gravity waves ({cite:p}`Cox1958`; {cite:p}`Keller1975`). Finally, several studies of nonlinear wave-wave interaction suggest that the small-scale ocean surface waves are not propagating in the wind direction ({cite:p}`Banner1990`;{cite:p}`Hwang2000`; {cite:p}`Irisov2000`). This might be an additional source of error in the wind direction retrieval from radiometer data. 
 
It has been empirically observed that the first and second Stokes parameters of the roughness correction are even functions of the relative azimuth angle $\phi_s=\phi_r-\phi_w$ in the FSA convention, while the third and fourth Stokes parameters are odd functions of this angle. Typically, the total surface induced brightness temperature is therefore decomposed into azimuthal harmonics of the relative wind direction $\phi_s$, as follows: 

$$
\begin{equation}
\left(
\begin{matrix}
E_{h,f}^{surf}\\
E_{v,f}^{surf}\\
E_U^{surf}\\
E_V^{surf}\\
\end{matrix}
\right)=
\left(
\begin{matrix}
e_{sh,f}^{(0)}+\Delta e_{h,f}^{(0)} +\Delta e_{h,f}^{(1)} \cos \phi_s+ \Delta e_{h,f}^{(2)} \cos 2\phi_s\\
e_{sv,f}^{(0)}+\Delta e_{v,f}^{(0)} +\Delta e_{v,f}^{(1)} \cos \phi_s +\Delta e_{v,f}^{(2)} \cos 2\phi_s\\
\Delta U_{f}^{(1)} \sin \phi_s+\Delta U_{f}^{(2)} \sin 2\phi_s\\
\Delta V_{f}^{(1)} \sin \phi_s+\Delta V_{f}^{(2)} \sin 2\phi_s\\
\end{matrix}
\right).
\end{equation}
$$ (eq:rough2)

For natural wind-driven ocean surfaces, the zeroth-harmonic components exist only for vertical ($e_{sv,f}^{(0)}+\Delta e_{v,f}^{(0)}$) and horizontal ($e_{sh,f}^{(0)}+\Delta e_{h,f}^{(0)}$) polarizations. Upwind and downwind asymmetry features are accounted for in the first-harmonic components ($\Delta e_{h,f}^{(1)}$, $\Delta e_{v,f}^{(1)}$, $\Delta U_{f}^{(1)}$, and $\Delta V_{f}^{(1)}$), and the second-harmonic components ($\Delta e_{h,f}^{(2)}$, $\Delta e_{v,f}^{(2)}$, $\Delta U_{f}^{(2)}$, and $\Delta V_{f}^{(2)}$) account for the upwind-crosswind anisotropy. Such symmetry is expected for reflection-symmetric ocean surfaces although it is not physically guaranteed for all ocean surfaces. Nonetheless, this nominal symmetry allows expansion of the four Stokes components in either cosine or sine Fourier series in the azimuth angle. Truncating these series at the second-azimuthal-harmonic captures virtually all of the currently observable azimuthal brightness behavior. In the present algorithm, we rely on well established empirical Geophysical Model Functions (GMF) for the harmonics coefficients at each of the 5 CIMR frequencies and associated polarization and incidence angles. 


### Wind-induced isotropic emissivity

For the 6.9, 10.65, 18.7, and 36.5 GHz CIMR frequencies, we rely on {cite:p}`meissner2012emissivity`'s Geophysical Model Functions (GMF) for $\Delta e_{p,f}^{(0)}(\theta_s,U_{10},T_s,S)$, derived from AMSR-E, WindSat, and, SSM/I data at these frequencies. The Aquarius V5’s GMF ({cite:p}`meissner2018salinity`) are used here for modelling the L-band $\Delta e_{p,f}^{(0)}(\theta_s,U_{10},T_s,S)$.
Note that the {cite:p}`meissner2012emissivity`’s GMFs for C- to Ka-bands are provided at a reference incidence angle of $\theta_{ref}$=55.2°, and the Aquarius L-band GMFs are provided at $\theta_{ref}$=29.36°, 38.44°, and 46.29°. As discussed in {cite:p}`meissner2012emissivity`, the wind induced emissivity $\Delta e_{p,f}^{(0)}(\theta_s,U_{10},T_s,S)$ has a small residual SST dependence and the GMFs are also provided for a reference SST of $T_{ref}$=20°C. The wind induced emissivity is however slightly larger in cold water than in warm water, and to correct for this effect, {cite:p}`meissner2012emissivity` used the following model:

$$
\Delta e_{rp,f}^{(0)}(\theta_{ref},U_{10},T_S,S)=\delta_{ref}^{p,f}(U_{10})\cdot\displaystyle\frac{e_{sp,f}^{(0)}(\theta_{ref},T_S,S)}{e_{sp,f}^{(0)}(\theta_{ref},T_{ref},S)}
$$ (eq:rough5)

where the second multiplicative term is the ratio of the specular sea emission at SST=$T_s$ to the specular sea emission at SST=$T_{ref}$ = 20°C (Eq. [Equation](#eq19) and [Equation](#eq20)), and $\delta_{ref}^{p,f}(U_{10},\theta_s)$ is the wind-speed induced isotropic emissivity for 10-meter height surface wind speed ($U_{10}$), polarization $p$, frequency $f$, at reference EIA $\theta_{ref}$ and at the reference SST $T_{ref}$=20°C, and, is fitted by the fifth-order polynomial:

$$
\delta_{ref}^{p,f}(U_{10})=\displaystyle\sum_{k=1}^5 \delta_{k}^{p,f}\cdot U_{10}^k
$$ (eq:rough6)

where the $\delta_{k}^{p,f}$ coefficients are given in {numref}`table3` for each CIMR frequency and polarization for $\theta_{ref}$ = 55° (C-to Ka bands) and $\theta_{ref}$= 52° (L-band). Note that we linearly-extrapolated the Aquarius L-band GMFs provided at $\theta_s$=29.36°, 38.44°, and 46.29° to derive the L-band coefficients $\delta_{k}^{p,f}$ at $\theta_{ref}$= 52°.

```{table} Coefficients $\delta_{k}^{p,f}$ of [Equation](eq:rough6) for each CIMR frequency and dual polarization for $\theta_{ref}$=52° (L-band) and $\theta_{ref}$=55° (C- to Ka bands).
:name: table3
 | f [GHz] | p | 1 | 2 | 3 | 4 | 5 |
 | :-: | :-: |:-: |:-: |:-: |:-: |:-: |
 |1.4 | v| 1.6097e-3   |  -2.6751e-4 |  2.4483e-5 | -8.6502e-7 | 1.0749e-8 |
 |1.4 | h| 4.3588e-3 | -5.8672e-4 | 4.3997e-5   | -1.4223e-6 |1.6548e-8 |
 |6.8 | v| 4.96726e-5 | -3.03363e-4 | 5.6050506e-5 | -2.86408e-6 | 4.88803e-8 |
 |6.8 | h| 3.85750e-3 | -5.10844e-4 | 4.89469e-5   | -1.50552e-6 | 1.200306e-8|
 |10.7 | v| -2.35464e-4 | -2.76866e-4 | 5.73583e-5 | -2.94364e-6 | 4.89421e-8 |
 |10.7 | h| 4.17650e-3 | -6.20751e-4 |  6.82607e-5 | -2.47982e-6 | 2.80155e-8 |
 |18.7 | v| 3.26502e-5 | -3.65935e-4 | 6.62807e-5 | -3.40705e-6 | 5.81231e-8 |
 |18.7 | h| 5.06330e-3 | -7.41324e-4 | 8.54446e-5 | -3.28225e-6 | 4.01950e-8 |
 |36.5 | v| -0.00068348 | -0.00022172 | 4.0782e-05 | -1.8903e-06 | 2.8515e-08 |
 |36.5 | h| 0.0056226 | -0.00084095 | 0.00010615 | -4.5762e-06 | 6.6006e-08 |
```

Note that for the mutliple horns at the 6.9, 10.65, 18.7, and 36.5 GHz CIMR frequencies, the earth incidence angle $\theta_s$ is varying from 54.6° to 56.2° depending on the horn, and at L-band it is centered on 52°. To account for small $\theta_s$ variation from $\theta_{ref}$ one can proceed as follows. At nadir, both $\Delta e_{rh,f}^{(0)}(\theta_s=0)$ and $\Delta e_{rv,f}^{(0)}(\theta_s=0)$ have the same value $\Delta e_{f}^{(nad,0)}$. The results from {cite:p}`hollinger1971passive` and {cite:p}`4072619` suggest that $\Delta e_{f}^{(nad,0)}$ is approximately given by the arithmetic average of the v-pol and h-pol values at around $\theta_{ref}=$55°:


$$
\Delta e_{f}^{(nad,0)}(U_{10},T_S,S)\simeq\displaystyle\frac{1}{2}\left[\Delta e_{rv,f}^{(0)}(\theta_{ref},U_{10},T_S,S)+\Delta e_{rh,f}^{(0)}(\theta_{ref},U_{10},T_S,S)\right]
$$ (eq:rough3)

The EIA dependence of $\Delta e_{p,f}^{(0)}$ can then be parameterized by a low/high order polynomial in $\theta_s$ for h-pol/v-pol:

$$
\Delta e_{rp,f}^{(0)}(\theta_s,U_{10},T_S,S)=\displaystyle\Delta e_{f}^{(nad,0)}(U_{10},T_S,S)+\left[\Delta e_{p,f}^{(0)}(\theta_{ref},U_{10},T_S,S)-\Delta e_{f}^{(nad,0)}(U_{10},T_S,S)\right]\cdot\left(\frac{\theta_s}{\theta_{ref}}\right)^{x_p}
$$ (eq:rough4)

For the exponents $x_p$, p = v, h: $x_v$ = 4.0 and $x_h$ = 1.5 at all C- to Ka-band CIMR frequencies and wind speeds. The form [Equation](eq:rough4) applies for $\theta_s\leq\theta_{ref}$ .Following {cite:p}`meissner2012emissivity`, we linearly extrapolate the $\theta_s$-dependence for $\theta_s\geq \theta_{ref}$.

 

```{figure} allband_CIMR_isotropic_GMF.png
---
name: allband_CIMR_isotropic_GMF
---
Isotropic wind induced emissivity at L, C, X, Ku and Ka-band for (a) H-polarization and (b) V-polarization. The GMF are for the CIMR L-band horn nominal incidence angle of $\theta_{ref}$=51.95° and the C,X,Ku and Ka -band at $\theta_{ref}$=55.2°.

```

As illustrated in {numref}`allband_CIMR_isotropic_GMF`, the proposed GMFs reveal a systematically higher impact of the wind-induced roughness on the H-pol than V-pol emissivity at all frequencies. In H-pol, the impact of wind-induced roughness on the isotropic emissivity is increasing with increasing radiometer frequency. Contrarily, at V-pol, the L-band $\Delta e_{v,f}^{(0)}$ is higher than at the higher CIMR frequencies for 10-m height wind speed $\le$ 12 m/s. In this wind sped regimes, the increasing wind speed increases the brightness temperature at L-band, while for the C-, X-, Ku- and Ka -bands and for 10-m height wind speed $\le$ 6-7 m/s, the increasing wind speed decreases the brightness temperature. This behaviour is consistent with in situ and aircraft measurements at such angle and frequencies ({cite:p}`Hollinger1970`,{cite:p}`hollinger1971passive`,{cite:p}`Camps2004`, {cite:p}`Martin2014`), as well as, with the prediction of two-scale emissivity models ({cite:p}`Dinnat2002`,{cite:p}`yin2016roughness`,{cite:p}`Kilic2019`,{cite:p}`MA2021112661`). This behaviour is due to resonance in the scattering functions, occurring at wavelengths larger than 3$\lambda_o$ (where $\lambda_o$ is the electromagnetic wavelength) for high incidence angles ({cite:p}`john:zhang99`).
 
### Wind-induced anisotropic emissivity
 
We now turn to the model function $\Delta e_{p=v,h,U,V,f}^{(i=1,2)}$ for the four Stokes parameters of the wind direction signal for L- to Ka- bands entering in [Equation](eq:rough2). The GMFs for the anisotropic components are described in {cite:p}`meissner2012emissivity`, at $\theta_{ref}$=55.2° for the C- to Ka-band and in {cite:p}`meissner2018salinity` at $\theta_{ref}$=29.36°, 38.44°, and
46.29° for the L-band. They are given by:

$$
\Delta e_{p,f}^{(i=1,2)}(\theta_{ref},U_{10})=\sum_{k=1}^5 \alpha_{i,k}^{p,f}\cdot U_{10}^k
$$ (eq:rough7)
 
where the $\alpha_{i,k}^{p,f}$ coefficients are given in {numref}`table4`, for i=1 and {numref}`table5`, for i=2. They are directly provided at $\theta_{ref}$=55.2° for the C- to Ka-band in {cite:p}`meissner2012emissivity`. We linearly extrapolated the lower incidence Aquarius L-band GMFs functions to estimate the $\alpha_{i,k}^{p,f}$ coefficients at 1.4 GHz and $\theta_{ref}$=52°.

Note that only data from spaceborne fully-polarimetric radiometers operating at L-, X-, Ku- and Ka -bands are today available to characterize the third and fouth stokes parameters as a function of wind speed. To our knowledge, no spaceborne data based GMFs were derived for the third and fouth Stokes parameter at C-band ({cite:p}`meissner2012emissivity`): CIMR shall be the first spaceborne radiometer to measure third Stokes at C-band. To estimate the 3rd and 4th Stokes parameters GMF at C-band, we therefore bi-linearly interpolated the $\Delta e_{p,f}^{(i=1,2)}$ functions at 6.9 GHz from the GMFs at L-, X-, Ku- and Ka -bands. As well, the GMFs from {cite:p}`meissner2012emissivity` are provided at Ka-band at 37 GHz while CIMR Ka-band chanels center frequency is 36.5 GHz: we also linearly interpolated the GMF functions to derive them at the 36.5 GHz CIMR's central frequency.
 
```{figure} HVpol_allband_CIMR_anisotropic_1_GMF.png
---
name: HVpol_allband_CIMR_anisotropic_1_GMF
---
GMF of the first azimuthal harmonic coefficients $\Delta e_{p,f}^{(1)}(U_{10},\theta_{ref})$ as a function of surface wind speed at L, C, X, Ku and Ka-band for (a) V-polarization, (b) H-polarization, (c) Third Stokes parameter and (d) fourth Stokes parameter. The GMF are for the L-band reference incidence angle of $\theta_{ref}$=46.3° and the C, X, Ku, and Ka -band are at $\theta_{ref}$=55.2°.

```

As shown in {numref}`HVpol_allband_CIMR_anisotropic_1_GMF`, the amplitude of the first harmonic coefficients ($\Delta e_{v,f}^{(1)}$, $\Delta e_{h,f}^{(1)}$, $\Delta U_{f}^{(1)}$, $\Delta V_{f}^{(1)}$), characterizing the upwind–downwind asymmetry of the excess surface emissivity, is small for low winds and it increases with increasing wind speed. The relative polarization behavior is consistent between frequency observations at L-, X-, Ku-, and Ka-bands ({cite:p}`Yueh1999`,{cite:p}`Piepmeier2001`,{cite:p}`yueh2006`): there is larger first harmonic amplitude for vertical polarization than for horizontal polarization at all frequencies. The first harmonic amplitude is also in general significantly higher than the second harmonic amplitude ($\Delta e_{v,f}^{(2)}$, $\Delta e_{h,f}^{(2)}$, $\Delta U_{f}^{(2)}$, $\Delta V_{f}^{(2)}$), which represents the upwind–crosswind asymmetry of the excess surface emissivity (see {numref}`HVpol_allband_CIMR_anisotropic_2_GMF`). 

```{figure} HVpol_allband_CIMR_anisotropic_2_GMF.png
---
name: HVpol_allband_CIMR_anisotropic_2_GMF
---
GMF of the second azimuthal harmonic coefficients $\Delta e_{p,f}^{(2)}(U_{10},\theta_{ref})$ as a function of surface wind speed at L, C, X, Ku and Ka-band for (a) V-polarization, (b) H-polarization, (c) Third Stokes parameter and (d) fourth Stokes parameter. The GMF are for the L-band reference incidence angle of $\theta_{ref}$=46.8° and the C, X, Ku, and Ka -band are at $\theta_{ref}$=55.2°.
```

The relative polarization behavior is consistent with the characteristics of high-frequency observations. At a wind speed of 20 m/s, the peak‐to‐peak change of $\Delta e_{v,f}^{(1)}(U_{10})$ in vertical-polarization is about 2.5 K at Ka-band and 0.5 K at L-band. At the same wind speed in horizontal polarization, the peak‐to‐peak change of $\Delta e_{h,f}^{(1)}(U_{10})$ decreases to about ~1 K at Ka-band and ~0.1 K at L-band. The peak-to-peak change of the second harmonic $\Delta e_{v,f}^{(2)}(U_{10})$ in vertical-polarization is ~0.5 K at Ka-band and ~0.3 K at L-band. In horizontal-polarization, $\Delta e_{h,f}^{(2)}(U_{10})$ peak-to-peak change is about 1.5 K at Ka-band and 0.25 K at L-band.

```{table} Coefficients $\alpha_{1,k}^{p,f}, k=1,...,5, p=h,v,U,V $ of the first azimuthal harmonic coefficients in [Equation](eq:rough7) for the L-, C-, X-, Ku- and Ka-bands at a reference SST of 290K at reference incidence angle $\theta_{ref}$=46.9° (L-band) and $\theta_{ref}$=55.2° (C-, X-, Ku- and Ka bands).
:name: table4
 | f [GHz] | p | 1 | 2 | 3 | 4 | 5 |
 | :-: | :-: |:-: |:-: |:-: |:-: |:-: |
 |1.4 | v| 9.1197181e-03|-3.0431623e-03 | 5.083957e-04| -2.037598e-05| 2.458082e-07| 
 |1.4 | h|9.6160121e-03 | -4.3505334e-03| 6.07180e-04|-2.753646e-05 | 4.073317e-07 | 
 |1.4 | U| 2.1437e-05 | 1.84e11e-06 | -1.044e-06 | 4.3478e-08 | -5.3051e-10 | 
 |1.4 | V| -1.3375e-05 |5.3239e-06 | -6.5753e-07 |4.2225e-08 | -8.0259e-10| 
 |6.8 | v| 4.466633e-07 | 3.34314e-07 | 3.12587e-06 | -1.99336e-07 | 3.55175e-09 |
 |6.8 | h| 2.17314E-05 |	-1.54052E-06	| 7.43743E-07	| -3.32899E-08	| 3.04367E-10|
 |6.8 | U| -4.1435e-05 |	3.241e-05	| -7.3226e-06	| 4.2224e-07	| -7.7643e-09|
 |6.8 | V| -5.4651e-06 |2.1754e-06 |-2.6867e-07 |1.7253e-08 |-3.2794e-10 | 
 |10.7 | v| 4.96132E-05	|-2.90991E-05 | 9.05913E-06| -5.73703E-07| 1.10332E-08| 
 |10.7 | h|-2.20699E-05 |8.92180E-06 | 4.69873E-08| -2.41047E-08| 5.71120E-10|
 |10.7 | U| -8.48737E-05|5.35295E-05 | -1.16605E-05| 6.83923E-07|-1.27622E-08 | 
 |10.7 | V| 0.00000E+00|0.00000E+00 |0.00000E+00 |0.00000E+00 |0.00000E+00 | 
 |18.7 | v| -4.88686E-05| -2.6779E-06| 9.94735E-06| -7.51560E-07|1.55400E-08 | 
 |18.7 | h| 3.95872E-05 | -2.88339E-05 | 6.61597E-06| -4.08181E-07 |7.87906E-09 | 
 |18.7 | U| -3.29350E-05| 4.32977E-05 | -1.33822E-05 | 8.75024E-07 | -1.74093E-08 | 
 |18.7 | V| 0.00000E+00|0.00000E+00 |0.00000E+00 |0.00000E+00 |0.00000E+00 | 
 |36.5 | v| -0.00023591|7.4506e-05| 3.8283e-06 | -5.6458e-07|1.3619e-08 | 
 |36.5 | h| -5.178e-05| 2.1035e-05| 1.3162e-06 |-1.6558e-07 |3.7184e-09 | 
 |36.5 | U| 2.4803E-04| -9.8294E-05| 2.6171E-06| 9.0522E-08|-3.2364E-09 | 
 |36.5 | V| 0.00000E+00|0.00000E+00 |0.00000E+00 |0.00000E+00 |0.00000E+00 | 
```

```{table} Coefficients $\alpha_{2,k}^{p,f}, k=1,...,5, p=h,v,U,V $ of the second azimuthal harmonic coefficients in [Equation](eq:rough7) for the L-, C-, X-, Ku- and Ka-bands at a reference SST of 290K at reference incidence angle $\theta_{ref}$=4.95° (L-band) and $\theta_{ref}$=55.2° (C-, X-, Ku- and Ka bands).
:name: table5
 | f [GHz] | p | 1 | 2 | 3 | 4 | 5 |
 | :-: | :-: |:-: |:-: |:-: |:-: |:-: |
 |1.4 | v|  9.3408423E-02 |-3.3492931E-02	| 3.802560E-03	| -1.6925890E-04	| 2.6396519E-06 |
 |1.4 | h| -5.197487E-03 | 1.0855313E-02	| -1.84117E-03	| 9.571413E-05	| -1.605944E-06 | 
 |1.4 | U| -6.5015E-05 | 4.6888E-05 | -7.2679E-06 | 3.5813E-07 | -5.7833E-09 | 
 |1.4 | V| -3.4803E-04 | 1.5574E-04 |-2.0192E-05 |9.3006E-07 | -1.4414E-08| 
 |6.8 | v|  2.21863E-04	| -1.18053E-04 |	1.68718E-05	| -8.94076E-07	| 1.60273E-08 |
 |6.8 | h| -3.50262E-06	| 1.02052E-05 | -5.28636E-06 | 3.82864E-07 |-7.87283E-09 |
 |6.8 | U| -0.00013924 |	8.4043E-05	| -1.4662E-05	| 8.0212E-07	| -1.4012E-08|
 |6.8 | V| -0.00019835| 8.6777E-05| -9.2229E-06 | 3.6747E-07 | -5.0171E-09 | 
 |10.7 | v| 1.48213E-04 |	-7.15954E-05 |	1.01992E-05 |	-5.41575E-07|	9.71451E-09|
 |10.7 | h |-8.09058E-05|	6.06930E-05	|-1.42500E-05	|8.86313E-07	|-1.69340E-08|
 |10.7 | U| -1.90531E-04|	1.09714E-04|	-1.97712E-05|	1.10888E-06|	-1.96980E-08| 
 |10.7 | V| -9.49332E-05|	3.91291E-05	|-1.64418E-06|	-2.12315E-08 |	1.47529E-09 | 
 |18.7 | v| 1.21860E-04| -6.39714E-05| 9.34100E-06| -5.24394E-07| 9.97506E-09 | 
 |18.7 | h| 2.65036E-04 | -9.32568-05 | 1.41605E-06| 2.98507E-07 | -9.64763E-09 | 
 |18.7 | U| 1.66139E-04| -4.39714E-05 | -5.42274E-06 | 6.82097E-07 | -1.69151E-08 | 
 |18.7 | V| -1.62337E-04| 7.13779E-05 | -5.42054E-06 |1.26562E-07 | -3.00476E-10 |  
 |36.5 | v| =2.32150E-04| -1.2285E-04| 1.4729E-05 | -7.0225E-07| 1.1826E-08 | 
 |36.5 | h| 7.143E-04| -2.795E-04| 2.1529E-05 |-5.4446E-07 |2.664E-09 | 
 |36.5 | U| 1.37851E-04| -1.58017E-05| -9.08052E-06| 9.03144E-07|-2.16700E-08 | 
 |36.5 | V| -1.3425E-04|7.0944E-05 | -8.5829E-06 |3.9147e-07 |-6.1555e-09 | 
```

A shown in {numref}`HVpol_allband_CIMR_anisotropic_1_GMF` and {numref}`HVpol_allband_CIMR_anisotropic_2_GMF`, the wind direction signal is in all Stokes parameters for sea surface emission ({cite:p}`Bespalova1982`;{cite:p}`Gasiewski1994`;{cite:p}`Trokhimovski1995`; {cite:p}`yueh1997`). However, sensitivity of vertically and horizontally polarized brightness temperatures to cloud liquid water and atmospheric water vapor at Ka- to C-band result in the inability to measure wind direction exactly from Space as the signal is relatively small with respect the amplitudes of errors made in the atmospheric corrections, particularly in rainy conditions. The 3rd ($U$) and 4th ($V$) Stokes parameters are less sensitive to cloud liquid water and atmospheric water vapor at these frequencies, and are therefore more suitable for wind direction retrieval ({cite:p}`Irisov1991`; {cite:p}`yueh1994`; {cite:p}`Irisov2000`, {cite:p}`Laursen2001`; {cite:p}`Piepmeier2001`; {cite:p}`Lahtinen2003`; {cite:p}`yueh2006`). While the H and V polarization signal depend on the wind direction, the retrieval of sea surface wind direction from CIMR measured brightness temperatures will therefore require a very accurate knowledge of the third Stokes parameter, which is one of the basic inputs for any wind vector retrieval algorithm ({cite:p}`Meissner2006`). 
 
At ka-band and for ‘normal to high wind conditions’ (<15 m/s), the 3rd Stokes parameter amplitude is less than 3K peak-to peak. The Fourth Stokes parameter first harmonic is almost zero for all wind speed and frequencies. The $V$ parameter second harmonic is higher than the first harmonic and can reach peak-to-peak change of 1 K at 1.4 GHz. Note that everything above, say 17 m/s, is pretty much guess work. Some algorithm keep the signals constant above 24.5 m/s or use linear extrapolation of the GMFs. The third stokes harmonics amplitude (and therefore sensitivity to wind direction) are significantly reduced (by about a factor 2) at L-band with respect X- and Ka-band to stay below 0.5 K peak-to-peak for most wind speed conditions < 15 m/s, making the retrieval of wind direction from L-band third stokes rather challenging. Note however that according to Aquarius and SMAP data, $V$ directional asymmetries seem larger at L-band than at the higher CIMR frequencies-band. 


### Functionnal flow diagram

```{figure} sketch_CIMR_GMF.png
--- 
name: TSM_Flowchart
---
Flowchart of the microwave rough ocean surface emissivity model used in this ATBD. 
```


## Atmospheric contributions 

Our forward model algorithm for atmospheric corrections for CIMR data consists in:
- Input co-localized auxiliary atmospheric parameters (pressure, temperature, relative humidity, cloud water,...), obtained from e.g., ECMWF atmospheric forecast model on multiple levels,
- Attenuation rates and atmospheric absorption are estimated on N-layers along the vertical from ground to satellite altitude using the Milimeter Wave Propagation Model (MPM) and finally integrated along the path from target to satellite.

### Physics of the problem

#### Electromagnetic Wave Propagation through the Atmosphere

At microwave frequencies, atmospheric scattering can be neglectedfor the cases of interest where there is little or no precipitation. To begin the development, the electric field components in the plane normal to the propagation direction may be written as

$$
\begin{eqnarray}
E_h(r,t) &=& \Re\left\{\hat{E}_h(r,t) \right\} = \Re\left\{a_h e^{i(k r - \omega t - \phi_h)}\right\},\\
E_v(r,t) &=& \Re\left\{\hat{E}_v(r,t) \right\} = \Re\left\{a_v e^{i(k r - \omega t - \phi_v)}\right\},
\end{eqnarray}
$$ (eqatm1)

where $\phi_h$ and $\phi_v$ are constant phases, $r$ is distance along the propagation path, $k$ is wavenumber magnitude, $\omega$ is the radiation frequency, $t$ is time, and the real amplitudes $a_h(r)$ and $a_v(r)$ are functions of propagation distance $r$. In general as the radiation propagates through the atmosphere it experiences changes in the dielectric properties of the medium. We will assume that the amplitude coefficients satisfy the simple ordinary different equations:

$$
\begin{eqnarray}
\frac{d a_h}{dr} = -b(r)a_h(r),\label{eq_dah}\\
\frac{da_v}{dr} = -b(r)a_v(r).\label{eq_dav}
\end{eqnarray}
$$(eqatm2)

In reality, the amplitude attenuation rate $b(r)$ is a function of space and time and may be computed using molecular oxygen ($O_2$) and water vapor concentration profiles along with atmospheric physical temperature and pressure profiles. The attenuation rate, or attenuation coefficient, $b$ (typically expressed in units of nepers per meter), generally is a complicated function of atmospheric state (i.e. pressure, temperature, water content in various forms, etc.). Multiplying first equation in [Equation](eqatm2) by $a_h$ and second by $a_v$ and rearranging yields:

$$
\begin{eqnarray}
\frac{d a_h^2}{dr} = -2 b(r)a_h^2(r),\label{eq_dah2}\\
\frac{d a_v^2}{dr} = -2 b(r)a_v^2(r).\label{eq_dav2}
\end{eqnarray}
$$ (eqatm3)

Similarly, multiplying first equation in [Equation](eqatm2) by $a_v$ and second by $a_h$ and adding yields:

$$
\begin{eqnarray}
\frac{d a_va_h}{dr} = -2 b(r)a_va_h(r).\label{eq_davh}
\end{eqnarray}
$$ (eqatm4)

If the attenuation rate $b$ is independent of spatial location and time, and if we let the electric field amplitudes at some reference location (at which $r=0$) be $a_{vo}$ and $a_{ho}$, then

$$
\begin{eqnarray}
a_h(r) = a_{ho}e^{-b r},
a_v(r) = a_{vo}e^{-b r},
\end{eqnarray}
$$ (eqatm5)

so that

$$
\begin{eqnarray}
E_h(r,t) &=& \Re\left\{\hat{E}_h(r,t) \right\} = \Re\left\{a_{ho} e^{i(k r - \omega t - \phi_h) - b r}\right\},\\
E_v(r,t) &=& \Re\left\{\hat{E}_v(r,t) \right\} = \Re\left\{a_{vo} e^{i(k r - \omega t - \phi_v) - b r}\right\}.
\end{eqnarray}
$$ (eqatm6)

where $a_{ho}$ and $a_{vo}$ are the real amplitudes of the components at some reference location $r=0$. We may also represent this attenuation rate as an imaginary part of the wavenumber magnitude $k$, so that we let

$$
\begin{eqnarray}
\tilde{k} = k + i b = \tilde{k}_r + i \tilde{k}_i,
\end{eqnarray}
$$ (eqatm7)

where now $\Re(\tilde{k})$ gives the propagation speed in terms of $\omega$ while $\Im(\tilde{k})$ gives the attenuation rate.

$$
\begin{eqnarray}
E_h(r,t) &=& \Re\left\{\hat{E}_h(r,t) \right\} = \Re\left\{a_{ho} e^{i(\tilde{k} r - \omega t - \phi_h)}\right\},\\
E_v(r,t) &=& \Re\left\{\hat{E}_v(r,t) \right\} = \Re\left\{a_{vo} e^{i(\tilde{k} r - \omega t - \phi_v)}\right\}.
\end{eqnarray}
$$ (eqatm8)

The complex wavenumber magnitude $\tilde{k}$ is the key quantity required to model the radiation propagation (including curvature in propagation path) and attenuation along the path, and in the present algorithm, we use the Millimeter-wave Propagation model of {cite:p}`Liebe1993` (hereafter referred to as the MPM93), which is a refined version of the model presented in {cite:p}`Liebe1989`, to compute $\tilde{k}$ as a function of atmospheric state along the radiation propagation path. As $\tilde{k}$ depends on molecular oxygen concentration and, water vapor concentration, the key atmospheric variables required are dry air pressure and water vapor mixing ratio. The Millimeter-wave Propagation model provides an explicit expression for the so-called complex index of refraction, denoted by $N$,which is defined so that:

$$
\begin{eqnarray}
\tilde{k} = \tilde{k}_r + i \tilde{k}_i = k + i b = k + k N = k + k (N_0 + N'_0) + i N'',
\end{eqnarray}
$$ (eqatm9)

where $N_0$, $N'$, and $N''$ are all real quantities that depend upon the atmospheric state. The nondispersive part $N_0$ is real and positive and independent of frequency while $N'_0$ and $N''$ depend on frequency, in general. Refractivity is easily converted into path-sêcific propagation rates; i.e.,the imaginary part of [Equation](eqatm9) lead to power attenuation. The real and imaginary parts of complex index of refraction are related to the real and imaginary parts of the complex wavenumber by the equations

$$
\begin{eqnarray}
\tilde{k}_r &=& k \left(1 + N_0 + N'\right),\\
\tilde{k}_i &=& b(r) = k N''.
\end{eqnarray}
$$ (eqatm10)

Thus, $N''$ corresponds to the loss portion of $\tilde{k}$ while $N_0+N'$ corresponds to the propagation speed portion of $\tilde{k}$. It follows that the corresponding *amplitude* attenuation rate, $b(r)$, expressed in nepers per meter, is

$$
\begin{eqnarray}
b(r) = kN'' = \left(\frac{2\pi f}{c}\right) N'' \quad \mbox{[Np m$^{-1}$]},
\end{eqnarray}
$$ (eqatm11)

and the *power* attenuation rate is

$$
\begin{eqnarray}
a(r) = 2b(r) = 2kN'' = \left(\frac{4\pi f}{c}\right) N'' \quad \mbox{[Np~m$^{-1}$]},
\end{eqnarray}
$$(eqatm12)

where $c$ is the speed of light in a vacuum (m.s$^{-1}$) and $f$ is
the electromagnetic frequency in hertz. The index of refraction as
provided by the MPM93, $\tilde{N}=\tilde{N}_0+\tilde{N'}+\tilde{N}''$,
is expressed in ppm (i.e., it is scaled by $10^6$) so that for $b(r)$
in nepers per meter, we have

$$
\begin{eqnarray}
\tilde{k}_r(r) = b(r) = kN'' = \left(\frac{2\pi f}{c}\right) \cdot 10^{-6} \cdot
\tilde{N}''
\quad
\mbox{[Np m$^{-1}$]},
\end{eqnarray}
$$(eqatm13)

or for $b(r)$ in dB.km$^{-1}$ with $f$ in gigahertz,

$$
\begin{eqnarray}
b(r) = kN'' = \left(\frac{2\pi f}{c}\right)
\left(\frac{10}{\log_e(10)}\frac{\mbox{dB}}{\mbox{Np}}\right)
\left(10^3\frac{\mbox{m}}{\mbox{km}}\right)
\left(10^9\frac{\mbox{Hz}}{\mbox{GHz}}\right)
\cdot 10^{-6}
\cdot \tilde{N}''
\approx
0.0910\cdot f \tilde{N}''
\quad
\mbox{[dB km$^{-1}$]}.
\end{eqnarray}
$$(eqatm14)

The real part of the complex wavenumber, $\tilde{k}_r(r)$, is

$$
\begin{eqnarray}
\tilde{k}_r(r)
=
\frac{360}{2\pi}
\left(\frac{\mbox{deg}}{\mbox{rad}}\right)
\left(\frac{2\pi f}{c}\right)
\left(10^9\frac{\mbox{Hz}}{\mbox{GHz}}\right)
\left(10^3\frac{\mbox{m}}{\mbox{km}}\right)
\left[1 + \cdot 10^{-6} \cdot \left(\tilde{N}_0 + \tilde{N}'\right) \right]
\quad
\mbox{[deg km$^{-1}$]}.
\end{eqnarray}
$$(eqatm15)

The variable part of the preceding expression for $\tilde{k}_r(r)$ is
called the *phase dispersion*, $\beta$, and is approximately

$$
\begin{eqnarray}
\beta
=
1.2 f \left(\tilde{N}_0 + \tilde{N}'\right)
\quad
\mbox{[deg km$^{-1}$]},
\end{eqnarray}
$$(eqatm16)

with $f$ expressed in gigahertz and $\tilde{N}_0$ and $\tilde{N}'$
expressed in ppm. From $\tilde{k}_r$ we can derive the wave
propagation speed $\tilde{c}(r)$:

$$
\begin{eqnarray}
\tilde{c}(r)
=
1000
\cdot
\frac{\omega}{\tilde{k}_r(r)}
\left(\frac{\mbox{deg~s$^{-1}$}}{\mbox{deg km$^{-1}$}}\right)
=
1000
\cdot
\frac{360 f}{\tilde{k}_r(r)}
\left(\frac{\mbox{deg~s$^{-1}$}}{\mbox{deg km$^{-1}$}}\right)
=
c
\left[1 + 10^{-6} \cdot \left(\tilde{N}_0 + \tilde{N}'\right) \right]^{-1}
\quad
\mbox{[m s$^{-1}$]},
\end{eqnarray}
$$ (eqatm17)

where as before $c$ is expressed in meters per second and $\tilde{N}_0$ and $\tilde{N}'$ are expressed in ppm as in the MPM93. If we were concerned about propagation path curvature, we would need to use this expression to derive the propagation path for each point in the antenna pattern director cosine coordinates. But we will assume that at CIMR frequencies such curvature effects are negligible. Next we will examine the formulation of $\tilde{N}_0$ and $\tilde{N}'$ in the MPM93 and then relate the total refractive index $\tilde{N}$ to the Stokes vector, which is our primary concern.

##### Formulation of the Atmospheric Refractive Index

As formulated in the MPM93, the total index of refraction is the sum of indices of refraction owing to :

- molecular oxygen ($ \tilde{N}_D$),
- water vapor ($ \tilde{N}_V$), 
- cloud water ($ \tilde{N}_W$), 
- ice water ($ \tilde{N}_I$), and,
- rain ($ \tilde{N}_R$), 

so that

$$
\begin{eqnarray}
\tilde{N}(T_r,e,p_d,f) = \tilde{N}_0 + \tilde{N}' + i\tilde{N}''
= \tilde{N}_D(T_r,e,p_d,f) +\tilde{N}_V(T_r,e,p_d,f) + \tilde{N}_W(T_r,\rho_w,f) + \tilde{N}_I(T_r,\rho_i,f)+ \tilde{N}_R(R,z,f)
\quad\mbox{[ppm]},\nonumber
\end{eqnarray}
$$(eqatm18)

where :
- $p_d$ and $e$ are the partial pressures of dry air and water vapor (hPa), respectively; 
- $\rho_w$ and $\rho_i$ are the liquid water and ice densities (g.m$^{-3}$), respectively; 
- $R$ is rain rate at altitude $z$,
- $T_r$ is the *reciprocal temperature*, defined by

$$
\begin{eqnarray}
T_r = \frac{300}{T_p},
\end{eqnarray}
$$(eqatm19)

where $T_p$ is the physical temperature in kelvin. The indices of refraction are expressed in the MPM93 in terms of the reciprocal temperature, partial pressures of dry air and water vapor (which is a function of relative humidity and temperature), and cloud water and ice densities (not mixing ratios). The molecular oxygen concentration is a function of the partial pressure of dry air, $p_d$ (expressed in hPa), which is approximately equal to the total pressure $p_t$ minus the partial pressure of water vapor $e$:

$$
\begin{eqnarray}
p_d = p_t - e,
\end{eqnarray}
$$(eqatm20)

Following {cite:p}`Liebe1989`, we introduce the following approximation to the water saturation vapor pressure over a plane surface of water:

$$\begin{eqnarray}
e_s(T_r) = 2.408\times 10^{11}T_r^5 e^{-22.644 \cdot T_r},
\end{eqnarray}
$$(eqatm21)

Using this approximation, the partial pressure of water vapor in hectopascals is

$$
\begin{eqnarray}
e(T_r,r_H) = e_s(T_r)\frac{r_H}{100} = \frac{r_H}{100} \cdot 2.408\times 10^{11}T_r^5 e^{-22.644 \cdot T_r},
\end{eqnarray}
$$(eqatm22)

where $r_H$ is the relative humidity in percent. 

The dry air density is given in [$kg/m^3$],

$$
\rho = \frac{p_d\times100}{(R_d\times T_r)}
$$ (eqatm22a)

where $R_d=287.1$ J kg$^{-1}$K$^{-1}$ and $p_d$ is the dry air pressure in [hPa].

The density of cloud water in [kg/m$^3$] is defined as the product of the dry air density by the cloud water mixing ratio, which is defined as the ratio of the mass of water to the mass of dry air, and it has units of [kg/kg].

$$
\rho_w = \rho\cdot m_{clw}
$$ (eqatm22b)

##### Formulation of the dry air index of refraction

The dry air index of refraction $\tilde{N}_D$ consists of a nondispersive term $N_d$, a nonresonant term $N_n$, and a sum over relevant molecular oxygen absorption lines:

$$
\begin{eqnarray}
\tilde{N}_D(T_r,e,p_d,f) = \tilde{N}_d + \tilde{N}_n + \displaystyle\sum_{k=1}^{44} S_kF_k
\quad\mbox{[ppm]}.
\label{eq_n_D_tilde}
\end{eqnarray}
$$(eqatm23)

The nondispersive term is

$$
\begin{eqnarray}
\tilde{N}_d = 0.2588 p_dT_r
\quad\mbox{[ppm]},
\end{eqnarray}
$$(eqatm24)

and the nonresonant term is given by the sum of a relaxation spectrum term $S_\circ F_\circ$ and a term associated with pressure-induced $N_2$ absorption (which makes a small contribution above 100 GHz), $S_nF_n$:

$$
\begin{eqnarray}
\tilde{N}_n = S_\circ F_\circ + i S_n F_n
\quad\mbox{[ppm]},
\end{eqnarray}
$$(eqatm25)

with

$$
\begin{eqnarray}
S_\circ &=& 6.14\times10^{-5} p_d T_r^2\quad\mbox{[ppm]},\\
F_\circ &=& -f\left[f+i0.56\times10^{-3}(p_d+e)T_r^{0.8}\right]^{-1},\\
S_n     &=& 1.4\times10^{-12} p_d^2T_r^{3.5}\quad\mbox{[ppm]},\\
F_n     &=& f\left[1 + 1.93\times10^{-5}f^{1.5}\right]^{-1}.
\end{eqnarray}
$$(eqatm26)

In the sum over absorption lines, $\displaystyle\sum_{k=1}^{44} S_kF_k$, the individual line strengths are given by

$$
\begin{eqnarray}
S_k = 1\times10^{-6}\frac{a_1}{\nu_k}p_dT_r^3\exp{\left[a_2(1-T_r)\right]}\quad\mbox{[ppm]},
\end{eqnarray}
$$ (eqatm27)

where $a_1$ and $a_2$ are constants for each line. The line form (or line spreading) factor, known as the Van Vleck-Weisskopf function, is given by

$$
\begin{eqnarray}
F_k = f\left[\frac{1-i\delta_k}{\nu_k-f-i\gamma_k} - \frac{1+i\delta_k}{\nu_k+f+i\gamma_k}\right],
\end{eqnarray}
$$ (eqatm28)

with the overlap parameter $\delta_k$ given by

$$
\begin{eqnarray}
\delta_k = 1\times10^{-3}\left(a_5+a_6T_r\right)\left(p_d+e\right)T_r^{0.8},
\end{eqnarray}
$$(eqatm29)

where $a_5$ and $a_6$ are constants for each line. The width parameter
$\gamma_k$ is given by

$$
\begin{eqnarray}
\gamma_k = \left(\tilde{\gamma}_k^2 + 2.25 \times 10^{-6}\right)^{1/2}
\quad\mbox{[GHz]},
\end{eqnarray}
$$ (eqatm30)

with

$$
\begin{eqnarray}
\tilde{\gamma}_k = 1\times10^{-3}a_3\left(p_dT_r^{a_4} + 1.1 e T_r\right)
\quad\mbox{[GHz]},
\end{eqnarray}
$$ (eqatm31)

where $a_3$ and $a_4$ are constants for each line. The difference between $\gamma_k$ and $\tilde{\gamma}_k$ is related to the Zeeman effect in which absorption lines are split into multiple lines.

Note that the $a_1$ to $a_6$ parameters for each line are provided as input tables in the model.

##### Formulation of the index of refraction for water vapor

The index of refraction for water vapor is the sum of a nondispersive term, a continuum term, and a sum over 35 resonant absorption lines (including one pseudo-line at 1780 GHz). At the CIMR frequencies the continuum term is negligible so that

$$
\begin{eqnarray}
\tilde{N}_V \approx \tilde{N}_v + \displaystyle\sum_{k=1}^{35}
S^{(v)}_kF^{(v)}_k \quad\mbox{[ppm]}.
\label{eq_n_V_tilde}
\end{eqnarray}
$$ (eqatm33)

The nondispersive term is

$$
\begin{eqnarray}
\tilde{N}_v(T_r,e,p_d) = \left(4.163T_r + 0.239\right) e T_r
\quad\mbox{[ppm]}.
\end{eqnarray}
$$ (eqatm34)

The absorption line strength in the sum over the lines is

$$
\begin{eqnarray}
S^{(v)}_k = \left(\frac{b_1}{\nu_k}\right) e T_r^{3.5}\exp{\left[b_2\left(1-T_r\right)\right]},
\end{eqnarray}
$$ (eqatm35)

where $b_1$ and $b_2$ are constants defined for each line $k$. The
line form function has the same form as for oxygen except that there
is no line overlap effect:

$$
\begin{eqnarray}
F^{(v)}_k = f\left[\frac{1}{\nu^{(v)}_k-f-i\gamma^{(v)}_k} - \frac{1}{\nu^{(v)}_k+f+i\gamma^{(v)}_k}\right].
\end{eqnarray}
$$ (eqatm36)

For a total pressure above 0.7 hPa, the width of a pressure-broadened
vapor line, $\gamma^{(v)}_k$, is given by

$$
\begin{eqnarray}
\gamma^{(v)}_k = 1\times10^{-3} b_3 \left(b_4 e(e_s(T_r),r) T_r^{b_6} + p_dT_r^{b_5}\right)
\quad\mbox{[GHz]},
\end{eqnarray}
$$ (eqatm37)

where $b_3$, $b_4$, $b_5$ and $b_6$ are constants defined for each line $k$. Below 0.7 hPa doppler broadening can be significant, so that in this case $\gamma^{(v)}_k$ is modified to be

$$
\begin{eqnarray}
\gamma^{(v)}_k = 0.535\tilde{\gamma}^{(v)}_k + \left(0.217\left(\tilde{\gamma}^{(v)}_k\right)^2 + \gamma_D^2\right)^{1.2}
\quad\mbox{[GHz]},
\end{eqnarray}
$$ (eqatm38)

where $\tilde{\gamma}^{(v)}_k$ is given by

$$
\begin{eqnarray}
\tilde{\gamma}^{(v)}_k = 1\times10^{-3} b_3 \left(b_4 e(e_s(T_r),r) T_r^{b_6} + p_dT_r^{b_5}\right)
\quad\mbox{[GHz]}
\end{eqnarray}
$$ (eqatm39)

and the Doppler width $\gamma_D$ is

$$
\begin{eqnarray}
\gamma_D = 1.46\times 10^{-6}\nu^{(v)}_k T_r^{1/2}
\quad\mbox{[GHz]}.
\end{eqnarray}
$$ (eqatm40)

##### Formulation of the liquid water index of refraction

The liquid water index of refraction is given by

$$
\begin{eqnarray}
\tilde{N}_W(T_r,\rho_w,f) &=& 1.5 \rho_w \left(\frac{\epsilon_w-1}{\epsilon_w+2}\right)
\quad\mbox{[ppm]},
\label{eq_n_W_tilde}
\end{eqnarray}
$$ (eqatm40b)

which is a function of both the cloud water density $\rho_w$ (g.m$^{-3}$) and the complex permittivity of pure water $\epsilon_w$. The complex permittivity of pure water, in turn, is approximated by a double-Debye fit to measured data,

$$
\begin{eqnarray}
\epsilon_w = \epsilon_0 - f\left(\frac{\epsilon_0-\epsilon_1}{f + i\gamma_1} + \frac{\epsilon_1-\epsilon_2}{f + i\gamma_2}\right),
\end{eqnarray}
$$ (eqatm41)

with

$$
\begin{eqnarray}
        \epsilon_0 &=& 77.66 + 103.3(T_r-1),\\
        \epsilon_1 &=& 0.0671 \epsilon_0,\\
        \epsilon_2 &=& 3.52 - 7.52(T_r-1),\\
          \gamma_1 &=& 20.2 - 146.4(T_r-1) + 316(T_r-1)^2\quad\mbox{[GHz]},\\
          \gamma_2 &=& 39.8 \gamma1\quad\mbox{[GHz]}.
\end{eqnarray}
$$ (eqatm42)

Here, $\epsilon_0$ and $\epsilon_1$ are the static and high-frequency permittivities, respectively; $\epsilon_2$ is a model parameter which has a slight temperature dependence that has been removed in {cite:p}`Liebe1993` in order to avoid unphysical behavior for supercooled water above 100 GHz. As we do not consider liquid water effects below freezing, we retain this dependence. The parameters $\gamma_1$ and $\gamma_2$ are two relaxation frequencies expressed in gigahertz; $\rho_w$ is the liquid water density (g.m$^{-3}$) and $f$ is the radiation frequency in gigahertz. 

###### Formulation of the index of refraction for ice

The index of refraction for ice is given by

$$
\begin{eqnarray}
\tilde{N}_I(T_r,\rho_i,f) &=& 1.5\left(\frac{\rho_i}{0.916}\right)\left(\frac{\epsilon_i-1}{\epsilon_i+2}\right)
\quad\mbox{[ppm]},
\label{eq_n_I_tilde}
\end{eqnarray}
$$ (eqatm43)

where $\rho_i$ is the ice water density (g.m$^{-3}$). The permittivity of ice, $\epsilon_i$ is given as a function of electromagnetic frequency and reciprocal temperature by

$$
\begin{eqnarray}
\epsilon_i = 3.15 + i\left(\frac{a_i}{f} + b_i f\right),
\end{eqnarray}
$$ (eqatm44)

where

$$
\begin{eqnarray}
a_i &=& (T_r-0.171)\exp{\left[17.0 - 22.1 T_r\right]}\quad\mbox{[GHz]},\\
b_i &=& 1\times 10^{-5}\left[\left(\frac{0.233}{1-0.993/T_r}\right)^2 + \frac{6.33}{T_r} - 1.31\right]\quad\mbox{[GHz$^{-1}$]}.
\end{eqnarray}
$$ (eqatm45)



##### Formulation of the index of refraction for rain


Refractivity of rain, $N_R$ is governed by absorption and scattering effects. Substantial interactions take place when drop diameters (0.1 to 5 mm) and radio wavelengths become comparable. Bypassing elaborate, lengthy Mie calculations which require drop shape and size distributions as well as the dielectric permittivity of water, the following approximations are used,

$$
\begin{eqnarray}
\tilde{N}_R(R,z,f) &=& R\cdot (0.012 R-3.7)\cdot \displaystyle\frac{y^{2.5}}{f_R(1+y^{2.5})}+i\cdot c_R R^z
\end{eqnarray}
$$ (eqatm45a)

where $R$ is the rain rate in [mm/h], $z$ the altitude, $y=f/f_R$, $f_R=53-R(0.37-0.0015R)$, $c_R=x_1 and $z=x_2\cdot f\cdot y_2$, where $x_1$=3.51e-4, $y_1$=1.03, $x_2$=0.851 and $y_2$=0.158 for f=1.4 GHz and $x_1$=2.31e-4, $y_1$=1.42, $x_2$=1.41 and $y_2$=-0.0779 for the 4 higher frequencies of CIMR.


### Effects on the Stokes Vector

For a deterministic signal, the coefficients $a_h(r)$ and $a_v(r)$ may be considered to be functions of distance, but for a non-deterministic signal these coefficients must be considered to be random variables, and in this case, we are primarily interested in the second moments of the electric field vector. As such, we are concerned with the effect of the atmosphere on the Stokes vector,

$$
\begin{eqnarray}
\left(
\begin{matrix}
I\\
Q\\
U\\
V\\
\end{matrix}
\right) =
{\cal K}
\left(
\begin{matrix}
\left<E_v E_v^* + E_h E_h^*\right>\\
\left<E_v E_v^* - E_h E_h^*\right>\\
2\Re{\left<E_v E_h^*\right>}\\
2\Im{\left<E_v E_h^*\right>}\\
\end{matrix}
\right)
=
\left(
\begin{matrix}
\left<a_v^2+a_h^2\right>\\
\left<a_v^2-a_h^2\right>\\
2\left<a_va_h\cos(\delta_0)\right>\\
2\left<a_va_h\sin(\delta_0)\right>\\
\end{matrix}
\right),
\end{eqnarray}
$$ (eqatm46)

where ${\cal K} = \frac{\lambda^2}{k_b\eta_0 B}$ is a constant coefficient that depends upon the receiver bandwidth $B$, and the electromagnetic wavelength $\lambda$.

The amplitude components are now random variables with a polarized and a non-polarized component. We now assume that the atmospheric attenuation rate $b(r)$ is not a random variable, so that the attenuation coefficients may be extracted from the ensemble averages. In this case, [Equation](eqatm3), and [Equation](eqatm4) become, respectively,

$$
\begin{eqnarray}
\frac{d\left<a_h^2\right>}{dr}  &=& -2 b(r)\left<a_h^2(r)\right>,\label{eq_dah2r}\\
\frac{d\left<a_v^2\right>}{dr}  &=& -2 b(r)\left<a_v^2(r)\right>,\label{eq_dav2r}\\
\frac{d\left<a_va_h\right>}{dr} &=& -2 b(r)\left<a_va_h(r)\right>.\label{eq_davhr}
\end{eqnarray}
$$ (eqatm47)

It follows directly from [Equation](eqatm46), and [Equation](eqatm47) that the Stokes vector components satisfy the attenuation equations

$$
\begin{eqnarray}
\frac{d}{dr}
\left(
\begin{matrix}
I(r)\\
Q(r)\\
U(r)\\
V(r)\\
\end{matrix}
\right)
=
-2 b(r)
\left(
\begin{matrix}
I(r)\\
Q(r)\\
U(r)\\
V(r)\\
\end{matrix}
\right).\label{eq_satt_i}
\end{eqnarray}
$$(eqatm48)

The modified Stokes vector satisfies a similar equation:

$$
\begin{eqnarray}
\frac{d}{dr}
\left(
\begin{matrix}
T_h(r)\\
T_v(r)\\
U(r)\\
V(r)\\
\end{matrix}
\right)
=
-2 b(r)
\left(
\begin{matrix}
T_h(r)\\
T_v(r)\\
U(r)\\
V(r)\\
\end{matrix}
\right).\label{eq_satt_thtv}
\end{eqnarray}
$$(eqatm49)


### Atmospheric Emission

The dispersion relation for electromagnetic radiation in free space is

$$
\begin{eqnarray}
\omega = c k = \frac{2 \pi c}{\lambda}, 
\end{eqnarray}
$$ (eqatm50)

where $c$ is the speed of light in free space (m.s$^{-1}$), $\omega$ (rad.Hz) and $\lambda$ (m) are the electromagnetic radian frequency and wavelength, respectively. Thus,

$$
\begin{eqnarray}
\frac{\partial \lambda}{\partial \omega}
= -\frac{2 \pi c}{\omega^2}
= \frac{(2 \pi c) \lambda^2}{(2 \pi c)^2}
= \frac{\lambda^2}{2 \pi c}.\label{eq_lam_om}
\end{eqnarray}
$$ (eqatm51)

To compute the atmospheric emission we assume that the atmosphere is characterized by an emissivity $\epsilon(r)$ varying along the path $r$ across the atmosphere, and that its emission is unpolarized and well-approximated by the Rayleigh-Jeans approximation for blackbody emission multiplied by the (dimensionless) emissivity $\epsilon$

$$
\begin{eqnarray}
I = \epsilon\frac{2\pi c k_b}{\lambda^4}
T_{p}\cdot\left(\frac{\partial \lambda}{\partial \omega}\right),
\label{eq_rjl}
\end{eqnarray}
$$ (eqatm52)

where $I$ is the emitted power (specifically, the spectral radiance or brightness) with units (W m$^{-2}$sr$^{-1}$Hz$^{-1}$), $T_{p}$ is the physical temperature. Using [Equation](eqatm51), [Equation](eqatm52) becomes

$$
\begin{eqnarray}
I = \epsilon\frac{k_b}{\lambda^2}T_{p}
\end{eqnarray}
$$ (eqatm53)

In the above, $k_b$ is Boltzmann's constant (1.38×10$^{-23}$ J K$^{-1}$). The emissivity accounts for the fact that the atmosphere emits much less radiation than a blackbody at the same physical temperature, and from Ku to L-band this emissivity is quite close to zero but not completely negligible compared with the signal variations owing to wind speed variations. With this modified Rayleigh-Jeans form, the unpolarized atmospheric emission leads to the following ordinary differential equations for the Stokes vector,

$$\begin{eqnarray}
\frac{\partial }{\partial r}
\left(
\begin{matrix}
I(r)\\
Q(r)\\
U(r)\\
V(r)\\
\end{matrix}
\right)
=
\epsilon(r)
\left(
\begin{matrix}
T_p(r)\\
0\\
0\\
0\\
\end{matrix}
\right),\label{eq_sem_i}
\end{eqnarray}
$$ (eqatm54)

or

$$
\begin{eqnarray}
\frac{\partial }{\partial r}
\left(
\begin{matrix}
T_h(r)\\
T_v(r)\\
U(r)\\
V(r)\\
\end{matrix}
\right)
=
\epsilon(r)
\left(
\begin{matrix}
T_p(r)\\
T_p(r)\\
0\\
0\\
\end{matrix}
\right).\label{eq_sem_thtv}
\end{eqnarray}
$$ (eqatm55)

where the emissivity $\epsilon=\epsilon(r)$ is a function of
location along the propagation path, and the factor $k_b/\lambda^2$
does not appear because the Stokes elements implicitly contain this
factor in their definition in terms of moments of the electric field.


### Combining Attenuation and Emission

Combining the atmospheric attenuation [Equation](eqatm48), [Equation](eqatm49) and emission [Equation](eqatm54), [Equation](eqatm55) equations, we have:

$$
\begin{eqnarray}
\frac{\partial }{\partial r}
\left(
\begin{matrix}
I(r)\\
Q(r)\\
U(r)\\
V(r)\\
\end{matrix}
\right)
=
-2 b(r)
\left(
\begin{matrix}
I(r)\\
Q(r)\\
U(r)\\
V(r)\\
\end{matrix}
\right)
+
\epsilon(r)
\left(
\begin{matrix}
2 T_p(r)\\
0\\
0\\
0\\
\end{matrix}
\right),\label{eq_rad_i}
\end{eqnarray}
$$ (eqatm56)

or

$$
\begin{eqnarray}
\frac{\partial }{\partial r}
\left(
\begin{matrix}
T_h(r)\\
T_v(r)\\
U(r)\\
V(r)\\
\end{matrix}
\right)
=
-2 b(r)
\left(
\begin{matrix}
T_h(r)\\
T_v(r)\\
U(r)\\
V(r)\\
\end{matrix}
\right)
+
\epsilon(r)
\left(
\begin{matrix}
T_p(r)\\
T_p(r)\\
0\\
0\\
\end{matrix}
\right).\label{eq_rad_thtv}
\end{eqnarray}
$$ (eqatm57)

Interestingly, with the assumptions we have made, the third and fourth Stokes parameters are affected by attenuation but not by emission. Having established the ordinary differential equation the describes the change in the Stokes vector along the propagation path, we now turn to the problem of implementing a solution procedure that is practical for scene modeling. The straightforward approach is to ignore refraction and to integrate along linear paths through the atmosphere, and this is the approach we shall take.

### Relating Attenuation to Emission

In general radiative transfer scattering may be important, so that attenuation may involve both absorption and scattering. At CIMR frequencies, however, attenuation is dominated by absorption, even in the presence of cloud droplets and ice, so we may assume that the emissivity is equal to the *power* attenuation rate (twice the amplitude attenuation rate):


$$
\begin{eqnarray}
\epsilon(r) \approx 2 b(r).
\end{eqnarray}
$$ (eqatm58)

Given the similar forms for all Stokes vector components, in what
follows, when we will discuss attenuation, we will use the compact Stokes
vector notation:

$$\begin{eqnarray}
\frac{\partial \bf T}{\partial r} = -2 b(r){\bf T} + b(r){\bf T}_p,
\end{eqnarray}
$$ (eqatm59)

where ${\bf T}$ is the modified Stokes vector (with orthogonal linear
components rather than $I$ and $Q$ above) and

$$
\begin{eqnarray}
{\bf T}_p =
\epsilon(r)
\left(
\begin{matrix}
T_p(r)\\
T_p(r)\\
0\\
0\\
\end{matrix}
\right).
\end{eqnarray}
$$ (eqatm60)

We will be concerned about propagation of radiation in the atmosphere at some zenith angle $\theta$ from the vertical direction, so we let $r=z \sec\theta$ be the path length in the propagation direction. We assume that, for a given location in the antenna director cosine coordinates, we can compute the propagation path. As noted in the development above, in general this path will be curved if the propagation speed $c$ (related to the real part of $\tilde{k}$) is a function of position. However, we will neglect this curvature in what follows. At each point of the director cosine grid for which the line-of-sight intersects the earth, the zenith angle is assumed to be identical to the target incidence angle. At each point of the director cosine grid for which the line-of-sight does not intersect the earth, the signal entering the radiometer will be equal to the sum of the atmospheric attenuated sky/sun/moon noise plus the integrated atmospheric emission along the path. In this case, the zenith angle can be computed directly in the geographic frame. In general, refraction should be taken into account when computing the integration path, but for CIMR frequencies this refraction is expected to be negligible and so we will neglect it in what follows.

### Integration of the Radiative Transfer Equation

As mentioned above, our main concern is attenuation and emission along the propagation path, where the *amplitude* attenuation coefficient is given by

$$
\begin{eqnarray}
b(r) = kN'' = 1 \times 10^{-6}\left(\frac{2\pi f}{c}\right)
\Im{\left\{\tilde{N}\right\}}\quad\mbox{[Np~m$^{-1}$]},
\end{eqnarray}
$$ (eqatm61)


As before, $c$ is the speed of light in a vacuum in meters per second, $f$ is the electromagnetic frequency in hertz and $\tilde{N}$ is the sum of the individual indices of refraction for dry air, water vapor, cloud water, and cloud ice as given by [Equation](eqatm23), [Equation](eqatm33), [Equation](eqatm40b), and [Equation](eqatm43), respectively:

$$
\begin{eqnarray}
\tilde{N}(T_r,e,p_d,\rho_w,\rho_i,f) = \tilde{N}_D(T_r,e,p_d,f) + \tilde{N}_V(T_r,e,p_d,f) + \tilde{N}_W(T_r,\rho_w,f) + \tilde{N}_I(T_r,\rho_i,f)\quad\mbox{[ppm]}.
\end{eqnarray}
$$ (eqatm62)

Here we have included explicit dependence of each index of refraction on atmospheric parameters $T_r$,$e$,$p_d$,$\rho_w$ and $\rho_i$. In the forward model we typically take the atmospheric pressure $p$ (derived from geopotential height as a function of pressure), temperature $T$, relative humidity $r$, and cloud water mixing ratio fields $q_c$ from an atmospheric model such as the ECMWF. From the fields in the tmospheric model analyses one can compute the water vapor pressure $e$ from relative humidity $r$ and temperature $T$; we then compute the partial pressure of dry air, $p_d$ from $e$ and $p$. We assume that water is entirely ice below freezing and entirely liquid above freezing, with liquid and ice water densities being $\rho_w=\rho_i=\rho_d q_c$, respectively, in their appropriate temperature ranges.

Having obtained $T$, $p_d$, $e$, $r$ $\rho_w$ and $\rho_i$, we then call four functions implementing the above equations to compute the indices of refraction owing to dry air, water vapor, and liquid and ice water. The resulting refractive indices can then be used to compute the attenuation rates in units of nepers per meter.

The solution procedure involves interpolation of the attenuation rates derived from the atmospheric model fields onto a uniformly spaced grid with $N_a$ layers with layer bottom heights $z_k$ ranging from $z_s=0$ km through $z_t=30$ km with a $\Delta{z}=200$ m grid interval in geopotential height $z$. The *power* attenuation rates, denoted by $a_D(z)$, $a_V(z)$, $a_W(z)$ and $a_I(z)$, are twice the corresponding amplitude attenuation rates given by $b_D(z)$, $b_V(z)$, $b_W(z)$ and $b_I(z)$. Using these power attenuation rates, we then compute the total absorption for each of these components along *vertical* paths from the bottom of the domain to each level. For simplicity, here we first form the total power attenuation rate, $a(z)$, which is the sum of the individual attenuation rates of dry air, water vapor, and liquid and ice water:

$$
\begin{eqnarray}
a(z)
&=& 2b(r) = 2kN'' = a_D(z) + a_V(z) + a_W(z) + a_I(z)\nonumber\\
&=& 2\times10^{-6}\left(\frac{2\pi f}{c}\right)\Im{\left\{\tilde{N}\right\}}\nonumber\\
&=& 2\times10^{-6}\left(\frac{2\pi f}{c}\right)\Im{\left\{\tilde{N}_D(T_r,e,p_d,f) + \tilde{N}_V(T_r,e,p_d,f) + \tilde{N}_W(T_r,\rho_w,f) + \tilde{N}_I(T_r,\rho_i,f)\right\}}\quad\mbox{[Np.m$^{-1}$]}.\nonumber
\end{eqnarray}
$$ (eqatm63)

The integrated attenuation from the surface at height $z_s$ to height $z$ is

$$
\begin{eqnarray}
A^{(u)}(z) \doteq A(z_s,z) = \displaystyle\int_{z'=z_s}^{z} a(z')\,dz',
\end{eqnarray}
$$ (eqatm64)

where the superscript denotes integration from below up to height $z$.

Similarly, the integrated attenuation from height $z$ to the top of the atmosphere is

$$
\begin{eqnarray}
A^{(d)}(z) \doteq A(z,z_t) = \displaystyle\int_{z'=z}^{z_t} a(z')\,dz'\quad\mbox{[Np]},
\end{eqnarray}
$$ (eqatm65)

where the superscript denotes integration from above down to height $z$. The corresponding power transmittances for radiation propagating upward from below and downward from above are, respectively,

$$\begin{eqnarray}
\tau^{(u)}(z) &\doteq& \tau(z_s,z) = \exp{\left[-A^{(u)}(z)\right]} = \exp{\left[-\displaystyle\int_{z'=z_s}^{z} a(z')\,dz'\right]},\\
\tau^{(d)}(z) &\doteq& \tau(z,z_t) = \exp{\left[-A^{(d)}(z)\right]} = \exp{\left[-\displaystyle\int_{z'=z}^{z_t} a(z')\,dz'\right]}.
\end{eqnarray}
$$ (eqatm66)

In discrete form the integrated upward and downward attenuation factors (in nepers) are, respectively,

$$
\begin{eqnarray}
A^{(u)}(z_m) &=& \displaystyle\sum_{k=1}^{m} a(z_k)\Delta{z}\quad\mbox{[Np]},\\
A^{(d)}(z_m) &=& \displaystyle\sum_{k=m}^{N_a} a(z_k)\Delta{z}\quad\mbox{[Np]},
\end{eqnarray}
$$ (eqatm67)

where $A^{(u)}(z_m)$ and $A^{(u)}(z_m)$ have units of nepers since they are attenuation rates integrated over small height ranges. Here the subscript $m$ is an index into the vector of vertical layers that form a discrete vertical grid with layer center heights $z_m$. Except at near grazing zenith angles, an arbitrary path will not traverse a horizontal distance of more than a few kilometers, and if we assume that the atmosphere on this spatial scale is horizontally uniform, then the total attenuation along a path at zenith angle $\theta$ may be obtained from the preceding total attenuation values by multiplication by $\sec\theta$. The resulting zenith transmissivity between the surface and layer $k$ is then

$$
\begin{eqnarray}
\tau^{(u)}(z_m) &=& \tau(z_s,z_m) = \exp{\left[-A^{(u)}_m\right]}.
\end{eqnarray}
$$ (eqatm68)

In terms of the individual contributions by dry air, water vapor,
cloud water and cloud ice, the total transmissivity from the surface
to the top of layer $z_m$ is

$$
\begin{eqnarray}
\tau^{(u)}(z_m) &\doteq& \tau(z_s,z_m) = \exp{\left[-A^{(u)}(z_m)\right]} = \tau_D^{(u)}(z_m)\tau^{(u)}_V(z_m)\tau^{(u)}_W(z_m)\tau^{(u)}_I(z_m),
\end{eqnarray}
$$ (eqatm69)

while the total transmissivity from the top of the atmosphere to the base of layer $z_m$ is

$$
\begin{eqnarray}
\tau^{(d)}(z_m) &\doteq& \tau(z_s,z_m) = \exp{\left[-A^{(d)}(z_m)\right]} = \tau_D^{(d)}(z_m)\tau^{(d)}_V(z_m)\tau^{(d)}_W(z_m)\tau^{(d)}_I(z_m).
\end{eqnarray}
$$ (eqatm70)

The transmissivities at zenith angle $\theta$ are obtained by raising these zenith transmissivities to the negative $\sec\theta$ power:

$$
\begin{eqnarray}
\tau^{(u)}(z_m,\theta) &\doteq& \tau(z_s,z_m,\theta) = \exp{\left[-A^{(u)}(z_m)\sec\theta\right]} = \left[\tau_D^{(u)}(z_m)\tau^{(u)}_V(z_m)\tau^{(u)}_W(z_m)\tau^{(u)}_I(z_m)\right]^{\sec\theta},\\
\tau^{(d)}(z_m,\theta) &\doteq& \tau(z_s,z_m,\theta) = \exp{\left[-A^{(d)}(z_m)\sec\theta\right]} = \left[\tau_D^{(d)}(z_m)\tau^{(d)}_V(z_m)\tau^{(d)}_W(z_m)\tau^{(d)}_I(z_m)\right]^{\sec\theta}.
\end{eqnarray}
$$ (eqatm71)

To complete the model we must account for atmospheric emission. The (assumed to be unpolarized) brightness temperature emitted by the atmosphere per unit height interval at some height $z$ above the ground (i.e., a brightness temperature *rate*) is, assuming that the atmosphere is in thermal equilibrium,

$$
\begin{eqnarray}
\hat{T}_{ba}(z) &=& a(z) T_p(z),
\label{eq_atm_tb_rate}
\end{eqnarray}
$$(eqatm72)

where $T_p(z_k)$ is the physical temperature at height $z_k$ and $\hat{T}_{bd}(z_k)$ is a brightness temperature *rate* with units of kelvin per meter. The total brightness temperature rate of atmospheric emission at the height $z_k$ is, considering all components,

$$
\begin{eqnarray}
\hat{T}_{ba}(z_k) = \hat{T}_{bd}(z_k)+\hat{T}_{bv}(z_k)+\hat{T}_{bw}(z_k)+\hat{T}_{bi}(z_k).
\end{eqnarray}
$$(eqatm73)

We can then vertically integrate this total brightness temperature rate to derive the upwelling attenuated atmospheric brightness temperature at the top of the atmosphere:

$$
\begin{eqnarray}
T^{toa}_{ba} = \displaystyle\int\limits_{z'=z_s}^{z_t} \hat{T}_{ba}(z')\exp{\left[-\int\limits_{z''=z'}^{z_t}a(z'')\,dz''\right]}\,dz'
\end{eqnarray}
$$(eqatm74)

which in discrete form becomes

$$
\begin{eqnarray}
T^{toa}_{ba} = \displaystyle\sum_{k=1}^{m} \tau^{(d)}(z_k)T_{bak} = \displaystyle\sum_{k=1}^{m} \tau(z_k,t_t)T_{bak}
= \displaystyle\sum_{k=1}^{m} \tau(z_k,t_t)a(z_k)T_p(z_k)\Delta{z},
\end{eqnarray}
$$(eqatm75)

where

$$
 \begin{eqnarray}
T_{bak} \approx a(z_k)T_p(z_k)\Delta{z}
\end{eqnarray}
$$ (eqatm76)

is the unattenuated incremental brightness temperature of emission in layer $k$ (with units of kelvin). Similarly, the zenith downwelling brightness temperature at the bottom of the atmosphere is

$$
\begin{eqnarray}
T^{boa}_{ba} = \displaystyle\int\limits_{z'=z_s}^{z_t} \hat{T}_{ba}(z')\exp{\left[-\int\limits_{z''=z_s}^{z'}a(z'')\,dz''\right]}\,dz'
\end{eqnarray}
$$ (eqatm77)

which in discrete form becomes

$$
\begin{eqnarray}
T^{boa}_{ba} = \displaystyle\sum_{k=1}^{m} \tau^{(u)}(z_k)T_{bak} = \displaystyle\sum_{k=1}^{m} \tau(z_s,z_k)T_{bak}
= \displaystyle\sum_{k=1}^{m} \tau(z_s,z_k) a(z_k)T_p(z_k)\Delta{z}.
\end{eqnarray}
$$ (eqatm78)

Although $T^{toa}_{ba}$ and $T^{boa}_{ba}$ do not differ much, they are not identical. Since we must model scenes for a satellite radiometer within the antenna patterns, we also need the self-attenuated atmospheric emission at the flight level in an arbitrary direction whithin the antenna patterns. In general this is a complicated problem because certain directions may involve near-grazing incidence, or even propagation parallel to the ground, in which case refraction and earth curvature effects may become important even at Ku, Ka, X, C and L-bands. Here we choose to simplify the problem by neglecting refraction and earth curvature effects in the propagation path modeling. With this simplification, computing the brightness temperature at antenna level $z_a$ and some zenith angle $\theta$ owing to self-attenuated atmospheric emission reduces to one possible integral when the path is directed upward the earth's surface:

$$
\begin{equation}
T_{ba}(z)
=
\begin{array}{ll}
\sec\theta\displaystyle\int\limits_{z'=z_a}^{z_t} \hat{T}_{ba}(z')\exp{\left[-\sec\theta\int\limits_{z''=z_a}^{z'}a(z'')\,dz''\right]}\,dz',\quad0^\circ<\theta<90^\circ,\\
\end{array}
\label{eq_atm1}
\end{equation}
$$ (eqatm79)

where $\hat{T}_{ba}(z')$ is given by [Equation](eqatm72) evaluated at height $z'$ above the ground. It is important to realize that this is a significant simplification, since in general we would have to integrate along curved paths over the curved surface of the earth, and such curved paths may both decrease and increase in elevation, or even remain parallel to the ground, leading to very large brightness temperatures that may approach the physical atmospheric temperature.

Even with the simplified linear paths, it is not practical to precompute the preceding integrals for all possible antenna heights and zenith angles, and it is also not practical to compute such integrals for each director cosine gridpoint as part of the scene brightness modeling for each measured Stokes vector. Therefore, a further approximation is necessary for practical implementation. The approach we take is to extract the zenith angle dependence from the inner attenuation integrations by expanding the exponentials in series of powers of the integrated path attenuation. Doing so will lead to approximate expressions for the self-attenuated atmospheric emission brightness temperatures in powers of $\sec\theta$, with coefficients that result from integrations along vertical paths only. Such approximate expressions are expected to be reasonable except for nearly horizontal paths. Using

$$
\begin{eqnarray}
e^x = 1 + x + {\cal O}(x^2),
\end{eqnarray}
$$ (eqatm80)

we have

$$
\begin{eqnarray}
\exp{\left[-\sec\theta\int\limits_{z''=z_a}^{z'}a(z'')\,dz''\right]} &\approx& 1 - \sec\theta\int\limits_{z''=z_a}^{z'}a(z'')\,dz'',\\
\end{eqnarray}
$$ (eqatm81)

Substituting the preceding two approximate transmissivity expressions into [Equation](eqatm79), we obtain the approximate brightness temperature at the antenna height:

$$
\begin{equation}
T_{bad}(z)
\approx
\begin{array}{ll}
\sec\theta\left[\displaystyle\int\limits_{z'=z_a}^{z_t} \hat{T}_{ba}(z')\,dz'\right]-\sec^2\theta\left[\displaystyle\int\limits_{z'=z_a}^{z_t} \hat{T}_{ba}(z')\int\limits_{z''=z_a}^{z'}a(z'')\,dz''\,dz'\right],\quad0^\circ<\theta<90^\circ,\\
\end{array}
\label{eq_atm2}
\end{equation}
$$ (eqatm82)

As may be seen, each approximate expression consists of the difference between the unattenuated integrated emission brightness temperature and a term involving attenuation of the brightness along the path. Since all zenith angle dependence has been removed from the integrals, we may precompute these integrals for a fixed antenna elevation and store the results for later calculations at arbitrary zenith angles. In particular, we precompute the following four integrals (each with units of kelvin):

$$
\begin{eqnarray}
\tilde{T}^{(0)}_{bad}(z_a) &=& \displaystyle\int\limits_{z'=z_a}^{z_t} \hat{T}_{ba}(z')\,dz',\label{eq_atm3a}\\
\tilde{T}^{(0)}_{bau}(z_a) &=& \displaystyle\int\limits_{z'=z_s}^{z_a} \hat{T}_{ba}(z')\,dz',\label{eq_atm3b}\\
\tilde{T}^{(1)}_{bad}(z_a) &=& \displaystyle\int\limits_{z'=z_a}^{z_t} \hat{T}_{ba}(z')\int\limits_{z''=z_a}^{z'}a(z'')\,dz''\,dz',\label{eq_atm3c}\\
\tilde{T}^{(1)}_{bau}(z_a) &=& \displaystyle\int\limits_{z'=z_s}^{z_a} \hat{T}_{ba}(z')\int\limits_{z''=z'}^{z_a}a(z'')\,dz''\,dz'.\label{eq_atm3d}
\end{eqnarray}
$$ (eqatm83)

These first two functions are the unattenuated *zenith* brightness temperatures associated with emission from above and below the antenna, respectively; the last two functions represent the extent of brightness temperature attenuation for emission from above and below, respectively, that would be obtained at *zenith*. For the algorithm, one can compute these four functions for a range of discrete heights $z_m$ over the horizontal and temporal domain for which we obtained gridded atmospheric data. Then, in the scene modeling process we interpolated these functions to the antenna height and then computed the actual unpolarized attenuated atmospheric emission brightness temperatures at the antenna for arbitrary zenith angle $\theta$, where $\theta$ is a function of director cosine coordinates as well as of the antenna orientation. The final self-attenuated unpolarized atmospheric emission brightness temperatures incident at the antenna are

$$
\begin{equation}
T_{ba}(z,\theta(\xi,\eta))
\approx
\begin{array}{ll}
\sec\theta\tilde{T}^{(0)}_{bad}(z_a) - \sec^2\theta\tilde{T}^{(1)}_{bad}(z_a) ,\quad0^\circ<\theta<90^\circ,\\
\end{array}
\label{eq_atm4}
\end{equation}
$$ (eqatm84)


The final expression constitutes the model for self-attenuated Ku to L-band atmospheric brightness temperature incident at the antenna. This brightness temperature should be applied equally to both all components of the Stokes vector before the antenna gain pattern is applied to compute the final impact on the antenna temperature. This approximate equation has been found to agree very well with the exact calculation (for linear paths). The difference between this approximate and the exact solutions is less than 0.1 K up to about 86$^\circ$ away from zenith for both upwelling and downwelling radiation. The approximation breaks down badly beyond 89$^\circ$ and therefore should not be used in this zenith angle range. In fact, at large zenith angles path and earth curvature may become significant as well, so that this simplified linear path/flat earth model may introduce significant error.


### Functionnal flow diagram

```{figure} FFD_atmo.png
--- 
name: FFD_atmo
---
Flowchart of the atmospheric radiative transfer model used in this ATBD. Input data are the air surface temperature $T_o$, surface pressure $P_s$, and total column water vapor $V$ and the radiometer incidence angle $θ_s$. Output data are the 1-way atmospheric transmittances associated with molecular oxygen absorption $τ_d$ and water vapor $τ_v$ along a line of sight at angle $θ_s$ from nadir and $T_{ea}$, the unpolarized brightness temperature of atmospheric 1-way emission.
```


## Accounting for rotation of the polarization plane in the Stokes vector

In this section, we summarize the Stokes vector transformation that is applied to the forward model from the surface basis to the instrument antenna frame basis, accounting for both a change in polarization basis and the Faraday rotation associated with the passage of radiation through the ionosphere.

### From surface polarization basis to Ludwig-3 antenna basis


```{figure} ludwig-3.png
--- 
name: ludwig-3
---
Diagram summarizing the two rotations required to transport a brightness temperature vector from the surface basis $(\bf{h},\bf{v})$ into the instrument Ludwig-3 basis $(\bf{\hat{L'}}_x,\bf{\hat{L'}}_y)$. Here boresight is into the page so we are looking down towards the target from the instrument. Positive Faraday rotation corresponds to the rotation of the electric field vector $\bf{E}$ into $\bf{E’}$ by the angle $\Omega$ as shown. The additional rotation associated with the change of basis is a further counterclockwise rotation of the electric field vector, or clockwise rotation of the basis $(\bf{h},\bf{v})$ by the angle $\alpha'$. 
```

The first rotation, counterclockwise by angle $\alpha'$ looking down towards the target from the instrument, is associated with the change of polarization basis from the surface basis to the instrument basis (so-called Ludwig-3 basis as defined in {cite:p}`Ludwig1973`), so that:

$$
\begin{pmatrix}
E_{x} \\ 
E_{y} \\
\end{pmatrix}=\begin{pmatrix}
\cos\alpha' & -\sin\alpha'  \\ 
 \sin\alpha' & \cos\alpha' \\ 
\end{pmatrix}
\begin{pmatrix}
E_{h} \\ 
E_{v} \\
\end{pmatrix}
$$ (eq189)

and the corresponding transformation of the Stokes vector is given by:

$$
\begin{pmatrix}
T_{x} \\ 
T_{y}  \\
U_{xy} \\
V_{xy}  \\
\end{pmatrix}=\begin{pmatrix}
\cos^2\alpha' & \sin^2\alpha' & -\cos\alpha'\sin\alpha' & 0 \\ 
\sin^2\alpha' & \cos^2\alpha' & \cos\alpha'\sin\alpha' & 0 \\
\sin2\alpha' & -\sin2\alpha' & \cos2\alpha' & 0 \\
0 & 0 & 0 & 1 \\
\end{pmatrix}
\begin{pmatrix}
T_{h} \\ 
T_{v}  \\
U \\
V  \\
\end{pmatrix}
$$ (eq190)


```{figure} ludwig-3_2.png
--- 
name: ludwig-32.png
---
Top: Diagram showing the geometry and polarization basis vectors in the surface target frame, denoted by $(\bf{h},\bf{v})$. The altitude of the emission vector, directed towards the satellite, is $\theta_e$, and the azimuth of this vector, $\phi_e$, is measured positive counterclockwise from due east. Right : Diagram showing the geometry in the instrument, or antenna, frame. Ludwig-3 polarization basis vectors are denoted by basis $(\bf{\hat{L'}}_x,\bf{\hat{L'}}_y)$. The polarisation basis rotation angle $\alpha'$ is the clockwise rotation of the surface $(\bf{h},\bf{v})$ into the instrument Ludwig-3 polarization basis $(\bf{\hat{L'}}_x,\bf{\hat{L'}}_y)$. Equivalently, this angle is the counterclockwise rotation of the electric field vector looking down towards the target. The angle of the look direction (towards the ground) off of boresight is $\theta_s$, and the azimuth of the look direction $\phi_s$, is measured positive clockwise from north. 
```

{numref}`ludwig-32.png` shows the surface and instrument (Ludwig-3) polarization basis vectors. The polarization basis rotation angle is found using the method introduced by {cite:p}`Zundo2010`. In this method, the surface polarization basis vectors have the following cartesian components:

$$
\begin{matrix}
\mathbf{\hat{h}}\cdot\mathbf{\hat{X_e}}&=&-\sin\phi_e \\
\mathbf{\hat{h}}\cdot\mathbf{\hat{Y_e}}&=&\cos\phi_e \\
\mathbf{\hat{h}}\cdot\mathbf{\hat{Z_e}}&=&0 \\
\mathbf{\hat{v}}\cdot\mathbf{\hat{X_e}}&=&-\sin\theta_e\cos\phi_e \\
\mathbf{\hat{v}}\cdot\mathbf{\hat{Y_e}}&=&-\sin\theta_e\sin\phi_e \\
\mathbf{\hat{v}}\cdot\mathbf{\hat{Z_e}}&=&\cos\theta_e \\
\end{matrix}
$$ (eq191)

For the instrument polarization basis, the following associations are made:

$$
\begin{matrix}
\mathbf{\hat{x}_{s}} & \rightarrow & \mathbf{\hat{y}} \\
\mathbf{\hat{y}_{s}} & \rightarrow & \mathbf{\hat{x}} \\
\mathbf{\hat{z}_{s}} & \rightarrow & -\mathbf{\hat{z}} \\
\end{matrix}
$$ (eq192)

Now in the conventional formulation for the Ludwig-3 polarization basis vectors, we denote the vector pointing from the antenna to the target by $\bf{\hat{t}}$ and we simply begin by defining the usual « zonal » and « meridional » unit vectors on the sphere and then rotate them about the target vector $\bf{\hat{t}}$ by the antenna azimuth $\phi$. Thus, we define :

$$
\hat{e}_{\phi}=\displaystyle\frac{\mathbf{\hat{z}}\times\mathbf{\hat{t}}}{||\mathbf{\hat{z}}\times\mathbf{\hat{t}}||}=\frac{(\mathbf{\hat{x}}\times\mathbf{\hat{y}})\times\mathbf{\hat{t}}}{||(\mathbf{\hat{x}}\times\mathbf{\hat{y}})\times\mathbf{\hat{t}}||}=\frac{\mathbf{\hat{y}}(\mathbf{\hat{t}}\cdot\mathbf{\hat{x}})-\mathbf{\hat{x}}(\mathbf{\hat{t}}\cdot\mathbf{\hat{y}})}{||\mathbf{\hat{y}}(\mathbf{\hat{t}}\cdot\mathbf{\hat{x}})-\mathbf{\hat{x}}(\mathbf{\hat{t}}\cdot\mathbf{\hat{y}})||}
$$ (eq193)

$$
\hat{e}_{\theta}=\displaystyle (\mathbf{\hat{z}}\times\mathbf{\hat{t}})\times \mathbf{\hat{t}}
$$ (eq194)

For convenience, we also define the corresponding unnormalized polarization vectors:

$$
e_{\phi}=\displaystyle \mathbf{\hat{y}}(\mathbf{\hat{t}}\cdot\mathbf{\hat{x}})-\mathbf{\hat{x}}(\mathbf{\hat{t}}\cdot\mathbf{\hat{y}})
$$ (eq195)

$$
e_{\theta}=\displaystyle (\mathbf{\hat{z}}\times\mathbf{\hat{t}})\times\mathbf{\hat{t}}=(\mathbf{\hat{z}}\cdot\mathbf{\hat{t}})\mathbf{\hat{t}}-\mathbf{\hat{z}}
$$ (eq196)

which both have the same length, given by $||\mathbf{\hat{y}}(\mathbf{\hat{t}}\cdot\mathbf{\hat{x}})-\mathbf{\hat{x}}(\mathbf{\hat{t}}\cdot\mathbf{\hat{y}})||$. For simplicity, we will use these latter two vectors, rather than the normalized vectors, in what follows. The Ludwig-3 unnormalized components are defined in terms of the preceding unnormliazed vectors by a rotation by the target azimuth in the antenna frame. This rotation is defined so that at boresight, the resulting vectors are now a function of azimuth $\phi$:

$$
\mathbf{L_x}'=e_{\theta}\cos\phi-e_{\phi}\sin\phi
$$ (eq197)

$$
\mathbf{L_y}'=e_{\theta}\sin\phi+e_{\phi}\cos\phi
$$ (eq198)

Now $\cos⁡\phi$ and $\sin⁡\phi$ can be expressed in terms of the target vector and the cartesian basis vector as follows:

$$
\cos⁡\phi=-\mathbf{\hat{y}}\cdot\displaystyle\left[\frac{\mathbf{\hat{t}}\times\mathbf{\hat{z}}}{||\mathbf{\hat{t}}\times\mathbf{\hat{z}}||}\right]
$$ (eq199)

$$
\sin⁡\phi=-\mathbf{\hat{x}}\cdot\displaystyle\left[\frac{\mathbf{\hat{t}}\times\mathbf{\hat{z}}}{||\mathbf{\hat{t}}\times\mathbf{\hat{z}}||}\right]
$$ (eq200)

The normalized Ludwig-3 basis vectors are:

$$
\mathbf{\hat{L}_x}'=\mathbf{L_x}'/||\mathbf{L_x}'||
$$ (eq201)

$$
\mathbf{\hat{L}_y}'=\mathbf{L_y}'/||\mathbf{L_y}'||
$$ (eq202)

Given a target/satellite position with angles $(\theta_e,\phi_e)$ and $(\theta_s,\phi_s)$, both 

- the surface polarization basis vectors $(\hat{h},\hat{v})$ 

and 

- Ludwig-3 basis $(\hat{L_x}',\hat{L_y}')$

can be determined with the previous equations. To find the clockwise basis rotation of the surface basis into the Ludwig-3 basis, we note that this corresponds to a counterclockwise rotation of the electric field vector itself, and so :

$$
\begin{pmatrix}
E_{x} \\ 
E_{y} \\
\end{pmatrix}=\begin{pmatrix}
\mathbf{\hat{L}_x}'\cdot\mathbf{\hat{h}} & \mathbf{\hat{L}_x}'\cdot\mathbf{\hat{v}}\\ 
\mathbf{\hat{L}_y}'\cdot\mathbf{\hat{h}} & \mathbf{\hat{L}_y}'\cdot\mathbf{\hat{v}}\\
\end{pmatrix}
\begin{pmatrix}
E_{h} \\ 
E_{v} \\
\end{pmatrix}=
\begin{pmatrix}
\cos\alpha' & -\sin\alpha'  \\ 
 \sin\alpha' & \cos\alpha' \\ 
\end{pmatrix}
\begin{pmatrix}
E_{h} \\ 
E_{v} \\
\end{pmatrix}
$$ (eq203) 

Therefore, we have :

$$
\mathbf{\hat{L}_x}'\cdot\mathbf{\hat{h}}=\cos\alpha'
$$ (eq204)

$$
\mathbf{\hat{L}_x}'\cdot\mathbf{\hat{v}}=-\sin\alpha'
$$ (eq205)

and so, the polarization rotation angle $\alpha'$ may be computed as :

$$
\alpha'=\mathrm{atan2}(-\mathbf{\hat{L}_x}'\cdot\mathbf{\hat{v}},\mathbf{\hat{L}_x}'\cdot\mathbf{\hat{h}})
$$ (eq206)


### Faraday rotation angle


The polarization vector of an electromagnetic wave of frequency $f$ [Hertz] in the microwave range that propagates from the Earth to the S/C through the geomagnetic field and the Earth’s ionosphere undergoes a rotation (Faraday rotation) by the angle $\Omega$ ({cite:p}`yueh2000estimates`;{cite:p}`Meissner2006`):

$$
\Omega=(135⁄f^2 )\int n_e \vec{B}_{geo} \cdot d\vec{s}
$$ (eqFara1)

where $n_e$ is the free inospheric electron density [$m^{-3}$]. $\vec{B}_{geo}$ is the geomagnetic field vector [Gauss] and $d\vec{s}$ is the vector line element in the direction of propagation. When looking into the propagation direction of the electromagnetic wave, the electric field polarization vector rotates clockwise if $\Omega>0$, i.e., if the geomagnetic field is pointing along the direction of propagation. The Faraday rotation corresponds to the Stokes vector transformation

$$
\begin{eqnarray}
\left(
\begin{matrix}
I'_{hv} \\
Q'_{hv} \\
U'_{hv} \\
V'_{hv} \\
\end{matrix}
\right)
=
\left(
\begin{matrix}
                 1 &               0 &              0  &              0 \\
                 0 &   \cos(2\Omega) &   \sin(2\Omega) &              0 \\
                 0 &  -\sin(2\Omega) &   \cos(2\Omega) &              0 \\
                 0 &               0 &              0  &              1 \\
\end{matrix}
\right)
\left(
\begin{matrix}
I_{hv} \\
Q_{hv} \\
U_{hv} \\
V_{hv}
\end{matrix}
\right).
\end{eqnarray}
$$ (eq:rot1)

The corresponding transformation of the modified Stokes vector is
$$
\begin{equation}
\left(
\begin{matrix}
T'_{h}\\
T'_{v}\\
U'    \\
V'    \\
\end{matrix}
\right)=
\left(
\begin{matrix}
(I'_{hv}-Q'_{hv})/2 \\
(I'_{hv}+Q'_{hv})/2 \\
U'                 \\
V'                 \\
\end{matrix}
\right)=
\left(
\begin{matrix}
           \cos^2\Omega &              \sin^2\Omega &     -\cos\Omega\sin\Omega &                    0 \\
           \sin^2\Omega &              \cos^2\Omega &      \cos\Omega\sin\Omega &                    0 \\
          \sin(2\Omega) &            -\sin(2\Omega) &             \cos(2\Omega) &                    0 \\
                      0 &                         0 &                        0  &                    1 \\
\end{matrix}
\right)
\left(
\begin{matrix}
T_{h}  \\
T_{v}  \\
U      \\
V      \\
\end{matrix}
\right).
\end{equation}
$$(eq:rot2)

```{figure} faraday.png
--- 
name: faraday.png
---
Diagram showing how the sense of Faraday rotation depends upon the relative directions of the magnetic field and energy propagation. 
Also noted is the expected sense of rotation in each hemisphere.
```

According to [Equation](eqFara1),  the magnitude of the Faraday rotation angle grows with $1/f^2$. For CIMR-like Earth incidence angles and all typical ocean scenes $Q_{hv}>>U_{hv}$. Therefore, according to [Equation](eq:rot1), for typical values of $\Omega$, the relative impact of Faraday rotation on the third Stokes parameter is much larger than on the second Stokes parameter (vertical and horizontal polarizations). For the CIMR instrument, Faraday rotation plays a significant role only for the third Stokes parameter at 1.4, 6.9 and 10.7 GHz.  At 1.4 GHz, the size of the Faraday rotation is more than 50 times larger than at 10.7 GHz. If not corrected, this would lead to a large relative error in the V- and H-pol brightness temperatures and therefore to inaccurate values for the OWV.

In order to compute the Faraday rotation for CIMR orbits we assume a spherical earth (radius km) and use the thin layer approximation ({cite:p}`LeVine2000`), which assumes that all electrons are concentrated at the ionospheric layer at an altitude $h_I$=400 km above mean sea level:

$$
n_e(z,lat,lon)=\delta(z-h_I)VTEC
$$ (eqFara2)

where

$$
VTEC(lat,lon)=\int_0^{h_{S/C}} n_e(z,lat,lon) dz
$$ (eqFara3)

is the Vertical Total Electron Content (VTEC) of the ionosphere between the Earth’s surface and the S/C altitude $h_{S/C}$. We can then substitute the full profile integral [Equation](eqFara1) by

$$
\Omega=VTEC\cdot(\vec{B}_I\cdot\vec{k})\cdot \frac{\partial s(h)}{\partial h}_{h=h_I}
$$ (eqFara4)

which can be further expressed as :

$$
\Omega=(K_f⁄f^2 )\cdot \mathrm{VTEC}(h_{S/C},lat_{400},lon_{400})\cdot B_I\cdot \cos⁡\tilde{\theta}\cdot\mathrm{sec}\psi
$$ (eq207)

where $K_f=1.355\times 10^4\rm{TECU}^{-1}\rm{GHz}^2T^{-1}$, $f$ is the electromagnetic frequency [GHz], VTEC is the vertical total electron content reduced to the satellite altitude
 *$h_{S/C}$* using the formulation of {cite:p}`Floury2007`, $B_I$ is the magnetic field strength [Tesla] evaluated at the ionospheric pierce point (IPP), the point where the ray from the spacecraft to the 
surface crosses 400 km $(lat_{400},lon_{400})$; $\psi$ is the angle the ray makes with the vertical towards the target and $\tilde{\theta}$ is the angle between the magnetic field vector and the ray from spacecraft to the surface. As shown in {numref}`faraday.png`, this angle is generaly larger than 90° in the northern hemisphere (with negative Ω) and less than 90° in the southern hemisphere (with positive Ω).
The reduction of VTEC to satellite altitude is formulated as two equations, one (morning) for local time within 6 hours of 6 a.m., and the other (evening) for local times within 6 hours of 6 p.m.

$$
\mathrm{VTEC}(z=h_{S/C},lat_{400},lon_{400})=$$ 

$$\mathrm{VTEC}(z=\infty,lat_{400},lon_{400})\times[(A_m \cdot F_s+B_m )+C_m \cdot \cos⁡(D_m \cdot C_m \cdot lat_{400}\cdot (\pi/180))]
$$ (eq209)

where $F_s$  is the daily solar flux that can be obtained from daily RSGA files [sfu] and the coefficients $A_m$, $B_m$, $C_m$ and $D_m$ were determined by N. Floury from ESA as provided in Table 5.
The $\mathrm{VTEC}(z=\infty,lat_{400},lon_{400})$ can be obtained from the 1-day forecast produced Centre for Orbit Determination in Europe (CODE), University of Berne, Switzerland. For future reprocessed OVW products, the VTEC can be obtained from IGS consolidated VTEC.

| Coefficient | Morning value (between 00 and 12 LT) | Evening value (between 12 and 24 LT) |
| :-: | :-: |:-: |
|$A_m$ | $-1.43\times 10^{-4}[\mathrm{sfu}^{-1}]$ | $-9.67\times 10^{-5}[\mathrm{sfu}^{-1}]$ |
|$B_m$ | $8.66\times 10^{-1}[\mathrm{nd}]$ | $8.76\times 10^{-1}[\mathrm{nd}]$ |
|$C_m$ | $3.75\times 10^{-3}[\mathrm{nd}]$ | $8.98\times 10^{-3}[\mathrm{nd}]$ |
|$D_m$ | $3.7[\mathrm{deg}^{-1}]$ | $2.03[\mathrm{deg}^{-1}]$ |
	Table: Coefficients in Floury TEC Altitude Correction

The Magnetic field vector can be obtained from the 12th generation of the International Geomagnetic Reference Field (IGRF), evaluated at 400 km above the earth's surface along the line of sight using the software provided [here](https://www.ngdc.noaa.gov/IAGA/vmod/igrf12.f), as converted into a callable FORTRAN function available [here](https://gist.github.com/myjr52/62ca6c3e9c78ea0411)
The function outputs magnetic field strength in nanoTeslas (1e-9 Teslas) which is converted into Gauss (1e-4 Teslas). This model is valid to the year 2020 and should be updated when a new version of the model becomes available.
Further information on the derivation of the associated geomagnetic model may be found [here](https://www.ngdc.noaa.gov/IAGA/vmod/igrf.html).


### Total rotation from surface basis to antenna basis

Of
course, Faraday rotation is just one of two rotations necessary to
transport a surface Stokes vector into the instrument basis. The
second rotation, counterclockwise by angle $\alpha'$ looking down
towards the target from the instrument, is associated with the change
of polarization basis from the surface basis to the instrument
basis. For the chosen CIMR geometry conventions, this polarization
basis rotation angle $\alpha'$ is defined with the same sign
convention as that for $\Omega$  so
that

$$\begin{eqnarray}
\left(
\begin{matrix}
E_h^{Ant}\\
E_v^{Ant}
\end{matrix}
\right)
=
\left(
\begin{matrix}
\cos \alpha' & -\sin \alpha'\\
\sin \alpha' &  \cos \alpha'\\
\end{matrix}
\right)
\left(
\begin{matrix}
E'_h\\
E'_v
\end{matrix}
\right)
\end{eqnarray}
$$(eq:rot6)

and

$$
\begin{eqnarray}
\left(
\begin{matrix}
T_{h}^{Ant}  \\
T_{v}^{Ant}  \\
U_{hv}^{Ant} \\
V_{hv}^{Ant} \\
\end{matrix}
\right)
=
\left(
\begin{matrix}
           \cos^2\alpha' &              \sin^2\alpha' &     -\cos\alpha'\sin\alpha' &                    0 \\
           \sin^2\alpha' &              \cos^2\alpha' &      \cos\alpha'\sin\alpha' &                    0 \\
          \sin(2\alpha') &            -\sin(2\alpha') &              \cos(2\alpha') &                    0 \\
                       0 &                          0 &                           0 &                    1 \\
\end{matrix}
\right)
\left(
\begin{matrix}
T_{h}  \\
T_{v}  \\
U_{hv} \\
V_{hv} \\
\end{matrix}
\right).
\end{eqnarray}
$$(eq:rot7)

Considering both angles together we then have

$$
\begin{eqnarray}
\left(
\begin{matrix}
E_h^{Ant}\\
E_y^{Ant}
\end{matrix}
\right)
=
\left(
\begin{matrix}
\cos (\alpha'+\Omega) & -\sin (\alpha'+\Omega)\\
\sin (\alpha'+\Omega) &  \cos (\alpha'+\Omega)\\
\end{matrix}
\right)
\left(
\begin{matrix}
E_h\\
E_v
\end{matrix}
\right)
\end{eqnarray}
$$ (eq:rot8)

and

$$
\begin{eqnarray}
\left(
\begin{matrix}
T_{h}^{ant}  \\
T_{h}^{ant}  \\
U_{hv}^{ant} \\
V_{hv}^{ant} \\
\end{matrix}
\right)
=
\left(
\begin{matrix}
           \cos^2(\alpha'+\Omega) &              \sin^2(\alpha'+\Omega) &     -\cos(\alpha'+\Omega)\sin(\alpha'+\Omega) &                    0 \\
           \sin^2(\alpha'+\Omega) &              \cos^2(\alpha'+\Omega) &      \cos(\alpha'+\Omega)\sin(\alpha'+\Omega) &                    0 \\
           \sin 2(\alpha'+\Omega) &             -\sin 2(\alpha'+\Omega) &                        \cos 2(\alpha'+\Omega) &                    0 \\
                                0 &                                   0 &                                             0 &                    1 \\
\end{matrix}
\right)
\left(
\begin{matrix}
T_{h}^{TOA}  \\
T_{v}^{TOA}  \\
U_{hv}^{TOA} \\
V_{hv}^{TOA} \\
\end{matrix}
\right).
\end{eqnarray}
$$(eq:rot9)

and we define the rotation matrix :

$$
\begin{eqnarray}
\mathbf{\Psi}(\phi)
=
\left(
\begin{matrix}
           \cos^2(\alpha'+\Omega) &              \sin^2(\alpha'+\Omega) &     -\cos(\alpha'+\Omega)\sin(\alpha'+\Omega) &                    0 \\
           \sin^2(\alpha'+\Omega) &              \cos^2(\alpha'+\Omega) &      \cos(\alpha'+\Omega)\sin(\alpha'+\Omega) &                    0 \\
           \sin 2(\alpha'+\Omega) &             -\sin 2(\alpha'+\Omega) &                        \cos 2(\alpha'+\Omega) &                    0 \\
                                0 &                                   0 &                                             0 &                    1 \\
\end{matrix}
\right)
\end{eqnarray}
$$(eq:rot10)

where $\phi=\alpha'+\Omega$.

## Sum of contributions at the Top of the atmosphere and antenna pattern integration

Considering all components of the scene brightness temperature, the complete model solution for $T_{tp}^{TOA}$, in the surface polarization basis, is:

$$
\left(\begin{matrix}
T_{th}^{TOA,RTM} \\ 
T_{tv}^{TOA,RTM} \\
U^{TOA,RTM} \\
V^{TOA,RTM} \\
\end{matrix}\right)=
\left(\begin{matrix}
T_{atm}^{up}+(\tau_d \tau_v \tau_w \tau_I \tau_R )[T_{surf,h}^{tot}+R_{surf,h}^{tot}\cdot T_{atm}^{dw}+T_{sch}+T_{ssh}] \\
T_{atm}^{up}+(\tau_d \tau_v \tau_w \tau_I \tau_R)[T_{surf,v}^{tot}+R_{surf,v}^{tot}\cdot T_{atm}^{dw}+T_{scv}+T_{ssv}] \\
(\tau_d \tau_v \tau_w \tau_I \tau_R ) T_{erU} \\
(\tau_d \tau_v \tau_w \tau_I \tau_R) T_{erV} \\
\end{matrix}\right)
$$ (eq210)
where 

- $T_{atm}^{up}$ and $T_{atm}^{dw}$ are the unpolarized upwelling and downwelling brightness temperature of atmospheric 1-way emission which can be derived from [Equation](#eq2) and [Equation](#eqatm84),
- $\tau_d$ is the 1-way atmospheric transmittance associated with molecular oxygen absorption, determined from [Equation](#eqatm71),
- $\tau_v$ is the 1-way atmospheric transmittance associated with water vapor absorption, determined from [Equation](#eqatm71),
- $\tau_w$ is the 1-way atmospheric transmittance associated with cloud liquid water absorption, determined from [Equation](#eqatm71),
- $\tau_I$ is the 1-way atmospheric transmittance associated with cloud ice absorption, determined from [Equation](#eqatm71),
- $\tau_R$ is the 1-way atmospheric transmittance associated with rain absorption, determined from [Equation](#eqatm71),
- $T_{surf,p}^{tot}$ and $R_{surf,p}^{tot}$, the p-pol brightness temperature, and reflectivity, of the total sea surface emission, including specular emission determined from [Equation](#eq19),[Equation 39](#eq20); rough and foamy sea surface induced emission from [Equation 43](#eq:rough4) to [Equation 46](#eq:rough7),
- $T_{erU}$	and $T_{erV}$ are the third and fourth Stokes brightness temperature of rough surface emission, respectively, determined in from [Equation 46](#eq:rough7) 
- $T_{scp}$	is the p-pol brightness temperature of scattered celestial sky radiation (not part of the present algorithm, see for L-band the L2SSS ATBD's dedicated [page](https://cimr-algos.github.io/L2SSS/baseline_algorithm_definition.html#sea-surface-scattered-celestial-sky-radiation-contribution)),
- $T_{ssp}$, is the p-pol brightness temperature of scattered solar radiation (sunglint), (not part of the present algorithm, see for L-band the L2SSS ATBD's dedicated [page](https://cimr-algos.github.io/L2SSS/baseline_algorithm_definition.html#sea-surface-scattered-solar-sunglint-contributions)).

Note that in order to be able comparing CIMR data and the RTM solutions, one finally need to integrate the $T_{tp}^{TOA,RTM}$ over the CIMR antenna patterns:

$$
T_{tp}^{TOA,RTMi}=\displaystyle\frac{1}{4\pi}\int_{\it{Earth}}\mathbf{G(b)}\mathbf{\Psi}(\phi)T_{tp}^{TOA,RTM}\frac{\partial \Omega}{\partial A}dA
$$ (eq210b)

The integral is over the surface of the earth visible to the sensor, where the differential surface area is $dA$ and $d\Omega$ is the differential solid angle. The ratio of the differential solid angle to the differential surface area is
 
$$
\frac{\partial \Omega}{\partial A}=f_{lat}\frac{\cos\theta_s}{r^2}
$$ (eq210c)

where $\theta_s$ is the incidence angle and $r$ is the range. For a spherical Earth, the leading term $f_{lat}$ would be unity. However, the Earth is modeled as an oblate spheroid and as a consequence this term is a function of latitude, deviating about ±1% from unity. The matrix $G$ is a 4×4 matrix describing the antenna gain function. Each element in this matrix is a function of the look direction $\mathbf{b}$ which  is the unit vector pointing from the antenna to $dA$. The term $\mathbf{\Psi}(\phi)$ is the rotation matrix defined in previous section ([Equation (165)](#eq:rot10)).



## CIMR Leve1b re-sampling approach

We recommend the Backus-Gilbert (BG) Optimum Interpolation for the CIMR Leve1b re-sampling approach, which is an established and widely used method for sampling and gridding passive microwave satellite data ({cite:p}`Poe1990`). It finds a set of weights $A_i$ in the neighborhood of a chosen synthetic target footprint and computes the antenna temperature $T_A$ of the target $T_{A,rsp}$, as weighted sum of the individual observations $T_{A,i}$:

$$
T_{A,rsp}=\sum_{i} A_i\cdot  T_{A,i}
$$ (eq211)

The weights $A_i$ are determined by minimizing the least square deviation of the fit:

$$
Q=\int\int [G_T(x,y)-\sum_i A_i \cdot G_i(x,y)]^2 dx dy
$$ (eq212)

between the chosen target response (gain) GT and the resampled gain. The index $i$ runs over all samples in the neighborhood of the target cell that have a sufficiently large weight $A_i$ to be included in the average $T_{A,rsp}$. On can include all samples within a 180 km radius of the target cell.
 
Carrying out this optimization requires the computation of the normalization integral 

$$
u_i=\int \int G_i(x,y) dxdy
$$ (eq213)

and the two overlap integrals

$$
v_i=\int \int G_T(x,y)\cdot G_i(x,y) dxdy
$$ (eq214)

$$
g_{ij}=\int \int G_T(x,y)\cdot G_i(x,y)+\beta\cdot\delta_{ij} dxdy
$$ (eq215)

The gain functions $G_i(x,y)$ of the individual CIMR observations are given by the pre-launch measured antenna patterns of the CIMR multi-frequency chanels and are the individual CIMR gain patterns of the effective field of view (EFOV) of 36 x 64 km for L-band, 11x19 km for C-band, 7x13 km for X-band, 4x6 km for Ku-band and 3x5 km 
for Ka-band. 

The result of the optimization can be summarized as follows (using vector/matrix notation, the superscript *T* denotes the transposed vector):

$$
\mathbf{A}=\mathbf{g}^{-1}\cdot[\mathbf{v}+\displaystyle\frac{(1-\mathbf{u}^{T}\cdot\mathbf{g}^{-1}\cdot\mathbf{v})}{\mathbf{u}^{T}\cdot\mathbf{g}^{-1}\cdot\mathbf{u}}\mathbf{u}]
$$ (eq216)

The parameter $\beta$ is a small smoothing parameter. Its value is chosen to optimize the noise reduction factor $NRF=\sum_i A_i^2$ compared to the orginal gain  pattern $g_i(x,y)$ in a tradeoff for the quality of fit $Q$. A smaller/larger value for $\beta$ results in a better/worse fit value $Q$ and in a worse/better $NRF$. 

The values of the resampling weights  $A_i$ , the fit $Q$ and the $NRF$ depend all on the scanning geometry and the scan azimuth angle.

The target cells for the CIMR L2OWV products at Moderate spatial Resolution are centered on the center points of a fixed $0.15^{\circ}$ Earth grids whose vertices are located at $0^{\circ},0.15^{\circ},0.3^{\circ}$, ....
longitude and at $0^{\circ},\pm 0.15^{\circ},\pm 0.30^{\circ}$, ..., latitude. For the CIMR L2OWV products at Low spatial Resolution, the data
 are centered on the center points of a fixed $0.4^{\circ}$ Earth grids whose vertices are located at $0^{\circ},0.4^{\circ},0.8^{\circ}$, ....
longitude and at $0^{\circ},\pm 0.4^{\circ},\pm 0.80^{\circ}$, ..., latitude.
The target gain patterns $g_i$ are the same as the original EFOV Ka-, ku-, X-, C- and L-band footprints. For the smoothing factor $\beta$ a value of 0.5 is chosen. 
This results in an average NRF of about 0.4.

The BG OI that can be applied in the CIMR L1B processing of the OVW retrieval algorithm can actually be done in two steps. The first step in the resampling is to take a single scan and adjustment the position of the observations to corresponds to integer azimuth angles (i.e. $0^{\circ}$ to $359^{\circ}$). The sampling in the along-scan direction well exceeds Nyquist sampling, and therefore the fit accuracy of the resampled data shall be very high. The second step is the resampling onto either the fixed $0.15^{\circ}\times 0.15^{\circ}$ or $0.4^{\circ}\times 0.4^{\circ}$ grids. 

## Ocean Wind Vector inversion algorithm

## Ocean Wind Vector inversion algorithm: a 2-step algorithm

For the algorithm applicable in the 'general atmospheric condition', i.e., for rain-free atmosphere and $U_{10}$ < 17 m/s and low rain rates (RR < 2 mm/h), the input data are CIMR Level 1b channel resampled four Stokes parameters for the aft- and fore-view of the instrument at the Top of the Atmosphere for the 4 highest frequencies (C- to Ka-bands), namely, $T_{th}^{TOA}$, $T_{tv}^{TOA}$, $U^{TOA}$, and $V^{TOA}$, properly resampled on the CIMR Level 1b X-band channel FWHM resolution (~15 km). Other needed input data from CIMR are the retrieved L2 sea surface temperature and sea surface salinity, also properly resampled on the CIMR Level 1b X-band channel FWHM resolution (~15 km). In case these two variables are not available, the algorithm will also rely on ECMWF weather forecasts and CMEMS ocean model. ECMWF forecasts will also provide an ensemble of auxiliary data (vertical profiles of temperature, water vapor, etc.) needed for evaluating the atmospheric corrections.

---

In this ATBD, we propose a two-step OWV retrieval:

1. **Step 1:** Retrieval of ocean surface wind speed modulus $U_{10}^{ret}$ (and of the SST $T_{s}^{ret}$) from the 16 input linearly polarized Tbs at C-, X-, Ku-, and Ka-band channel data, namely $T_{th}^{TOA}$ and $T_{tv}^{TOA}$, for aft and fore views.

2. **Step 2:** Retrieval of ocean surface wind direction from the 8 input C- and X-band channels 3rd and 4th Stokes parameters $U^{TOA}$ and $V^{TOA}$ for aft and fore views, as well as the surface wind speed $U_{10}^{ret}$ and SST $T_{s}^{ret}$ retrieved at the previous step.


### Step 1: Ocean Wind Speed inversion algorithm

To retrieve the surface wind speed vector modulus, we use a Bayesian inversion approach in which the posterior distribution of the retrieved wind speed, and of the SST: $\mathcal{P}$ is taken to be the product of the likelihood function  $\mathcal{L}$ and prior distribution functions $P$ and $P'$ for wind speed and SST, respectively:

$$
\mathcal{P}(\tilde{u}_{10}|T_p; \tilde{T}_s|T_p; \sigma_u, u_{10p}, \phi_{wp}, \sigma_T, T_{sp}) = \mathcal{L}(\tilde{u}_{10}, \tilde{T}_s, T_p, \phi_{wp}) \cdot P(\tilde{u}_{10}|\sigma_u, u_{10p}) \cdot P'(\tilde{T}_s|\sigma_T, T_{sp}) \quad (Eq.175)
$$

where:
- $\mathcal{P}$ is the posterior distribution of the retrieved wind speed,
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

As discussed in {cite:p}`Monahan2018`, the bivariate Rice distribution for wind speed follows from assuming that the wind components have Gaussian and isotropic fluctuations. The prior distribution for wind speed can thus take the form of a Rice distribution:

$$
P(\tilde{u}_{10}|\sigma_u, u_{10p}) = \frac{\tilde{u}_{10}}{\sigma_u^2} \exp\left( -\frac{\tilde{u}_{10}^2 + u_{10p}^2}{2\sigma_u^2} \right) \cdot I_0\left(\frac{\tilde{u}_{10} u_{10p}}{\sigma_u^2}\right) \quad (Eq.176)
$$

where $I_0$ is the modified Bessel function of the first kind with order zero.

---

For the prior distribution of SST, one can assume a Gaussian distribution:

$$
P'(\tilde{T}_s|\sigma_T, T_{sp}) = \frac{1}{2\pi\sigma_T^2} \exp\left( -\frac{(\tilde{T}_s - T_{sp})^2}{2\sigma_T^2} \right) \quad (Eq.177)
$$

In fact, while SST displays nonzero skewness and kurtosis ({cite:p}`Sura2008`), these non-Gaussian features are sufficiently modest that the specification of Gaussian fluctuations in SST is a reasonable first approximation.

Alternatively, these two distributions can also be set to $P = P' = 1$, to give zero impacts of priors on the end retrievals.

The likelihood function $\mathcal{L}$ is computed using the previously described RTM, here represented by the geophysical model function $G$, and can be evaluated using (Eq.166) and the input CIMR TOA Tbs $T_p$:

$$
\mathcal{L}(\tilde{u}_{10}, \tilde{T}_s, T_p, \phi_{wp}) = \prod_{i=1}^n \exp\left( -\frac{(T_{pi} - G(\tilde{u}_{10}, \tilde{T}_s, \phi_{wp}))^2}{2\sigma_{pi}^2} \right) \quad (Eq.178)
$$

where $\sigma_{pi}$ is the standard deviation of the CIMR TOA Tbs.

The nominal Bayesian wind speed and SST solution are then taken to be the Maximum Likelihood Estimate (MLE).

$$
(U_{10}^{ret}, T_s^{ret}) = arg_{max(u_{10}, T_s)} \mathcal{P}(\tilde{u}_{10}|T_p, \tilde{T}_s|T_p, \sigma_u, u_{10p}, \phi_{wp}, \sigma_T, T_{sp}) \quad (Eq.179)
$$

This non-linear problem is solved iteratively using a Levenberg-Marquardt ({cite:p}`Marquardt1963`) algorithm to find the local maxima.

Note that when retrieving wind speed and SST, the wind direction $\phi_{pp}$, which is used to evaluate the RTM in the geophysical model function $G$, can be taken to be a prior from ECMWF forecast fields. In our Bayesian retrieval algorithm, we choose to re-evaluate internally the CIMR SST together with the surface wind speed instead of fixing it with the value of the L2SST retrievals for two main reasons:

1. Using the L2 CIMR retrieved SST as a first guess, the combined Bayesian retrieval might produce a different retrieved SST than the Level 2 SST. Retrieving both parameters together shall ensure that both the retrieved SST and the surface wind speed are coherent with respect to the forward RTM predictions.

2. Given the significant sensitivity of the C-band channel to SST with respect to its sensitivity to wind speed (particularly in V-pol): any small change in the SST or wind speed will have to be accounted for proper evaluation of the geophysical model function $G$.

---

### Step 2: Ocean Wind Direction Inversion Algorithm

In a second step, the algorithm aims at retrieving the wind direction, $\phi_{pp}^{ret}$, using as input 8 datasets corresponding to C- and X-band channels 3rd and 4th Stokes parameters for both aft and fore views:

$$
T_p = [U_C^{TOA,fore}, V_C^{TOA,fore}, U_C^{TOA,aft}, V_C^{TOA,aft}, U_X^{TOA,fore}, V_X^{TOA,fore}, U_X^{TOA,aft}, V_X^{TOA,aft}]
$$

The algorithm also uses as input the surface wind speed $U_{10}^{ret}$ and temperature $T_s^{ret}$, retrieved from step 1.

To retrieve the surface wind speed vector direction, we use a Bayesian inversion approach in which the posterior distribution of the retrieved wind direction $\tilde{\phi}_{w}$. $P'$ is taken to be the product of the likelihood function $\mathcal{L}'$ and prior distribution functions $P''$ for wind direction:

$$
\mathcal{P}'(\tilde{\phi}_{w}|T_p, \sigma_u, U_{10}^{ret}, T_s^{ret}, \sigma_T) = \mathcal{L}'(\tilde{\phi}_{w}, U_{10}^{ret}, T_s^{ret}, T_p, \phi_{wp}) \cdot P''(\tilde{\phi}_{w}|\phi_{w}, U_{10}^{ret}) \quad (Eq.180)
$$

The likelihood function $\mathcal{L}'$ is computed using the RTM, here represented by the geophysical model function $G$, and can be evaluated using (Eq.166) and the input CIMR TOA 3rd and 4th Stokes Tbs $T_p$:

$$
\mathcal{L}'(\tilde{\phi}_{wp}, U_{10}^{ret}, T_s^{ret}, T_p, \phi_{wp}) = \prod_{i=1}^{n} \exp\left( -\frac{(T_p^i - G(\tilde{\phi}_{w}, U_{10}^{ret}, T_s^{ret}))^2}{2\sigma_{pi}^2} \right) \quad (Eq.181)
$$

where $\sigma_{pi}$ is the standard deviation of the CIMR TOA 3rd and 4th Stokes parameters.

The nominal Bayesian wind direction solution is then taken to be the Maximum Likelihood Estimate (mode of the posterior distribution), following:

$$
\phi_{w}^{ret} = arg_{max(\phi)} \mathcal{P}'(\tilde{\phi}_{w}|T_p, \sigma_u, U_{10}^{ret}, T_s^{ret}, \sigma_T) \quad (Eq.182)
$$

We apply the conjugate gradient technique using a modified Levenberg-Marquardt (1963) algorithm to find the local minima. The wind speed vector solution to this constrained minimization problem is the final L2B retrieval.

For the two-look retrieval, the MLE typically finds 2–3 minima, called ambiguities. This is most likely to occur when the dependence of $T_B$ on the relative wind direction is small, which happens at low wind speeds.

When an OWV solution is ambiguous, spatial information can be used to break the ambiguity. Median filtering has a long history in OWV retrieval ({cite:p}`hilburn2015ocean`). It is important to understand that the wind vectors themselves are not being median filtered. Instead, rather than choosing the first-ranked ambiguity, the ambiguity closest to the area-median direction is chosen. The median filter must be initialized with some wind field. One choice is to use the first-ranked ambiguity; however, the best results are obtained using a smoother wind field from numerical weather prediction.

This does raise the potential of selecting the wrong solution if the numerical weather prediction winds do not have the same meteorological features in the same locations as observed by the satellite. For the purpose of this ATBD, the selected ambiguity refers to the ambiguity resulting from the median filtering process initialized with wind direction from ECMWF. The benefit of a two-look configuration is increased resilience to errors in measured $T_B$ and in the RTM $T_B$.


The input data from CIMR are the "eight-flavors" CIMR Leve1b chanel resampled four stokes parameters for the aft- and fore view of the instrument at the Top of the Atmosphere for the 5 frequencies, namely, $T_{th}^{TOA}$, $T_{tv}^{TOA}$, $U^{TOA}$, and $V^{TOA,aft}$. Other input data from CIMR are the L2 sea surface temperature and sea surface salinity, also properly resampled on the CIMR Leve1b X-band channel grid. In case, these two variables are not available, the algorithm will also rely on ECMWF weather forecasts and CMEMS model. It will also provide an ensemble of auxilliary data (vertical profiles of temperature, water vapor, etc..) needed for evaluating the atmospheric corrections.

In the proposed processing, we allow the wind speed vector to vary within a region about the a priori wind speed, direction and surface temperature and salinity (which shall be derived from the multi-frequency chanels of CIMR, or, from a numerical weather or ocean forecasts such as ECMWF and CMEMS) via additional penalty terms in the objective function while leaving the wind vector unconstrained. To retrieve OWV, we will use a Maximum-likelihood method with the following objective sum of square function:

$$
\chi^2(U_{10},\phi_{w})=\displaystyle\sum_f\sum_i\sum_p \left[\frac{T_{f,p,ti}^{TOA,CIMR}-T_{f,p,ti}^{TOA,RTM}(U_{10},\phi_{w},T_{s}^{p},S^{p},V,L,\theta_s,\phi_s)}{NEDT_i}\right]^2+\left[\frac{U_{10}-U_{10}^{p}}{\delta_{U_{10}}}\right]^2+\left[\frac{\phi_{w}-\phi_{w}^{p}}{\delta_{\phi_{w}}}\right]^2
$$ (eq:MLE)


The environmental parameters used to calculate RTM $T_B$ include the sea surface temperature $T_s$ and salinity $S$, the surface wind speed $U_{10}$ and wind direction $\phi_{w}$, the columnar water vapor $V$, and columnar cloud liquid water $L$. The Earth incidence angle 𝜃s and the azimuthal look angle $\phi_s$ depend on the channel *i* at frequency $f$ and on whether the observation is from forward or backward look. The sum in [Equation](eq:MLE) runs over all channels of the five polarimetric frequency bands: 1.4, 6.9, 10.7, 18.7, and 36.5 GHz. The inverse weights of these channels are the expected variances, i.e., squares of the expected errors. The weighting factors for the CIMR data are set according to the expected measurement and modeling uncertainties. We let $NEDT_i$ be the Noise-Equivalent-Delta-T (NEDT) of the radiometer chanel *i* at frequency *f*. 

The variables $U_{10}^{p}$, $\phi_{w}^{p}$, $S^{p}$ and $T_{s}^{p}$ are the *a priori* values for the auxilliray surface wind speed, wind direction (with uncertainties $\delta_{U_{10}}$, $\delta_{\phi_{w}}$), salinity and temperature, respectively. 

We apply the conjugate gradient technique using a modified Levenberg-Marquardt algorithm {cite:p}`Marquardt1963` to find the local minima. The wind speed vector solution to this constrained minimization problem is the final L2B retrievals.

For the two-look retrieval, the MLE typically finds 2–3 minima, called ambiguities. The ambiguities are ranked by the value of chi-square in ascending order. Thus, the first-ranked ambiguity is the solution with the smallest chi-square residual. If there were no errors in the measured $T_B$ or in the RTM $T_B$, then the first-ranked ambiguity would always be the correct solution. However, the presence of errors can cause incorrect solutions to have the lowest chi-square value. This is most likely to occur when the dependence of $T_B$ on the relative wind direction is small, which happens at low wind speeds

When an OVW solution is ambiguous, spatial information can be used to break the ambiguity. Median fil a long history in OVW retrieval {cite:p}`hilburn2015ocean`. It is important to understand that the wind vectors themselves are not being median filtered. Insted, rather than choosing the first-ranked ambiguity, the ambiguity closest to the area-median direction is chosen. The median filter must be initialized with some wind field. One choice is to use the first-ranked ambiguity; however, the best results are obtained using a smoother wind field from numerical weather prediction. This does raise the potential of selecting the wrong solution if the numerical weather prediction winds do not have the same meteorological features in the same locations as observed by satellite. For the purpose of this ATBD, the selected ambiguity refers to the ambiguity resulting from the median filtering process initialized with winds from ECMWF. The benefit of a two-look configuration is increased resilience to errors in measured $T_B$ and in the RTM $T_B$.