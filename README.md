# VectorSage Cosine Similarity Analysis

This repository contains a comprehensive analysis of cosine similarity scores across different vector embedding systems and document categories.

## Overview

The project evaluates and compares cosine similarity metrics from multiple embedding systems (VectorSage, BioGPT, PubMedBERT) across various document relevance categories.

## Contents

- **vectorsage_cosine_comparison.ipynb** - Main Jupyter notebook with analysis and visualizations
- **query_results.json** - Raw query results data
- **query_results_docs_scored.json** - Query results with cosine similarity scores
- **Figures/** - Output visualizations (TIFF and SVG formats)

## Key Findings

The analysis includes:
- Overall mean cosine similarity per embedding system
- Mean cosine similarity per document relevance category
- Per-document relevance label distribution
- Combined comparative visualizations

## Relevance Categories

- **Relevant** - Highly relevant documents (score ≥ 0.70)
- **Partially relevant** - Moderately relevant documents (score ≥ 0.50)
- **Weakly relevant** - Low relevance documents (score ≥ 0.25)
- **Irrelevant** - Non-relevant documents (score < 0.25)

## Requirements

- Python 3.x
- pandas
- numpy
- matplotlib
- seaborn
- scikit-learn

## Usage

Run the Jupyter notebook to generate all analyses and visualizations:

```bash
jupyter notebook vectorsage_cosine_comparison.ipynb
```


