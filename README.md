# California Wildfire Occurrence Prediction

CSCI 567 course project for row-level wildfire occurrence prediction using daily California weather and seasonal features.

The final report evaluates wildfire occurrence as a daily tabular classification problem. The main modeling notebook uses a chronological split and compares a class-prior baseline, logistic regression, Random Forest, XGBoost, tuned tree models, and a row-level MLP. A second notebook preserves the temporal-windowed experiments used during project development.

## Authors

Demy Brati, Calvin Kwong, Cheonhong (Jun) Lee, and Matthew Montoya
University of Southern California
CSCI 567: Machine Learning (Spring 2026)

## Repository Layout

```text
.
├── README.md
├── doc/
│   ├── main.pdf
│   ├── main.tex
│   ├── main.bib
│   ├── icml2021.sty
│   ├── icml2021.bst
│   └── figures/
├── input/
│   └── CA_Weather_Fire_Dataset_1984-2025.csv
└── src/
    ├── 01_row_level_one_day_modeling.ipynb
    └── 02_temporal_windowed_exploratory_analysis.ipynb
```

## Project Scope

The primary submission is the row-level one-day modeling benchmark:

```text
src/01_row_level_one_day_modeling.ipynb
```

This notebook produces the final model comparison, feature relevance analysis, calibration analysis, and seasonal error analysis used in the report.

The temporal-windowed notebook is included for completeness:

```text
src/02_temporal_windowed_exploratory_analysis.ipynb
```

That notebook contains exploratory temporal-windowed experiments, including multi-horizon experiments and LSTM/GRU sequence-model work. These experiments are part of the project record, but they are not the final benchmark. The final report uses the row-level formulation because the dataset does not include a stable location identifier. Without a location key, adjacent rows cannot be treated as consecutive observations from the same place.

## Data

The dataset file is:

```text
CA_Weather_Fire_Dataset_1984-2025.csv
```

It is stored in the repository at:

```text
input/CA_Weather_Fire_Dataset_1984-2025.csv
```

For the Colab workflow, copy the same CSV to the top level of Google Drive:

```text
MyDrive/CA_Weather_Fire_Dataset_1984-2025.csv
```

After mounting Drive, the expected path is:

```text
/content/drive/MyDrive/CA_Weather_Fire_Dataset_1984-2025.csv
```

Do not rename the CSV unless the notebook path configuration is updated.

## Runtime

The notebooks were developed and run in Google Colab.

Recommended runtime:

```text
Python 3
GPU runtime
T4 GPU preferred
```

The notebooks can fall back to CPU in some places, but the intended workflow uses Colab GPU acceleration where available. XGBoost and PyTorch use CUDA when supported by the runtime.

## Running the Notebooks

1. Upload or open the repository notebooks in Google Colab.
2. Copy `input/CA_Weather_Fire_Dataset_1984-2025.csv` to the top level of Google Drive.
3. Start a GPU runtime. A T4 GPU is preferred.
4. Run the row-level notebook first:

   ```text
   src/01_row_level_one_day_modeling.ipynb
   ```

5. Run the temporal-windowed notebook only if reproducing the exploratory analysis:

   ```text
   src/02_temporal_windowed_exploratory_analysis.ipynb
   ```

Generated outputs are written to Colab-local directories:

```text
/content/wildfire_row_level_one_day_outputs
/content/wildfire_temporal_windowed_outputs
```

## Modeling Setup

The final benchmark uses data through 2023. The 2024 and early 2025 rows are excluded from the primary analysis because the dataset audit found an all-negative tail during that period.

The final chronological split is:

```text
Train:      1984-2017
Validation: 2018-2020
Test:       2021-2023
```

Target variable:

```text
FIRE_START_DAY
```

## Report

The final report is available at:

```text
doc/main.pdf
```

LaTeX source files are included in `doc/`.

## Notes for Reproduction

- Keep the CSV filename unchanged.
- Use the same chronological split to reproduce the reported results.
- Run the row-level notebook before using generated row-level result tables or figures.
- Colab GPU assignment is not deterministic; runtimes may vary across sessions.
- Minor numerical differences can occur across hardware/runtime versions even with fixed random seeds.

## Acknowledgements & Disclosures

This project was completed for USC CSCI 567. We acknowledge the CSCI 567 course staff for providing the report template. The report uses the ICML 2021 LaTeX style file, originally created by P. Langley and later modified by ICML template contributors including Terran Lane, Kristian Kersting, Prasad Tadepalli, Andrew Moore, Ricardo Silva, Sam Roweis, Kiri Wagstaff, Hal Daumé III, Christoph Sawade, Tobias Scheffer, Francesco Figari, Sanjoy Dasgupta, Fei Sha, Percy Liang, Daniel Roy, and Iain Murray.

The implementation uses standard Python machine learning tools, including scikit-learn, XGBoost, and PyTorch.

AI-assisted tools used during the project included OpenAI's ChatGPT,  Microsoft's Github Copilot, Alibaba Cloud's Qwen, and DeepSeek. These tools supported brainstorming, code drafting and refinements, LaTeX formatting, English-language editing, spell checking, translation, and prose revision. The project team ran the experiments, reviewed the outputs, selected the final results, and is responsible for the submitted code and report.
