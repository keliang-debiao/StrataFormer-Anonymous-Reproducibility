StrataFormer Anonymous Reviewer Code

This repository contains the anonymized implementation and supporting materials for StrataFormer, including the model architecture, multimodal data interface, participant-disjoint data splitting utilities, training and evaluation code, ablation configurations, statistical analysis utilities, efficiency profiling tools, automated tests, documentation, and manuscript-reference artifacts.

The repository is organized for anonymous review. It does not include raw source videos, personal metadata, or identifiable participant information.

Repository Structure

StrataFormer_Anonymous_Reproducibility/
├── .github/
│   └── workflows/
│       └── tests.yml
├── artifacts/
│   └── manuscript_reference/
├── configs/
│   ├── paper.yaml
│   ├── smoke.yaml
│   ├── local_only.yaml
│   ├── global_only.yaml
│   └── serial.yaml
├── data/
│   ├── README.md
│   ├── manifest_schema.csv
│   └── example_manifest.csv
├── docs/
│   ├── ANONYMOUS_RELEASE_CHECKLIST.md
│   ├── AI_EXPERIMENT_GUIDE.md
│   └── CONFIGURATION_NOTES.md
├── folds/
│   ├── README.md
│   └── reported_fold_composition.csv
├── logs/
│   └── reference/
├── scripts/
├── src/
│   └── strataformer/
└── tests/

Source Code

The main implementation is located in src/strataformer/.

Model Components

src/strataformer/models/ contains the neural-network implementation:

model.py defines the StrataFormer model and model-construction interface.

tcn.py contains the masked temporal convolution and residual TCN components used for visual temporal encoding.

fusion.py implements visual-query/audio-key-value cross-modal attention and classification-token handling.

masking.py contains mask propagation and mask-aware pooling utilities.

__init__.py exposes the model-building interface.

The implementation supports the full StrataFormer architecture and the local-only, global-only, and serial comparison variants.

Data Processing

src/strataformer/data.py contains:

NumPy feature loading;

common-interval handling for multimodal sequences;

fixed-length truncation and right padding;

validity-mask construction;

training-fold normalization-statistics estimation;

the LMVD dataset interface.

src/strataformer/splits.py contains:

manifest validation;

grouped fold generation;

participant-disjointness checks;

fold-composition summaries;

outer training, validation, and test fold construction;

manifest and fold-assignment integration.

Training and Evaluation

src/strataformer/engine.py contains the training and inference routines, including epoch scheduling, training, prediction, evaluation, and validation-based early stopping.

src/strataformer/metrics.py provides binary classification metrics, prediction conversion, confusion-matrix calculation, and metric aggregation utilities.

src/strataformer/statistics.py contains matched-fold statistical comparison utilities.

Architecture and Configuration Utilities

src/strataformer/architecture.py provides analytical checks for temporal sequence structure, attention-pair dimensions, and trainable parameter counts.

src/strataformer/config.py provides YAML configuration loading, inheritance, merging, and saving.

src/strataformer/utils.py contains random-seed control, worker seeding, participant hashing, JSON input/output, and command-line parsing helpers.

Configuration Files

The configs/ directory contains experiment configurations:

paper.yaml — main experiment configuration for the full StrataFormer architecture.

local_only.yaml — local-resolution comparison variant.

global_only.yaml — global-resolution comparison variant.

serial.yaml — serial local-to-global comparison variant.

smoke.yaml — reduced configuration for rapid code and pipeline checks.

These files define data dimensions, sequence lengths, model settings, training settings, fold settings, random seeds, and output locations used by the implementation.

Experiment Scripts

The scripts/ directory contains command-line utilities for the complete experimental workflow:

prepare_manifest.py — constructs a normalized feature manifest from metadata and feature directories.

audit_data.py — checks feature dimensions and fixed-length preprocessing outcomes.

make_folds.py — creates deterministic participant-disjoint folds.

train_cv.py — trains and evaluates StrataFormer across participant-disjoint outer folds.

evaluate_oof.py — aggregates seed-level predictions into out-of-fold evaluation files.

compare_variants.py — performs matched-fold statistical comparisons between architecture variants.

profile_models.py — profiles model parameters, inference latency, and CUDA memory usage.

architecture_audit.py — checks architecture dimensions and analytical parameter counts without requiring GPU execution.

export_attention.py — exports head-wise attention information for an anonymous sample.

make_toy_data.py — creates non-clinical toy feature tensors for smoke testing.

generate_reference_logs.py — generates formatted reference logs from manuscript-reference artifacts.

verify_repository.py — performs repository-level consistency checks.

Data Interface

The data/ directory documents the expected processed-data interface.

README.md describes the required multimodal feature format and preprocessing order.

manifest_schema.csv defines the expected manifest fields.

example_manifest.csv provides an example of the manifest structure.

The code expects processed audio and visual feature sequences stored as NumPy arrays together with anonymous sample identifiers, participant identifiers, and binary labels. Participant identifiers are used for grouped data splitting and are not provided to the model as predictive features.

Raw videos, names, platform identifiers, and other personally identifiable information are not included in this repository.

Fold Information

The folds/ directory contains documentation for participant-disjoint cross-validation and an aggregate fold-composition file.

folds/README.md describes the expected schema for exact fold assignments and the participant-level separation requirements used by the experimental pipeline.

Automated Tests

The tests/ directory contains unit tests for:

participant-disjoint splitting;

preprocessing and mask construction;

architecture dimensions;

model variants and tensor shapes;

statistical-analysis functions.

The GitHub Actions workflow in .github/workflows/tests.yml is included for automated repository testing.

Documentation

The docs/ directory contains supporting documentation:

ANONYMOUS_RELEASE_CHECKLIST.md — checklist for preparing the repository for anonymous review.

AI_EXPERIMENT_GUIDE.md — workflow and constraints for AI-assisted experiment execution.

CONFIGURATION_NOTES.md — explanation of configuration provenance and implementation settings.

Manuscript Reference Artifacts

The artifacts/manuscript_reference/ directory contains machine-readable files corresponding to tables, statistics, architecture checks, preprocessing summaries, and other numerical statements represented in the anonymized manuscript.

Included files cover:

main evaluation summaries;

seed-level summaries;

fold-level summaries;

paired statistical-analysis records;

out-of-fold confusion information;

efficiency-profile records;

preprocessing-distribution records;

baseline-comparison records;

dataset summary metadata;

architecture-contract information.

These files are provided as manuscript-reference materials and are separated from newly generated experimental outputs.

Reference Logs

The logs/reference/ directory contains formatted reference materials derived from the manuscript-reference artifacts, including:

manuscript summary logs;

training-log format examples;

efficiency-log references;

fold-level reference logs.

These files document expected file structures and logging formats and are kept separate from logs produced by new executions.

Scope of the Package

The repository contains the implementation, experiment configuration, validation utilities, test suite, documentation, and anonymous reference materials needed to inspect the StrataFormer experimental pipeline.

Source dataset files and identifiable participant information are not redistributed in the package.
