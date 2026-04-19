# Simulation-Based Inference for an Adaptive-Network Epidemic Model

This repository contains code to reproduce the results from the report.

## Contents
- ABC rejection implementation
- Regression-adjusted ABC
- SMC-ABC implementation
- Plot generation scripts

## Code Structure

- `main_analysis.py`  
  Contains the core implementation of the ABC methods (rejection ABC, regression adjustment, and SMC-ABC) used to generate the main results in the report.

- `additional_analysis.py`  
  Contains additional analyses including:
  - robustness checks (different seeds and distance metrics)
  - coefficient scatter plots
  - posterior predictive checks
  - synthetic truth recovery experiments

## Data
The required datasets are included in this repository.

## Usage
Run the main notebook or scripts to reproduce figures and results.

## Acknowledgements
LLM assistant's (ChatGPT + Claude) were used to support code development. All results, analysis, and interpretations are my own.

## Author
Millan Bhardwaj
