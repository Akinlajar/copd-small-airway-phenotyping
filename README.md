# COPD Small Airway Phenotyping: Do Discrete Phenotypes Exist?

A research project testing whether small airway remodelling in COPD falls into distinct patient phenotypes or varies continuously, using a histopathology biobank dataset.

> **Write-up only.** The data are governed clinical research data, so no data, code outputs or patient-level figures are published here. Everything below is aggregate and identifier-free.

**Stack:** Python (pandas, scikit-learn, SciPy), Excel

---

## The question
If COPD airways fall into discrete phenotypes, clustering should find stable, biologically meaningful groups. If not, forcing clusters onto the data will produce groups that reflect something else.

## Data and cleaning
- Source: a single unstructured spreadsheet of 1,346 rows × 114 columns across 8 stacked study sections, parsed into a tidy table with study of origin kept as a variable.
- A cleaning protocol agreed with the clinical data owners and logged for audit gave an analysis set of **536 airways from 251 tissue blocks and 129 patients**.
- Faults found and fixed: sign-flipped values, factor-of-10 and factor-of-1,000 entry errors, 11 exact duplicates, and a field-overwrite bug in one study's wall-thickness column.
- A data quality report flagged 37 patients and 24 tissue blocks with conflicting demographics, shared with the data owners along with an agreed fallback subset.

## Methods
- k-means with elbow and silhouette analysis (k = 2 to 10)
- Gaussian Mixture Models compared by BIC (1 to 6 components) on raw and log scales, to test whether discrete groups exist at all
- Paired within-patient analysis of the 52 patients sampled in more than one study
- Within-study standardisation as a correction, kept as a sensitivity analysis
- A confound-free three-variable analysis inside a single study (102 airways, 54 patients)

## Findings
1. **Cluster counts were unstable.** Removing just 2.7% of rows during cleaning moved the apparent best k from 4 to 3.
2. **Clusters tracked study of origin, not biology.** One cluster drew 80% of its airways from a single study, against 26% expected.
3. **The confound was confirmed directly.** In the paired analysis, 13 of 13 informative patients moved in the same direction between studies (sign test p = 0.0002).
4. **Standardisation removed it.** After within-study standardisation, every cluster-by-study cell was within 6 percentage points of expectation.
5. **Clusters describe airways, not patients.** 62.5% of patients with two or more sampled airways had airways in different clusters.

**Conclusion:** small airway remodelling varies along two largely independent continuous axes, with no discrete subgroups. Four lines of evidence agree: scatter geometry, weak silhouette scores, a BIC advantage that collapses under log transformation, and an unstable cluster count.

## Why it matters
A naive analysis would have reported three or four COPD phenotypes. Testing whether structure exists before choosing k, and checking clusters against study of origin, turned a misleading result into a defensible null finding.

## Governance
Data were processed in place on university research storage over VPN, with no local copies. Only aggregate, identifier-free results are shared.

## Author
**Judah Akinlaja**, Health Data Scientist
[LinkedIn](https://www.linkedin.com/in/judah-akinlaja-a10385194) · [Portfolio](https://judahakinlajar.co.uk) · [GitHub](https://github.com/Akinlajar)
