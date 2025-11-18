# Does AI-Assisted Scientific Writing Affect Readability?

Analysis of readability trends in scientific abstracts (2015-2025) across AI, Medicine, and Business domains using OpenAlex data.

## Overview

This study examines whether AI-assisted writing tools correlate with measurable changes in readability across peer-reviewed scientific literature. Using the OpenAlex API, we compiled 33,000 abstracts published between 2015 and 2025 across three domains: Artificial Intelligence, Medicine, and Business.

Readability was assessed using three established formulas: Flesch-Kincaid Grade Level (FKGL), Automated Readability Index (ARI), and Dale-Chall. Results reveal distinct patterns. The AI domain shows a consistent rise in complexity that sharply accelerates after 2022, whereas the Medicine and Business domains show high year-to-year volatility before converging in a less pronounced upward spike in 2023-2025.

Statistical significance appears primarily from 2024 onwards when comparing to 2018 baseline. These findings suggest that increased integration of AI tools in academic writing may be associated with more complex sentence structures and denser vocabulary.

## Repository Structure

```
├── AI/
│   ├── abstracts_2015/
│   ├── abstracts_2016/
│   └── ...
├── MEDICINE/
│   ├── abstracts_2015/
│   └── ...
├── BUSINESS/
│   ├── abstracts_2015/
│   └── ...
├── data/
│   ├── readability_scores_AI_2015_2025.csv
│   ├── readability_scores_MEDICINE_2015_2025.csv
│   └── readability_scores_BUSINESS_2015_2025.csv
├── figures/
│   ├── readability_trends_AI_2015_2025.png
│   ├── readability_trends_MEDICINE_2015_2025.png
│   └── readability_trends_BUSINESS_2015_2025.png
├── openalex_fetcher.py
├── readability_analyzer.py
├── statistical_comparison.py
├── requirements.txt
└── README.md
```

## Installation

Clone the repository and install dependencies:

```bash
git clone https://github.com/yourusername/ai-scientific-writing-readability.git
cd ai-scientific-writing-readability
pip install -r requirements.txt
```

Required packages: requests, pandas, textstat, scipy, matplotlib, numpy

## Usage

Fetch abstracts from OpenAlex:

```bash
python openalex_fetcher.py
```

This queries the OpenAlex API for abstracts from 2015-2025, saves 1,000 abstracts per year per domain, and converts inverted index format to plain text files.

Configure the domain by editing the CONCEPT variable:

```python
CONCEPT = "BUSINESS"  # or "AI" or "MEDICINE"
```

And the corresponding OpenAlex concept ID:

```python
f'concepts.id:C154945302,'  # AI
f'concepts.id:C71924100,'   # Medicine
f'concepts.id:C144133560,'  # Business
```

Calculate yearly readability trends:

```bash
python readability_analyzer.py
```

Outputs: CSV file with raw scores, PNG visualization with error bars

Compare two years statistically:

```bash
python statistical_comparison.py
```

Configure years to compare:

```python
initial_year = 2022
final_year = 2023
```

Outputs: Independent t-test results, mean comparisons, p-values

## Methodology

Data Collection: OpenAlex API, 1,000 abstracts per year per domain (2015-2025), total corpus of 33,000 abstracts, topic-based filtering for domain categorization.

Readability Metrics:

Flesch-Kincaid Grade Level (FKGL) - Measures years of education needed based on sentence length and syllables per word. Formula: 0.39 _ (words/sentences) + 11.8 _ (syllables/words) - 15.59

Automated Readability Index (ARI) - Character-based complexity measure of visual density. Formula: 4.71 _ (characters/words) + 0.5 _ (words/sentences) - 21.43

Dale-Chall Formula - Vocabulary familiarity assessment based on a 3,000-word list of easy English words. Formula: 0.1579 _ (difficult_words% _ 100) + 0.0496 \* (words/sentences)

Statistical Analysis: Welch's independent two-sample t-test (equal_var=False), significance level α = 0.05, error bars show Standard Error of Mean (SEM)

## Results

Statistical significance comparing 2018 to subsequent years:

| Comparison   | ARI p-value | FKGL p-value | Dale-Chall p-value | Significant? |
| ------------ | ----------- | ------------ | ------------------ | ------------ |
| 2018 vs 2019 | 0.6634      | 0.4753       | 0.9930             | No           |
| 2018 vs 2022 | 0.6591      | 0.6787       | 0.6481             | No           |
| 2018 vs 2023 | 0.9641      | 0.4895       | 0.3064             | No           |
| 2018 vs 2024 | 0.0419      | 0.0390       | 0.000009           | Yes          |

Statistical significance only appears when comparing 2024 to 2018, confirming measurable impact on readability starting from 2024.

## Data Format

Input from OpenAlex API:

```json
{
  "abstract_inverted_index": {
    "This": [0],
    "study": [1],
    "examines": [2]
  }
}
```

Output CSV format:

```csv
paper_id,corpus,ari,flesch_kincaid_grade,dale_chall_score
abstract_2015_0,2015,18.32,16.45,12.87
abstract_2015_1,2015,19.71,17.89,13.21
```

## Replication

Set up environment:

```bash
python -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

Edit scripts to set CONCEPT variable and corresponding OpenAlex concept ID. Fetch data (takes 10-15 min per domain), then run analysis scripts.

Customization options: Change sample size via per-page parameter and break condition, modify year range in loop, add additional textstat functions, use different OpenAlex concept IDs.

## Contributors

Daniel Duhnev - UPF Barcelona
Marcelo Jimenez - UPF Barcelona
Lydia Krifka-Dobes - UPF Barcelona

Contact: daniel.duhnev01@estudiant.upf.edu, marceloenrique.jimenez01@estudiant.upf.edu, lydia.krifka01@estudiant.upf.edu

## Acknowledgments

OpenAlex API for open access to scholarly metadata, textstat library for readability implementations, Prof. Davina Durgana (UPF) for supervision
