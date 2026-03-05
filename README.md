# MinHashing and LSH Assignment

**Course:** CSL7110 - Machine Learning with Big Data  
**Student:** Jahanvi Gajera (M25CSA012)

## Overview

This repository contains implementations of MinHashing and Locality Sensitive Hashing (LSH) algorithms for document similarity detection and nearest neighbor search on the MovieLens dataset.

## Implementation Details

### Question 1: K-Grams
- Created character 2-grams, 3-grams, and word 2-grams from documents
- Computed exact Jaccard similarity between document pairs
- **Result:** D1-D2 similarity = 0.978 (near-duplicates)

### Question 2: MinHashing
- Implemented MinHash approximation with varying hash functions (t = 20 to 1500)
- **Optimal choice:** t = 150 provides high accuracy (~0.9667) with efficient computation time (~0.013s)
- Trade-off analysis between accuracy and computational cost

### Question 3: LSH
- Tested multiple (b, r) combinations for similarity threshold τ = 0.7
- **Best configuration:** r = 8, b = 20 (inflection point ≈ 0.688)
- Achieved optimal balance between precision and recall

### Question 4: MinHashing on MovieLens
- Dataset: 943 users, 1682 movies
- Computed exact Jaccard for 444,153 user pairs
- MinHash evaluation with t = [50, 100, 200]
- **Results:** Higher t values reduce false positives and negatives

### Question 5: LSH on MovieLens
- Candidate pair detection for similarity thresholds τ = 0.6 and τ = 0.8
- **Best performer:** (t=200, r=5, b=40) with 0% FP and 0% FN for both thresholds
- Comprehensive S-curve analysis for all configurations

## Key Findings

- **MinHash:** Increasing hash functions improves accuracy but increases computation time
- **LSH:** Proper (r, b) tuning is critical for balancing false positives and false negatives
- **Optimal configuration:** t=200, r=5, b=40 provides reliable results with minimal errors

## Files

- `minHashing_and_LSH.ipynb` - Main implementation notebook
- `M25CSA012_CSL7110_Assignment.pdf` - Detailed assignment report


## Usage

Open the Jupyter notebook and run cells sequentially to reproduce all results.

---

**Repository:** [ML_with_BigData/Assignment2](https://github.com/jahanvi0106/ML_with_BigData/tree/Assignment2)
