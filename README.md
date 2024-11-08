# Calcium Imaging in ALM (Anterior Lateral Motor Cortex) for motor decision making task

[![MIT License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Build Status](https://img.shields.io/badge/build-passing-brightgreen)]()
[![Python](https://img.shields.io/badge/python-3.x-brightgreen)](https://www.python.org/)

This repository contains code and data analysis pipelines for studying neuronal activity in the **Anterior Lateral Motor Cortex (ALM)** of mice during decision-making tasks. Specifically, we analyze calcium imaging data to investigate neuronal patterns as mice choose between left and right options based on auditory cues.

## Table of Contents

- [Project Overview](#project-overview)
- [Data](#data)
- [Methods](#methods)
- [Results](#results)
- [License](#license)

## Project Overview

This project investigates the phenomenon of serial dependence in motor planning through a two-choice discrimination task in mice. Serial dependence refers to how recent past actions influence current motor decisions. The project focuses on understanding how neuronal activity in the anterolateral motor cortex (ALM) adapts when a mouse is required to make motor decisions based on previous trials, revealing a unique neural signature termed the "oomph effect."

## Data

The dataset used in this project consists of calcium imaging data from the anterolateral motor cortex (ALM) of mice engaged in a two-choice decision-making task based on auditory cues. The data includes:

### 1. Raw Data:
- **Calcium Imaging Recordings**: Collected from the ALM using GCaMP6 calcium indicators.
- **Optogenetic Stimulation Data**: Trials where optogenetic stimulation of the D2 pathway was applied.
- **Behavioral Data**: Trial-by-trial behavioral choices (left vs. right) and outcomes (correct vs. incorrect); separately, licking data for left and right licks.

### 2. Processed Data:
- Preprocessed calcium imaging traces including:
  - **Motion-corrected data** using the [Caiman package](https://github.com/flatironinstitute/CaImAn).
  - **Deconvolved neural activity** for estimating spike rates.
- **Trial Types**:
  - `prev_same`: Trials where the current choice matches the previous choice (e.g., left after left).
  - `prev_diff`: Trials where the current choice differs from the previous choice (e.g., left after right).

### 3. Analysis Output:
- **ICA/PCA Components**: Extracted independent or principal components from neural data to identify key patterns.
- **Oomph Effect Analysis**: Identified neurons showing increased activity after trials of different types.
- **Optogenetic Modulation**: Data showing the effects of D2 pathway stimulation on behavioral accuracy and neuronal activity.

### Data Access
Due to the size of the dataset, raw data files are not included in this repository. Please contact me if you require access to the data.

## Methods

This section describes the methods used for calcium imaging, optogenetic stimulation, and data analysis in this project.

### Calcium Imaging
Neuronal activity was recorded using a one-photon 3i VIVO microscope at a resolution of 512x512 pixels and a frame rate of 10 Hz. The calcium imaging was performed using **GCaMP6** calcium indicators to record activity in the ALM of mice during a two-choice decision-making task.

- **Preprocessing**: We used the **CaImAn package** (Giovannucci et al., 2019) for initial signal processing. This included:
  - Motion correction to correct for drift and other movements during imaging.
  - Segmentation of neurons to extract regions of interest.
  - Deconvolution to estimate spike times from calcium traces using sparse non-negative deconvolution (Pnevmatikakis et al., 2016). This step allows for improved temporal resolution and more accurate estimation of neuronal firing rates.

### Dimensionality Reduction
To analyze population-level activity, we employed dimensionality reduction techniques:
- **Principal Component Analysis (PCA)** was used to capture the most prominent activity patterns across trials.
- **Independent Component Analysis (ICA)** was applied to extract task-relevant neuronal components, which provided a better separation of neural signals than PCA, focusing on independent sources of neuronal activity.

### Optogenetic Stimulation
Optogenetic stimulation was performed to manipulate neuronal activity during certain trials.
- **Viral Vector**: We injected an **AAV9 viral vector** expressing **hChR2-EYFP** under the **EF1 promoter** into the ALM to enable optogenetic stimulation of the D2 pathway.
- **Laser Stimulation**: 473 nm blue light laser pulses (5 ms, 20 Hz) were delivered for a total of 250 ms at an intensity of 25 mW. Masking LEDs were used to prevent behavioral responses to the laser.

### Behavioral Tasks
Mice performed a two-choice discrimination task where they made left or right licks based on auditory cues.

### Population Activity Analysis
We performed population-level analyses to investigate the effects of serial dependence on motor planning:
- For each trial, we analyzed the trajectories of neuronal activity in a reduced-dimensional space obtained via PCA/ICA.
- We compared the peak activity for the components for `prev_same` and `prev_diff` trials and used non-parametric tests (Mann-Whitney U) to assess the significance of observed differences in neuronal dynamics.

### Visualization
Neuronal activity and results were visualized using custom scripts that generate trial-averaged activity traces, showing neuronal responses aligned to key task events (e.g., tone onset, choice response). The results include heatmaps, PCA component plots, and raster plots to demonstrate the task-related activity of neurons during the behavioral tasks.


## Results
Key Findings:  
* Mice show increased errors when a trial is preceded by a different trial type (left vs. right), highlighting the role of recent trial history in decision-making.
* Neuronal recordings show distinct patterns of activity in the ALM, with a subset of neurons showing increased firing rates after different trial types.
* Optogenetic stimulation of the D2 pathway reduces errors, mimicking the oomph effect, and provides insights into the neural mechanisms underlying motor planning influenced by previous actions.
* The oomph effect diminishes when trial choices are free (without external cues), indicating the role of reward-based learning in serial dependence.

## License

This project is licensed under the **MIT License**. You are free to use, modify, and distribute the code in this repository, as long as the original copyright notice and permission notice appear in all copies of the software.




