# ML_with_BigData

# CSL7110 – Assignment 1  
## ML with Big Data  

**Name:** Jahanvi Gajera  
**Roll No:** M25CSA012  
**Course:** ML with Big Data  
**Tools Used:** Hadoop (MapReduce), Apache Spark (PySpark)  

---

# 📌 Assignment Summary

This assignment covers practical implementation of:

- Hadoop MapReduce (WordCount)
- HDFS Commands & Configuration
- Spark Data Processing
- Metadata Extraction using Regex
- TF-IDF Computation
- Cosine Similarity
- Author Influence Network Construction

Dataset Used: **Project Gutenberg (D184MB dataset)**

---

# 🟢 Part A: Hadoop Tasks

## WordCount Implementation
- Executed WordCount example.
- Implemented `map()` and `reduce()` functions.
- Used `LongWritable`, `Text`, and `IntWritable`.
- Removed punctuation and tokenized text.
- Measured execution time.
- Experimented with split size parameter.

## Key Observations
- Increasing split size slightly reduced execution time.
- For small datasets, performance difference is minimal.
- Optimal split size depends on:
  - HDFS block size
  - Cluster size
  - Data volume

---

# 🔵 Part B: Spark Tasks

## 1️⃣ Metadata Extraction
Extracted:
- Title
- Release Date
- Language
- Encoding

Performed Analysis:
- Books released per year
- Most common language
- Average title length

Used Regular Expressions for extraction.

---

## 2️⃣ TF-IDF and Book Similarity

### TF-IDF
- TF measures word frequency in a document.
- IDF measures word rarity across documents.
- TF-IDF highlights important but unique words.

### Cosine Similarity
- Measures similarity between TF-IDF vectors.
- Formula:

  Cosine Similarity = (A · B) / (||A|| ||B||)

- Suitable because it:
  - Normalizes document length
  - Works with sparse vectors
  - Captures similarity in word importance

Generated CSV file for similarity results.

---

## 3️⃣ Author Influence Network

### Construction
- Extracted author and release year.
- Defined influence if books were released within X years.
- Represented network using Spark DataFrame:
