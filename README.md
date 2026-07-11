Overview

This project independently validates the ForSpEC (Forensic Sperm Epigenetic Clock) model — developed by Pisarek-Pacek et al. (2026) — on a Korean sperm cell dataset (GSE280299), to assess whether a model trained on Polish/European samples generalises to an East Asian population.
ForSpEC predicts donor age from DNA methylation at just 7 CpG sites in sperm cells, using bisulfite amplicon sequencing with Ion AmpliSeq™ technology. It was originally validated on two American cohorts (GSE185445, N=376; GSE185920, N=1419), achieving MAE values of 4.33 and 5.00 years respectively.

Dataset

Source: NCBI GEO — GSE280299
Population: Korean-Asian males
Samples: 56 sperm cell samples
Age range: 18–70 years
Platform: Illumina Infinium MethylationEPIC (EPIC) array
Reference: So & Lee (2025), Forensic Science International: Genetics


Methods

Downloaded preprocessed beta values from GEO supplementary file (GSE280299_Processed_File.txt.gz)
Extracted exact chronological ages from GEO sample metadata
Applied ForSpEC 7-CpG linear regression model using published coefficients (Table 1, Pisarek-Pacek et al. 2026)
Calculated MAE, RMSE, and Pearson correlation against chronological age
Generated scatter plot (predicted vs chronological age) and residual plot

ForSpEC model coefficients applied (Pisarek-Pacek et al. 2026):
CpGGeneCoefficientcg23335134SLC22A18AS−27.674cg14961598MTMR8+68.752cg03830712—+15.363cg26467528GPANK1−39.898cg14728380SECTM1+219.148cg00534655PURA−15.112cg03347590PITX1−38.965Intercept−157.291

Results

| Metric | Korean cohort (this study, N=56) | American GSE185445 (N=376) | American GSE185920 (N=1419) |
|---|---|---|---|
| MAE (years) | **23.81** | 4.33 | 5.00 |
| RMSE (years) | 34.16 | — | — |
| Pearson R | 0.313 | 0.645 | 0.616 |
| p-value | 0.019 | — | — |

Interpretation

ForSpEC shows dramatically reduced accuracy on the Korean cohort compared to American cohorts, with MAE increasing approximately 5-fold. The weak Pearson correlation (R = 0.313) and systematic underestimation across all age groups suggest the model does not generalise well to Korean sperm methylation patterns.
Two factors likely contribute to this:
1. Population-specific methylation differences — DNA methylation levels at the 7 ForSpEC CpGs appear to differ substantially between Polish/European and Korean populations. This is consistent with published findings showing that epigenetic age predictors trained on one population often perform poorly in others, and directly supports the cross-population validation concern raised by Pisarek-Pacek et al. in their discussion.
2. Normalisation differences — ForSpEC was trained on ssNoob-normalised EPIC array data. The preprocessed file used here may apply a different normalisation pipeline, which could contribute to systematic prediction bias. Future work should apply ssNoob normalisation to the raw IDAT files for a fairer comparison.
These findings suggest that population-specific recalibration or retraining of ForSpEC on East Asian cohorts may be necessary before it can be applied in forensic casework involving Korean or broader Asian populations.

Limitations

Normalisation pipeline of the processed GEO file is unknown and may differ from ssNoob used in the original ForSpEC study
N=56 is a relatively small validation cohort
Raw IDAT files were not processed — future work should validate using ssNoob normalisation via the R minfi package for a direct comparison


References

Pisarek-Pacek A, et al. (2026). ForSpEC: A compact forensic epigenetic age clock for sperm cells with cross-platform validation. Forensic Science International: Genetics, 82, 103426.
So MH & Lee HY (2025). DNA methylation-based semen age prediction using the markers identified in Koreans and Europeans. Forensic Science International: Genetics.

