# 🏥 QI-Core Compliant Synthetic Healthcare Dataset (Synthea-Based)

This repository contains synthetic patient data generated using [Synthea](https://github.com/synthetichealth/synthea), customized to produce **QI-Core compliant FHIR Bundles** for Clinical Quality Measure (CQM) evaluation.

## 📦 Dataset Overview

Synthetic patient data is generated for the following locations with 100 patients each:

- **California**
- **New York**

The data includes **FHIR Bundles (QI-Core)**, **CCDA**, **CPCDS**, and **CSV** exports, suitable for payer/clinical analytics and measure evaluation (e.g., HEDIS/eCQM).

## ✅ Features

- ✅ QI-Core compliant FHIR resources using [Flexporter mapping](https://github.com/synthetichealth/synthea/wiki/Flexporter).
- ✅ Condition-focused population using **custom `keep.json` file**:
  - BMI
  - Obesity
  - Diabetes
  - Hypertension
  - Depression
  - Chronic Disease Management
- ✅ Consistent deterministic seed values for reproducibility.
- ✅ Multi-format export: FHIR, CCDA, CPCDS, CSV, Symptoms CSV.

## 🗃 Directory Structure

```
synthea_data/
├── keep_bmi_obesity_diabetes_hypertension_depression_management.json
├── synthea_data_california/
│ ├── ccda/
│ ├── cpcds/
│ ├── csv/
│ ├── fhir/ # QI-Core FHIR Bundles (1 JSON per patient)
│ ├── metadata/
│ └── symptoms/
└── synthea_data_new_york/
│ ├── ccda/
│ ├── cpcds/
│ ├── csv/
│ ├── fhir/ # QI-Core FHIR Bundles (1 JSON per patient)
│ ├── metadata/
│ └── symptoms/
```

## ⚙️ Generation Configuration

**Synthea version**: latest as of July 2025

This dataset was generated using the open-source [Synthea™](https://github.com/synthetichealth/synthea) synthetic patient generator.

To reproduce this dataset or generate your own:

1. Follow Synthea setup instructions here:
   👉 https://github.com/synthetichealth/synthea#installation

2. Clone the repository and build the project using Maven (or download the prebuilt `.jar`).

3. Customize the configuration:
   - Replace `synthea.properties` file inside `src/main/resources` with your own settings (see below).
   - Use Flexporter for exporting QI-Core compliant FHIR resources.
   - Use a custom `keep.json` file to control the disease and condition profiles in the generated population.

Use the following command to generate deterministic QI-Core FHIR bundles:

**Command used**:

```bash
./run_synthea -p 100 -a 18-100 \
  --exporter.pretty_print=false \
  --exporter.years_of_history=3 \
  --generate.only_alive_patients=true \
  -fm src/test/resources/flexporter/qicore_withnotdone.yaml \
  -k ./keep_bmi_obesity_diabetes_hypertension_depression_management.json \
  --exporter.use_uuid_filenames=true \
  --exporter.baseDirectory=synthea_data_california \
  --seed=12345 --clinician_seed=12345 \
  --exporter.csv.export=true \
  California
```

(similar command for New York with seed 123456)

### `synthea.properties` Customization

```properties
exporter.ccda.export = true
exporter.cpcds.export = true
exporter.symptoms.csv.export = true
exporter.fhir.export = true
```

### 📚 Documentation Reference:

- 🔗 https://github.com/synthetichealth/synthea/wiki
- 🔗 https://github.com/synthetichealth/synthea/wiki/Flexporter

## 🔍 Use Cases

- FHIR-based measure evaluation using QI-Core (e.g., ecqm-content-qicore-2024)

- Patient access / payer interoperability testing (via CPCDS)

- Legacy system testing with CCDA

- Population cohort analysis based on custom conditions

## 📜 License

This dataset is fully synthetic and generated with open-source tools. No real patient data is used.

- 🔗 Synthea License: [MIT License](https://github.com/synthetichealth/synthea/blob/master/LICENSE)
