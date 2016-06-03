# Production Domain Overview

This is the repository containing both the package and the modules for
processing the production domain.

The repository also contains information on the complete processing cycle and
research materials.

---

## Production Domain Cycle

The complete cycle contains 4 stages:

1. **Data collection**

   This phase collects data and inputs from various sources and merge them into
   a single final information set.

   No R module is involved in this phase.

2. **Data validation**

   In this phase, the input data will be checked, corrected and validated prior
   to imputation of missing data. All the process will be automised with
   algorithms.

   The validation is performed by the `Production Input Validation` module.

3. **Imputation**

   In this phase, the missing records will be imputed. All the process will be
   automised with algorithms.

   The imputation is separated into three separate modules. The livestock can be
   imputed directly with the `Impute Livestock` module, while the non-livestock
   commodities requires the building imputed dataset with the `Impute
   non-livestock` before loading them with `Fill non-ivestock`.

4. **Post validation**

   During this phase, the processed dataset will be investigated. It will be
   possible to manually correct imputed values. However, all corrections are
   required to be scientifically justified, mandatorily explained in the
   metadata, and reported to team A for continual improvements of the algorithm.

   After the manual intervention, the execution of the `Balance Production
   Identity` is required to ensure the production is balanced.


![production_workflow_horizontal](https://cloud.githubusercontent.com/assets/1054320/15775155/a8b18c82-2980-11e6-980a-8e223202c793.jpg)


---

## Modules Overview

Currently, there are 5 modules in the production domain.

### Production Input Validation

This module performs both input validation of the production domain, and at the
same auto-correction of data with given rules.

### Impute Livestock

This module performs imputation on the livestock commodities and at the same
time ensure slaughtered animal is synchronised accross all related parent/child
commodities.

### Impute Non-livestock

This module craetes the imputed values for the non-livestock items, however,
does not write back directly to the database. Instead the imputed values are
saved to the shared drive.

### Fill Non-livestock

This module follows the `Impute Non-livestock` module and loads the imputed
value then fill in the imputation value then saves back to the database.

### Balance Production Identity

This module re-calculates the production identity, this ensures the relationship
of `Production = Area Harvested x Yield` holds when new changes are introduced
in the post validation phase.

---

**All work under this repository represents the latest status of development and
   is made public for collaboration purposes. It does not reflect the current
   state of the system and use of the program is at the discretion of the
   users.**
