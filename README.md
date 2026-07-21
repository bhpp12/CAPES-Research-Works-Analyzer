# CAPES Research Works Analyzer

## Overview

This project analyzes a dataset of academic works from **CAPES/UFC** using Python. It extracts statistical information about the dataset, including:

- Programs with the largest number of research works;
- Advisors with the highest number of supervised works;
- Most frequent knowledge areas;
- Most frequent words appearing in research titles.

To improve performance, the word frequency analysis is executed concurrently using **multithreading**.

---

## Project Structure

```
.
├── main.py                   # Main program
├── arquivo.py                # Dataset loading
├── trabalho.py               # Trabalho class
├── contagem.py               # Generic counting functions
├── contagem_thread.py        # Multithreaded word counting
├── carregar_stopwords.py     # Portuguese and English stopwords
├── normalizacao.py           # Text normalization utilities
├── ap2-capes-ufc-2021.csv    # Dataset
└── README.md
```

---

## Features

The program generates the following rankings:

- Top 10 graduate programs with the most research works.
- Top 10 advisors with the most supervised works.
- Top 10 combinations of Knowledge Area and Research Area.
- Top 20 most frequent words found in research titles.

The title analysis includes:

- Text normalization
- Accent removal
- Lowercase conversion
- Punctuation removal
- Stopword filtering (Portuguese and English)
- Removal of words with three or fewer characters

---

## Dataset

The input dataset must be a CSV file separated by semicolons (`;`).

The following columns are used:

| Column | Description |
|---------|-------------|
| NM_PROGRAMA | Graduate program |
| NM_ORIENTADOR | Advisor |
| NM_GRANDE_AREA_CONHECIMENTO | Major knowledge area |
| NM_AREA_CONHECIMENTO | Specific knowledge area |
| NM_PRODUCAO | Research title |

---

## Text Processing

Before counting words, every title is normalized by:

- Converting to lowercase;
- Removing accents;
- Removing punctuation and special characters;
- Removing extra spaces.

Example:

```
"Análise de Dados com Inteligência Artificial!"
```

becomes

```
analise de dados com inteligencia artificial
```

After normalization, Portuguese and English stopwords are removed.

---

## Multithreading

The project uses Python's `threading` module to speed up title processing.

The workflow is:

1. Split the dataset into four blocks.
2. Create one thread for each block.
3. Count word frequencies independently.
4. Merge all partial dictionaries into a final frequency dictionary.

Each thread processes only its assigned subset of research works.

---

## Requirements

- Python 3.8 or newer

### Libraries

Install the required dependency:

```bash
pip install pandas
```

---

## Running the Program

Using the default dataset:

```bash
python main.py
```

Using another dataset:

```bash
python main.py your_dataset.csv
```

---

## Example Output

```
Total research works loaded: 12548

Top 10 Programs with the Most Research Works
--------------------------------------------
Computer Science: 432
Education: 398
Mathematics: 352
...

Top 10 Advisors
---------------
Advisor A: 85
Advisor B: 79
...

Top 10 Knowledge Areas
----------------------
Engineering / Computer Science: 512
Health Sciences / Medicine: 487
...

Top 20 Most Frequent Words in Titles
------------------------------------
analysis: 241
model: 214
learning: 198
...
```

---

## Main Components

### `Trabalho`

Represents a research work containing:

- Graduate program
- Advisor
- Major knowledge area
- Specific knowledge area
- Title

---

### Dataset Loader

Reads the CSV file using **pandas** and creates a list of `Trabalho` objects.

---

### Text Normalization

Responsible for:

- Removing accents
- Removing punctuation
- Lowercase conversion
- Cleaning whitespace

---

### Stopword Loader

Loads Portuguese and English stopword lists and normalizes them before use.

---

### Word Counter Thread

Each thread:

- Processes a subset of research works;
- Normalizes every title;
- Removes stopwords;
- Counts valid words;
- Stores its partial result.

---

### Ranking Generator

Creates rankings sorted by:

1. Frequency (descending)
2. Alphabetical order (ascending) for tie-breaking

---

## Technologies Used

- Python
- Pandas
- Threading
- Regular Expressions (`re`)
- Unicode Normalization (`unicodedata`)

---

## Future Improvements

Possible enhancements include:

- Export rankings to CSV or Excel.
- Generate charts automatically.
- Use multiprocessing for larger datasets.
- Allow a configurable number of threads.
- Add stemming or lemmatization.
- Build an interactive graphical interface.

---

## Author

Developed as an academic project for analyzing CAPES/UFC research production using Python, text preprocessing, and concurrent programming.
