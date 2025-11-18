# Do LLM's Affect Readability of Scientific Writing?

This study investigates whether LLM's AI-Tools correlate with measurable changes in readability across peer-reviewed scientific literature from 2015 to 2025.

## Project Overview

Using the OpenAlex API, we compiled 33,000 abstracts published between 2015 and 2025 across three domains: Artificial Intelligence, Medicine, and Business. Readability was assessed using three established formulas: Flesch-Kincaid Grade Level (FKGL), Automated Readability Index (ARI), and Dale-Chall.

![AI Readability Trends](readability_trends_AI_2015_2025.png)
![Medicine Readability Trends](readability_trends_MEDICINE_2015_2025.png)
![Business Readability Trends](readability_trends_BUSINESS_2015_2025.png)

Key findings indicate that the AI domain shows a consistent rise in complexity that sharply accelerates after 2022, whereas the Medicine and Business domains show high year-to-year volatility before converging in an upward spike in 2023-2025. Statistical significance appears primarily from 2024 onwards when comparing to 2018 baseline.

## Repository Structure

The repository is organized as follows:

- **data/**: Contains raw readability scores in CSV format for all three domains
- **figures/**: Visualization outputs showing readability trends with SEM error bars
- **AI/**, **MEDICINE/**, **BUSINESS/**: Domain-specific abstracts organized by year
- **readability_analysis.ipynb**: Jupyter notebook for complete analysis pipeline (Google Colab ready)
- **methodology_flowchart.md**: Visual representation of the data processing workflow
- **requirements.txt**: Required Python packages

## Installation

Clone the repository:

```bash
git clone https://github.com/lydiakrifka/llm-readability-scientific-abstract.git
cd llm-readability-scientific-abstract
```

Install the required packages:

```bash
pip install -r requirements.txt
```

## Usage

**Using Jupyter Notebook (Recommended):**

Open `readability_analysis.ipynb` in Jupyter or Google Colab and follow the step-by-step analysis.

**Using Python Scripts:**

1. Fetch abstracts from OpenAlex:

```bash
python openalex_fetcher.py
```

2. Calculate readability scores:

```bash
python readability_analyzer.py
```

3. Compare specific years:

```bash
python statistical_comparison.py
```

## Methodology

```mermaid
flowchart LR
    subgraph Step1["<b>1. DATA COLLECTION</b>"]
        A1["<b>OpenAlex API</b><br/>Query Papers"]
        A2["<b>Filter by Domain</b><br/>AI / Medicine / Business"]
        A3["<b>Filter by Year</b><br/>2015-2025"]
        A4["<b>Collect Abstracts</b><br/>1000 per year"]
    end

    subgraph Step2["<b>2. TEXT PROCESSING</b>"]
        B1["<b>Parse Format</b><br/>Inverted Index"]
        B2["<b>Reconstruct</b><br/>Plain Text"]
        B3["<b>Save Files</b><br/>Individual .txt"]
        B4["<b>Organize</b><br/>abstracts_YEAR/"]
    end

    subgraph Step3["<b>3. READABILITY</b>"]
        C1["<b>FKGL</b><br/>Grade Level"]
        C2["<b>ARI</b><br/>Complexity Index"]
        C3["<b>Dale-Chall</b><br/>Vocabulary Score"]
    end

    subgraph Step4["<b>4. STATISTICAL ANALYSIS</b>"]
        D1["<b>Calculate</b><br/>Mean + SEM"]
        D2["<b>Aggregate</b><br/>By Year"]
        D3["<b>T-Test</b><br/>Significance"]
    end

    subgraph Step5["<b>5. RESULTS</b>"]
        E1["<b>CSV Files</b><br/>Raw Scores"]
        E2["<b>Visualizations</b><br/>Trend Plots"]
        E3["<b>Statistics</b><br/>p-values"]
    end

    Step1 ==> Step2
    Step2 ==> Step3
    Step3 ==> Step4
    Step4 ==> Step5

    A1 --> A2
    A2 --> A3
    A3 --> A4

    B1 --> B2
    B2 --> B3
    B3 --> B4

    C1 --> D1
    C2 --> D1
    C3 --> D1

    D1 --> D2
    D2 --> D3

    D3 --> E1
    D3 --> E2
    D3 --> E3

    style Step1 fill:#2196F3,stroke:#0D47A1,stroke-width:3px,color:#fff
    style Step2 fill:#9C27B0,stroke:#4A148C,stroke-width:3px,color:#fff
    style Step3 fill:#FF9800,stroke:#E65100,stroke-width:3px,color:#fff
    style Step4 fill:#4CAF50,stroke:#1B5E20,stroke-width:3px,color:#fff
    style Step5 fill:#E91E63,stroke:#880E4F,stroke-width:3px,color:#fff

    style A1 fill:#64B5F6,stroke:#0D47A1,stroke-width:2px,color:#000
    style A2 fill:#64B5F6,stroke:#0D47A1,stroke-width:2px,color:#000
    style A3 fill:#64B5F6,stroke:#0D47A1,stroke-width:2px,color:#000
    style A4 fill:#64B5F6,stroke:#0D47A1,stroke-width:2px,color:#000

    style B1 fill:#BA68C8,stroke:#4A148C,stroke-width:2px,color:#000
    style B2 fill:#BA68C8,stroke:#4A148C,stroke-width:2px,color:#000
    style B3 fill:#BA68C8,stroke:#4A148C,stroke-width:2px,color:#000
    style B4 fill:#BA68C8,stroke:#4A148C,stroke-width:2px,color:#000

    style C1 fill:#FFB74D,stroke:#E65100,stroke-width:2px,color:#000
    style C2 fill:#FFB74D,stroke:#E65100,stroke-width:2px,color:#000
    style C3 fill:#FFB74D,stroke:#E65100,stroke-width:2px,color:#000

    style D1 fill:#81C784,stroke:#1B5E20,stroke-width:2px,color:#000
    style D2 fill:#81C784,stroke:#1B5E20,stroke-width:2px,color:#000
    style D3 fill:#81C784,stroke:#1B5E20,stroke-width:2px,color:#000

    style E1 fill:#F06292,stroke:#880E4F,stroke-width:2px,color:#000
    style E2 fill:#F06292,stroke:#880E4F,stroke-width:2px,color:#000
    style E3 fill:#F06292,stroke:#880E4F,stroke-width:2px,color:#000
```

**Data Collection:** OpenAlex API, 1,000 abstracts per year per domain (2015-2025), total corpus of 33,000 abstracts.

**Readability Metrics:**

- Flesch-Kincaid Grade Level (FKGL): Measures years of education needed
- Automated Readability Index (ARI): Character-based complexity measure
- Dale-Chall Formula: Vocabulary familiarity assessment

**Statistical Analysis:** Welch's independent two-sample t-test, significance level α = 0.05, error bars show Standard Error of Mean (SEM).

## Results

Statistical significance comparing 2018 to subsequent years:

| Comparison   | ARI p-value | FKGL p-value | Dale-Chall p-value | Significant? |
| ------------ | ----------- | ------------ | ------------------ | ------------ |
| 2018 vs 2019 | 0.6634      | 0.4753       | 0.9930             | No           |
| 2018 vs 2022 | 0.6591      | 0.6787       | 0.6481             | No           |
| 2018 vs 2023 | 0.9641      | 0.4895       | 0.3064             | No           |
| 2018 vs 2024 | 0.0419      | 0.0390       | 0.000009           | Yes          |

Statistical significance only appears when comparing 2024 to 2018, confirming measurable impact on readability starting from 2024.

## License

This project is licensed under the GNU General Public License v3.0 - see the [LICENSE](LICENSE) file for details.

## Contributors

- Daniel Duhnev - UPF Barcelona
- Marcelo Jimenez - UPF Barcelona
- Lydia Krifka-Dobes - UPF Barcelona

Contact: daniel.duhnev01@estudiant.upf.edu, marceloenrique.jimenez01@estudiant.upf.edu, lydia.krifka01@estudiant.upf.edu

## Acknowledgments

OpenAlex API for open access to scholarly metadata, textstat library for readability implementations, Prof. Davinia Hernández-Leo (UPF) for supervision.
