# Phage Genome Clustering Pipeline

This repository contains a modular pipeline for phage genome clustering using sequence embeddings, Pharokka-derived genomic features, and downstream clustering analysis. The workflow is organized into separate stages so that users can either reproduce the full pipeline from raw phage genomes or directly reproduce the results of this project using the precomputed files provided in the repository.

## Repository Contents

The main codes in this repository are:

1. `extract_dnabert_embeddings`  
   Generates DNABERT embeddings from phage genome FASTA files.

2. `extract_pharokka_features_colab`  
   Extracts Pharokka-based genomic features. This code is intended to be run in Google Colab, and the notebook itself contains the required execution instructions.

3. `run_clustering`  
   Main clustering pipeline. This code imports the outputs of the DNABERT embedding extraction and Pharokka feature extraction steps, combines them, and performs the clustering analysis.

4. `run_naiive_clustering`  
   Baseline clustering pipeline. This is a simplified version of the main clustering workflow and performs clustering using only `gc_content` and genome `length`, without using DNABERT embeddings or Pharokka-derived features.

## Required Inputs

To run the full pipeline on a new phage dataset, the user must provide:

- A CSV file listing the phages to be analyzed, such as `PA.csv`
- The corresponding phage genome `.fasta` files

For this project, example/project-specific versions of these files are already provided:

- `PA.csv`
- `FASTA files.zip`

The FASTA archive must be unzipped before running the embedding extraction step.

## Provided Project Files

This repository includes precomputed project files so that users can reproduce the clustering results for the phages used in this study without rerunning all preprocessing steps.

Provided files include:

- `embeddings.csv`  
  Precomputed DNABERT embeddings for the phages used in this project

- `pharokka_outputs.zip`  
  Precomputed Pharokka output files for the phages used in this project

These files allow users to bypass the feature extraction stages if they only want to reproduce the clustering analysis for the phages used in this work.

## Pipeline Overview

The workflow consists of three main stages and one baseline analysis:

### Step 1: DNABERT Embedding Extraction

Run `extract_dnabert_embeddings` after preparing the metadata CSV and unzipping the FASTA files.

This code:
- reads the provided phage FASTA files,
- extracts DNABERT embeddings for each phage genome, and
- outputs the embedding results for downstream clustering.

If the goal is only to reproduce the results for the phages used in this project, this step can be skipped by using the provided `embeddings.csv` file.

### Step 2: Pharokka Feature Extraction

Run `extract_pharokka_features_colab` in Google Colab.

This code:
- processes the phage genomes using Pharokka,
- extracts the required genomic annotation outputs, and
- produces the Pharokka-derived outputs used later in clustering.

The instructions for running this step are provided inside the notebook itself.

If the goal is only to reproduce the results for the phages used in this project, this step can be skipped by using the provided `pharokka_outputs.zip` file.

### Step 3: Main Clustering Analysis

Run `run_clustering`.

This is the main clustering code in the repository. It:
- imports the DNABERT embedding results,
- imports the Pharokka-derived outputs,
- combines these extracted features into a unified dataset, and
- performs the clustering analysis.

This code is intended for the full feature-based clustering workflow.

### Step 4: Naive Baseline Clustering

Run `run_naiive_clustering`.

This code is a simplified baseline clustering workflow. Unlike `run_clustering`, it does not use DNABERT embeddings or Pharokka-derived features. Instead, it performs clustering using only:

- `gc_content`
- genome `length`

This code is useful as a baseline or comparison model for evaluating the value of the richer feature-based clustering approach.

## How to Use This Repository

There are two main ways to use this repository.

### Option 1: Reproduce the Full Pipeline on a New Dataset

Use this option if you want to run the complete workflow on your own phage genomes.

1. Prepare a metadata CSV file listing the phages to be analyzed.
2. Prepare the corresponding `.fasta` genome files.
3. Run `extract_dnabert_embeddings` to generate DNABERT embeddings.
4. Run `extract_pharokka_features_colab` in Google Colab to generate the Pharokka outputs.
5. Run `run_clustering` to perform the final clustering analysis.

### Option 2: Reproduce the Results of This Project

Use this option if you only want to reproduce the clustering results for the phages used in this repository.

1. Use the provided `embeddings.csv` instead of rerunning `extract_dnabert_embeddings`.
2. Use the provided `pharokka_outputs.zip` instead of rerunning `extract_pharokka_features_colab`.
3. Run `run_clustering` using the provided project files.

If you want to reproduce the simplified baseline analysis instead, run `run_naiive_clustering`.

## Input and Output Summary

### `extract_dnabert_embeddings`
**Input:**
- phage metadata CSV (e.g., `PA.csv`)
- phage FASTA files

**Output:**
- embedding results used in downstream clustering
- project version provided as `embeddings.csv`

### `extract_pharokka_features_colab`
**Input:**
- phage FASTA files

**Output:**
- Pharokka-derived outputs used in downstream clustering
- project version provided as `pharokka_outputs.zip`

### `run_clustering`
**Input:**
- DNABERT embedding outputs
- Pharokka outputs

**Output:**
- clustering results based on the combined extracted features

### `run_naiive_clustering`
**Input:**
- basic phage descriptors including `gc_content` and genome length

**Output:**
- clustering results based only on `gc_content` and genome length



## Acknowledgments

Initial components of this workflow were developed by Yassaman Ommi. The current repository reflects substantial modifications, restructuring, and final integration for reproducible analysis.
