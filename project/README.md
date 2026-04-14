# NX-414 Project

## Brain-Model Alignment Across Neural Recording Modalities


In this project, you will compare neural responses from multiple recording modalities to features extracted from two vision models. You will work with:

- **TVSD** macaque electrophysiology
- **THINGS-EEG2** human EEG
- **NSD** human fMRI

and compare them against features from:

- **Adv-ResNet152**
- **Qwen3-VL-2B-Instruct**

The project combines:

- dataset inspection and visualization,
- noise ceiling estimation,
- representational alignment analyses such as **RSA** and **unbiased linear CKA**,
- predictive alignment with **linear encoding models**,
- an open-ended extension beyond the baseline pipeline.

## Main Notebook Structure

The notebook is organized into four main sections:

1. **Introduction and setup**
   Load the datasets and feature files, inspect their structure, and verify stimulus matching.
2. **Inspection, visualization, and noise ceiling estimates**
   Explore EEG responses, compare two EEG noise ceiling estimators, and visualize NSD reliability.
3. **Brain-model alignment**
   Run representational analyses and predictive encoding analyses across models, layers, and neural targets.
4. **Open-ended research extension**
   Design an extension beyond the baseline linear readout pipeline and compare it against the baseline.

## What You Must Submit

Submit the following on **Moodle** by **May 6, 2026 at 23:59**:

1. **One Jupyter notebook** containing your full analysis.
2. **Any supporting Python scripts** needed to run the notebook.
3. **Figures that are part of your notebook answers** should be embedded and rendered in notebook Markdown.
4. **One PDF report** of **up to 2 pages**, **excluding references**, with **no appendix**.
5. **One zip archive** named exactly as:

```text
nx414_{SCIPER1}_{SCIPER2}_{SCIPER3}.zip
```

If your group has fewer than three members, remove the extra `_SCIPER` fields accordingly.

## Submission Rules

- Fill in the **group information** at the top of the notebook and in the report.
- **Clear all notebook outputs before submission.**
- Submit only the code needed to reproduce your analyses.
- **Do not submit model weights.**
- **Do not submit CSV files or other large derived result dumps.**
- Keep the archive lightweight and reproducible.
- For the final notebook, any figure you want to include as part of the notebook narrative or scientific argument should be embedded and rendered in **Markdown**, together with a short written interpretation, rather than left as an unexplained raw cell output.



## Use of LLMs

You may use LLM-based tools to help you write code, debug, or improve explanations. However, you remain fully responsible for the **correctness**, **quality**, and **clarity** of everything you submit, including both the notebook and the report.

In particular:

- check that any generated code actually runs and does what you claim it does,
- verify that any scientific statement or interpretation is correct,
- make sure the final writing sounds like a clear academic report written for this course,
- avoid vague, overly polished, or context-free text,
- avoid fancy wording or unnecessarily complex sentences that do not add clarity.

If you use an LLM, revise the output so that your submission reads naturally, is specific to your actual results, and does not look like generic generated text.

Failure to do so may result in **point deduction**.

## Recommended Pacing

This project is designed to span roughly **three weeks**.

- **Week 1:** complete setup, understand the datasets, verify stimulus matching, and complete Section 1.
- **Week 2:** Complete the required analyses in Section 2 and start Section 3.
- **Week 3:** complete the open-ended extension, polish the notebook, and write the report.

## Data and Features

For the project, the main shared resources are available on the platform at:

- neural datasets: `/shared/NX-414/data`
- extracted model features: `/shared/NX-414/extracted_features`

These directories are **read-only shared project resources**. You will need them to complete the notebook, but you are **not** expected to modify their contents.

Please **do not copy** these directories into your own workspace or home folder. The datasets and extracted features are **very large on disk**, and the project is designed so that you can read them directly from the shared location.

Main neural files used in the project:

- `tvsd.h5`
- `things_eeg2.h5`
- `things_eeg2-test_reps.h5`
- `nsd_func1pt8mm_individualROIs.h5`
- `nsd-subj01-ncsnr-lh.mgh`
- `nsd-subj01-ncsnr-rh.mgh`

Feature files are provided for both models and already contain extracted activations from multiple candidate layers. Feature extraction is **already done for you**. Your job is to:

- inspect available layers,
- match features to neural responses using stimulus IDs,
- compare layers using the required alignment metrics.

Important matching rule:

- **TVSD** and **EEG2** use byte-string stimulus identifiers and should be matched exactly.
- **NSD** uses integer stimulus IDs, and you must select subject-specific rows from the full NSD feature files.

## Required Analyses at a Glance

Your notebook should cover all of the following:

- dataset and feature inspection,
- stimulus matching verification,
- EEG visualization,
- **two noise ceiling estimators**:
  - variance-based,
  - split-half reliability,
- statistical comparison of these estimators against the stored EEG ceilings,
- NSD reliability conversion and cortical visualization,
- **RSA**,
- **unbiased linear CKA**,
- linear encoding models with proper train/validation/test discipline,
- predictive metrics:
  - `pearsonr`
  - `pearsonr_nc`
  - `explained_variance`
  - `explained_variance_nc`
- hybrid representational metrics on predicted responses:
  - `encoding-RSA`
  - `encoding-CKA`
- comparison across layers, models, ROIs, and modalities,
- one focused open-ended extension beyond the baseline pipeline,
- a short final discussion synthesizing your main findings.

## Report Expectations

Your **2-page PDF report** should tell a clear scientific story. It does not need to reproduce every notebook result. It can include:

- a short dataset overview,
- at least one exploratory figure from Section 1,
- the EEG noise ceiling comparison,
- the NSD reliability visualization,
- the main brain-model alignment results,
- a short conclusion and limitations.

Preferably, you should primarily focus on the open-ended extension you designed, describing:
- the motivation for your extension,
- the methods you implemented,
- the results you obtained,
- and the scientific insights you gained from it.

## Gnoto Setup

On [gnoto.epfl.ch](gnoto.epfl.ch), create a fresh environment and Jupyter kernel as follows:

```bash
my_venvs_create nx414
my_venvs_activate nx414
pip install scikit-learn nibabel nilearn seaborn h5py
my_kernels_create nx414 "NX-414"
```

After this, a kernel called **`NX-414`** should appear on the Jupyter launcher page.

When you open an existing notebook for this project, make sure to switch the notebook to the **`NX-414`** kernel.

If you prefer, you can also inspect the package list in [requirements.txt](./requirements.txt).

> **Important:** After the project deadline, your Gnoto workspaces will be deleted. Make sure to **back up any files or data you wish to keep** before then.

## Helpful Gnoto Links

- Troubleshooting:
  https://www.epfl.ch/education/educational-initiatives/cede/teaching-interactively/jupyter-notebooks-for-education/getting-started-using-jupyter-notebooks-in-your-classroom/troubleshooting/
- Performance tips:
  https://www.epfl.ch/education/educational-initiatives/cede/teaching-interactively/jupyter-notebooks-for-education/getting-started-using-jupyter-notebooks-in-your-classroom/getting-the-best-performance-on-noto/

If the recommendations above do not solve the issue, try shutting down your kernels here:

- https://gnoto.epfl.ch/hub/home

If that still does not resolve the problem, contact the teaching team on **Edstem**.

## Final Checklist

Before submitting, make sure that:

- the group information is filled in,
- the notebook runs from top to bottom,
- outputs are cleared,
- figures have readable labels and titles,
- written answers are included in the answer boxes,
- the archive name follows the required format,
- the notebook and report are both included in the final zip file.
