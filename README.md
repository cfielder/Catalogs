# Catalogs
[![Python 3.7](https://img.shields.io/badge/python-v3.7-blue)](https://www.python.org/downloads/release/python-3710/)
[![astropy](http://img.shields.io/badge/powered%20by-AstroPy-orange.svg?style=flat)](http://www.astropy.org/)
![GitHub last commit](https://img.shields.io/github/last-commit/cfielder/Catalogs.svg)

Catalogs associated with paper: A UV-IR Portrait of the Milky Way

## Installing

### Directly from Repository

`git clone https://github.com/cfielder/Catalogs`

## Usage
This is a set of a few catalogues utilised in our analyses that we have provided for those interested in the data. If using 
for your own work please be sure to provide proper credit to us and the sources of the original data. 
Data in these catalogues originates from:
  - SDSS DR8 and DR16: https://www.sdss.org
  - The Galex-SDSS-Wise-Legacy catalog 2: https://salims.pages.iu.edu/gswlc/
  - Galaxy Zoo 2: https://data.galaxyzoo.org
  - Legacy DR8: https://www.legacysurvey.org
  - The MPA-JHU catalog: https://www.sdss.org/dr12/spectro/galaxy_mpajhu/
  - The Simard Bulge-Disk decomposition catalog: https://ui.adsabs.harvard.edu/abs/2011ApJS..196...11S/abstract

The additional catalogs have been cross matched with the SDSS DR8 volume-limited sample constructed in https://ui.adsabs.harvard.edu/abs/2015ApJ...809...96L/abstract

## Catalog Description
### "Vollim_Simard_Salim_GZ2_Cross_match.pkl"
The base cross-matched catalog used in our work. Does not contain restframe WISE bands.

### "Vollim_Simard_Salim_GZ2_Cross_match_Legacykcornorth.pkl"
The final cross-matched catalog containing additionaly matches to Legacy North, with calculated k-corrections for WISE bands.
See Fielder et al. 2020 for details on the k-correction calculation.

### "Vollim_Simard_Salim_GZ2_Cross_match_Legacykcorsouth.pkl"
The final cross-matched catalog containing additionaly matches to Legacy South, with calculated k-corrections for WISE bands.
See Fielder et al. 2020 for details on the k-correction calculation.

## Catalog Implementation
**Read in the catalogs**
```
import pandas as pd
north_catalog = pd.read_pickle(Catalog / path / "Vollim_Simard_Salim_GZ2_Cross_match_Legacykcornorth.pkl")
```

For those interested in photometry NOT in WISE, it is sufficient to concatenate the North and South catalogs and do further 
analyses.
```
cross_matched_catalog = pd.concat([north_catalog, south_catalog])
```

**Column Description**
Please note that any photometry originating from the GSWLC catalog is offset by 5logh from the other photometry by h=0.7.
Non GSWLC photometry is presented assuming a hubble constant H0 = 100 (km/s)/Mpc. To match GSWLC photometry to the other 
photometry simply subtract 5log(0.7).
To match the other photometry to GSWLC simply add 5log(0.7).

Available columns:
```
['dr8_RA', 'dr8_Dec', 'dr8_fiberid', 'dr8_mjd', 'dr8_plate', 'redshift', 'redshift_err', 'AB_EXP', 'FRACPSF', 
'SPECPRIMARY', 'cmodel_M_u', 'cmodel_M_u_z0P1', 'model_M_u', 'model_M_u_z0P1', 'cmodel_M_g', 'cmodel_M_g_z0P1', 
'model_M_g', 'model_M_g_z0P1', 'cmodel_M_r', 'cmodel_M_r_z0P1', 'model_M_r', 'model_M_r_z0P1', 'cmodel_M_i', 
'cmodel_M_i_z0P1', 'model_M_i', 'model_M_i_z0P1', 'cmodel_M_z', 'cmodel_M_z_z0P1', 'model_M_z', 'model_M_z_z0P1', 
'cmodel_M_U', 'cmodel_M_U_z0P1', 'model_M_U', 'model_M_U_z0P1', 'cmodel_M_B', 'cmodel_M_B_z0P1', 'model_M_B', 
'model_M_B_z0P1', 'cmodel_M_V', 'cmodel_M_V_z0P1', 'model_M_V', 'model_M_V_z0P1', 'cmodel_M_R', 'cmodel_M_R_z0P1', 
'model_M_R', 'model_M_R_z0P1', 'cmodel_M_I', 'cmodel_M_I_z0P1', 'model_M_I', 'model_M_I_z0P1', 'gmr', 'umg', 'umr', 
'imz', 'logmass', 'sigma_logmass', 'sfr', 'sigma_sfr', 'mass_to_light_u', 'mass_to_light_u_z0P1', 'mass_to_light_g', 
'mass_to_light_g_z0P1', 'mass_to_light_r', 'mass_to_light_r_z0P1', 'mass_to_light_i', 'mass_to_light_i_z0P1', 
'mass_to_light_z', 'mass_to_light_z_z0P1', 'mass_to_light_U', 'mass_to_light_U_z0P1', 'mass_to_light_B', 
'mass_to_light_B_z0P1', 'mass_to_light_V', 'mass_to_light_V_z0P1', 'mass_to_light_R', 'mass_to_light_R_z0P1', 
'mass_to_light_I', 'mass_to_light_I_z0P1', 'B_T_r', 'e_B_T_r', 'Rd', 'e_Rd', 'FUV', 'e_FUV', 'fabs', 'NUV', 'e_NUV', 
'nabs', 'nabs_err', 'u', 'e_u', 'uabs', 'g', 'e_g', 'gabs', 'r', 'e_r', 'rabs', 'i', 'e_i', 'iabs', 'z', 'e_z', 
'zabs', 'J', 'e_J', 'jabs', 'H', 'e_H', 'habs', 'K', 'e_K', 'kabs', 'W1', 'e_W1', 'W2', 'e_W2', 'W3', 'e_W3', 'W4', 
'e_W4', 'salim_sfr', 'salim_sfr_err', 'salim_mass', 'salim_mass_err', 'salim_RA', 'salim_Dec', 'salim_z', 'bar_probability', 
'faceon_probability', 'feature_probability', 'expABErr_r', 'bass_offset', 'decam_offset', 'salim_distance', 
'salim_distance_mod', 'r_mAB', 'W1_mAB', 'e_W1_mAB', 'W2_mAB', 'e_W2_mAB', 'W3_mAB', 'e_W3_mAB', 'W4_mAB', 'e_W4_mAB', 
'legacy_RA', 'legacy_DEC', 'legacy_W1', 'legacy_e_W1', 'legacy_W2', 'legacy_e_W2', 'legacy_W3', 'legacy_e_W3', 
'legacy_W4', 'legacy_e_W4', 'legacy_g', 'legacy_r', 'legacy_e_r', 'legacy_z', 'my_restframe_W1', 'my_restframe_W2', 
'my_restframe_W3', 'my_restframe_W4', 'my_restframe_r']
```
Most columns are self-explanatory. ```AB_EXP``` refers to the galaxy axis ratio. The model and cmodel magtiudes are from SDSS. 
Columns with the ending ```_z0P1``` are calculated are redshift z=0.1, while the others are calculated at redshift 0. Those 
ending with ```abs``` are the restframe absolute magnitudes from GSWLC. We also include their accompanying apparent magnitudes 
and errors. ```W1_mAB``` and similar columns are the GSWLC observed photometry converted to AB magnitudes from mJy. ```my_restframe_``` 
refers to our calculations of restframe WISE bands. ```bass_offset``` and ```decam_offset``` are the offsets between Bass and 
Decam r-band from SDSS r-band, which we account for before performing our k-corrections.

## Authors
Catherine Fielder
