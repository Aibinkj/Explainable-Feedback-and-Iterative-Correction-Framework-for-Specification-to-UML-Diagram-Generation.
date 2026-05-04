# Explainable Feedback and Iterative Correction Framework for UML Diagrams

A web-based tool that leverages **Google Gemini AI** to automatically generate PlantUML use-case and class diagrams from software specifications, compare them against user-written diagrams, and deliver structured, explainable feedback with iterative correction support.

---

## Overview

Students and developers often struggle to validate whether their UML diagrams correctly represent a given software specification. This framework addresses that by:

1. **Generating** a reference UML diagram from a plain-text software specification using Gemini AI
2. **Comparing** it with a user-submitted PlantUML diagram
3. **Scoring** structural similarity on a 1–10 scale
4. **Explaining** missing actors, use cases, classes, relationships, and attributes
5. **Iteratively correcting** diagrams through a chat interface and modification panel

---

## Features

| Feature                      | Description                                                       |
|------------------------------|-------------------------------------------------------------------|
| AI Generation                | Gemini 2.5 Flash generates reference diagrams from specifications |
| Dual Diagram Support         | Supports both **Use-Case** and **Class** diagrams                 |
| Side-by-Side Comparison      | Visual comparison of system-generated vs user-written diagrams    |
| Similarity Scoring           | Numeric score (0–10) reflecting structural closeness              |
| Doubt Chat                   | Ask questions about the diagram or feedback in real time          |
| Iterative Correction         | Suggest modifications and regenerate the system diagram           |
| Update & Compare             | Submit a revised UML code and re-compare instantly                |

---

## Repository Structure
├── Minor_Pro_Final.ipynb          # Main Jupyter notebook (Flask app + AI logic)
├── dataset/                       # Prompt examples used for few-shot learning
│   ├── usecase_examples.json      # Use-case diagram input-output pairs
│   └── class_examples.json        # Class diagram input-output pairs
└── README.md

---

## Tech Stack

- **AI Model** — Google Gemini 2.5 Flash (`google-generativeai`)
- **Diagram Rendering** — [Kroki.io](https://kroki.io) PlantUML API
- **Backend** — Python, Flask
- **Frontend** — Tailwind CSS, vanilla JavaScript
- **Tunneling** — pyngrok (for Colab public URL exposure)

---

## Getting Started

### Prerequisites

- Google Colab (recommended) or a local Python 3.10+ environment
- A valid **Google Gemini API key**
- A valid **ngrok auth token**

### Running on Google Colab

1. Open `Minor_Pro_Final.ipynb` in Google Colab
2. Replace the API key and ngrok token in the notebook:
```python
   genai.configure(api_key='YOUR_GEMINI_API_KEY')
   conf.get_default().auth_token = "YOUR_NGROK_TOKEN"
```
3. Run the **"WebApp Run"** cell
4. Open the printed ngrok URL in your browser

### Local Setup

```bash
pip install flask pyngrok google-generativeai pillow requests
jupyter notebook Minor_Pro_Final.ipynb
```

---

## How It Works

User Input
├── Software Specification (plain text)
└── User PlantUML Code
│
▼
Gemini AI generates reference diagram
│
▼
Kroki.io renders both diagrams as PNG
│
▼
Gemini AI compares the two diagrams
(missing actors / use cases / classes / relationships)
│
▼
Similarity score (0–10) + structured feedback
│
▼
User can: Ask questions | Suggest modifications | Update UML

---

## Prompt Engineering

The system uses **few-shot prompting** with 30+ labeled examples for:

- **Use-case diagram generation** — ensures correct actor/use-case boundaries, `<<include>>` and `<<extend>>` relationships
- **Class diagram generation** — ensures access modifiers, multiplicities, inheritance, and composition
- **Comparison** — structured output format for missing elements and feedback
- **Similarity scoring** — calibrated 0–10 scale based on structural differences

---

## Dataset

The `dataset/` folder contains curated input-output pairs used in the few-shot prompts:

- **Use-case examples** — 30 system specifications with corresponding PlantUML use-case diagrams
- **Class diagram examples** — Feature descriptions with corresponding PlantUML class diagrams

These were manually curated and validated to ensure syntactic and semantic correctness.

---

## License

This project is intended for academic use. Please cite appropriately if you build upon this work.
