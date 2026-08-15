# 🎨 Text-to-Logo AI

> An AI-powered system that transforms a natural-language logo description into multiple logo concepts using NLP, Relation Extraction, Prompt Engineering, Stable Diffusion and LoRA fine-tuning.

---

## 📌 Overview

**Text-to-Logo AI** is an intelligent logo generation system designed to transform a textual description into visual logo concepts.

The system combines Natural Language Processing (NLP), semantic relation extraction, automatic prompt construction and generative AI.

Given a description such as:

> "Un logo moderne pour une marque de café avec une tasse noire, un style minimaliste et une typographie élégante."

the system automatically:

1. Analyzes the description.
2. Extracts relevant entities.
3. Identifies semantic relationships between entities.
4. Builds a structured JSON representation.
5. Generates an optimized prompt.
6. Uses Stable Diffusion with LoRA fine-tuning.
7. Generates multiple logo variations.
8. Returns four generated logos and a 2×2 result grid.

---

# 🚀 Main Features

- 📝 Natural-language logo description
- 🔎 Named Entity Recognition (NER)
- 🧠 CamemBERT-based NLP models
- 🔗 Semantic relation extraction
- 🧩 Automatic JSON block construction
- ✍️ Automatic prompt generation
- 🎯 Hybrid entity + relation processing
- 🎨 Stable Diffusion image generation
- 🔧 LoRA fine-tuning
- 🎲 Multi-seed generation
- 🖼️ Generation of four logo variations
- 🔲 Automatic 2×2 logo grid
- 🚀 REST API with FastAPI
- 🌐 Public API exposure using Ngrok
- ☁️ Google Colab GPU environment

---

# 🏗️ System Architecture

The complete system follows the pipeline:

```text
User
  │
  ▼
Textual Logo Description
  │
  ▼
FastAPI REST API
  │
  ▼
CamemBERT NER
  │
  ▼
Entity Extraction
  │
  ├── Objects
  ├── Colors
  ├── Styles
  ├── Typography
  ├── Text
  └── Brand
  │
  ▼
Relation Extraction
  │
  ├── Color relations
  ├── Style relations
  ├── Typography relations
  └── Layout relations
  │
  ▼
Hybrid Block Construction
  │
  ▼
Automatic Prompt Builder
  │
  ├── Rich Prompt
  └── Negative Prompt
  │
  ▼
Stable Diffusion v1.5
       +
     LoRA
  │
  ▼
Multi-Seed Generation
  │
  ├── Logo 1
  ├── Logo 2
  ├── Logo 3
  └── Logo 4
  │
  ▼
2×2 Result Grid
  │
  ▼
Final Output
```

---

# 🧠 AI Pipeline

## 1. Named Entity Recognition

The first stage analyzes the textual description using a fine-tuned **CamemBERT NER model**.

The model identifies relevant logo-related entities such as:

- Objects
- Colors
- Styles
- Typography
- Textual content
- Brand names
- Categories
- Layout information

Example:

```text
Input:
"Un logo moderne avec une tasse noire et une typographie élégante."

Detected entities:

Objets:
- tasse

Couleurs:
- noire

Styles:
- moderne

Typographies:
- élégante
```

The detected entities are represented using their text, label, start position and end position.

---

# 🔗 2. Relation Extraction

After entity detection, the system identifies relationships between entities.

A second **CamemBERT-based classification model** is used to predict semantic relationships.

Supported relationships include:

```text
A_COMME_COULEUR
A_COMME_STYLE
A_COMME_TYPOGRAPHIE
A_COMME_DISPOSITION
```

Example:

```text
Entity 1: tasse
Entity 2: noire

Relation:
A_COMME_COULEUR
```

Another example:

```text
Entity 1: texte
Entity 2: typographie élégante

Relation:
A_COMME_TYPOGRAPHIE
```

This allows the system to understand not only **what elements are present**, but also **how they are related**.

---

# 🧩 3. Hybrid Information Fusion

The system combines:

- NER predictions
- Relation extraction predictions

to create a structured representation of the logo description.

The resulting structure is organized into a JSON block.

Example:

```json
{
  "Marque": [],
  "Contenu_textuel": ["CAFÉ"],
  "Objets": ["tasse"],
  "Couleurs": [
    {
      "cible": "tasse",
      "couleur": "noire"
    }
  ],
  "Styles": [
    {
      "cible": "logo",
      "style": "moderne"
    }
  ],
  "Typographies": [
    {
      "cible": "CAFÉ",
      "typo": "élégante"
    }
  ],
  "Dispositions": [],
  "Dispositions_props": [],
  "Categories": ["café"]
}
```

This structured representation reduces ambiguity before prompt generation.

---

# ✍️ 4. Automatic Prompt Construction

The structured information is transformed into a natural-language prompt.

The prompt builder automatically combines:

- Brand information
- Textual content
- Objects
- Colors
- Styles
- Typography
- Layout
- Categories

Example:

```text
Logo vectoriel pour CAFÉ (café), mettant en scène tasse,
dans un style moderne, avec une palette tasse: noire,
et une typographie CAFÉ: élégante.
Fond neutre, lisible, net.
```

The system also generates a negative prompt to reduce unwanted visual characteristics.

Example:

```text
Éviter: photoréalisme, 3D, textures lourdes,
dégradés marqués, ombres dures, éléments non listés,
surcharge, pixelisation, bruit.
```

---

# 🎨 5. Image Generation

The final prompt is sent to:

**Stable Diffusion v1.5**

combined with a trained:

**LoRA adapter**

The system uses multiple random seeds to generate different visual interpretations of the same description.

Current seeds:

```text
7
21
42
87
```

This produces four different logo candidates.

---

# 🔲 6. Multi-Seed Generation

For each request, four images are generated.

```text
             Logo Generation
                    │
       ┌────────────┼────────────┐
       │            │            │
     Seed 7       Seed 21      Seed 42      Seed 87
       │            │            │             │
       ▼            ▼            ▼             ▼
    Logo 1        Logo 2       Logo 3        Logo 4
       └────────────┴────────────┴─────────────┘
                           │
                           ▼
                       2×2 Grid
```

This gives the user several alternatives instead of a single result.

---

# ⚙️ Technologies Used

## Programming

- Python

## NLP

- Hugging Face Transformers
- CamemBERT
- Token Classification
- Sequence Classification

## Generative AI

- Stable Diffusion
- LoRA
- Diffusers
- PyTorch

## API

- FastAPI
- Uvicorn
- Pydantic

## Image Processing

- Pillow
- Base64 encoding

## Deployment / Testing

- Google Colab
- NVIDIA GPU
- Ngrok

## Data Processing

- Pandas
- NumPy
- JSON

---

# 📂 Project Structure

```text
text-to-logo-ai/
│
├── api/
│   │
│   ├── app.py
│   │
│   ├── relation_extractor.py
│   │
│   ├── constructionpromptautomatiquement.py
│   │
│   └── model_validator.py
│
├── README.md
│
└── requirements.txt
```

---

# 📄 Main Components

## `api/app.py`

Main FastAPI application.

Responsibilities:

- API configuration
- CORS configuration
- Loading Stable Diffusion
- Loading LoRA
- Receiving textual descriptions
- Calling the NLP pipeline
- Building prompts
- Generating logos
- Returning results
- Saving generated images

Main pipeline endpoint:

```text
POST /full_pipeline2/
```

---

## `api/relation_extractor.py`

Responsible for semantic relation extraction.

Main responsibilities:

- Loading the relation extraction model
- Preparing entity pairs
- Building CamemBERT inputs
- Predicting relations
- Computing confidence scores
- Returning structured relation results

---

## `api/constructionpromptautomatiquement.py`

Responsible for automatic prompt construction.

Main responsibilities:

- Entity normalization
- Relation normalization
- JSON block construction
- Hybrid fusion
- Cleaning
- French normalization
- Prompt generation
- Negative prompt generation

---

## `api/model_validator.py`

Contains the optional prompt validation module based on:

```text
Mistral-7B-Instruct
+
LoRA
```

This module can validate and correct the generated prompt while respecting the original description.

The validation stage can be enabled when the required model is available.

---

# 🔄 Complete Processing Pipeline

```text
                 ┌──────────────────────┐
                 │       User           │
                 └──────────┬───────────┘
                            │
                            ▼
                 ┌──────────────────────┐
                 │ Textual Description  │
                 └──────────┬───────────┘
                            │
                            ▼
                 ┌──────────────────────┐
                 │       FastAPI        │
                 └──────────┬───────────┘
                            │
                            ▼
                 ┌──────────────────────┐
                 │    CamemBERT NER     │
                 └──────────┬───────────┘
                            │
                            ▼
                 ┌──────────────────────┐
                 │ Extracted Entities   │
                 └──────────┬───────────┘
                            │
                            ▼
                 ┌──────────────────────┐
                 │ Relation Extraction  │
                 └──────────┬───────────┘
                            │
                            ▼
                 ┌──────────────────────┐
                 │ Hybrid JSON Block    │
                 └──────────┬───────────┘
                            │
                            ▼
                 ┌──────────────────────┐
                 │ Prompt Construction  │
                 └──────────┬───────────┘
                            │
                            ▼
                 ┌──────────────────────┐
                 │  Stable Diffusion    │
                 │       + LoRA         │
                 └──────────┬───────────┘
                            │
                            ▼
                 ┌──────────────────────┐
                 │ 4 Generated Logos    │
                 └──────────┬───────────┘
                            │
                            ▼
                 ┌──────────────────────┐
                 │      2×2 Grid        │
                 └──────────────────────┘
```

---

# 🌐 API Endpoints

The application exposes several REST endpoints.

## Root

```http
GET /
```

Returns API information.

---

## Named Entity Recognition

```http
POST /predict_entities/
```

Example request:

```json
{
  "text": "Un logo moderne avec une tasse noire."
}
```

Example response:

```json
{
  "entities": [
    {
      "text": "logo",
      "label": "Objets",
      "start": 6,
      "end": 10
    }
  ]
}
```

---

## Relation Extraction

```http
POST /relation
```

Receives the description and detected entities and returns predicted relations.

---

## Prompt Construction

```http
POST /build_prompts/
```

Builds:

- JSON block
- Rich prompt
- Negative prompt

---

## Prompt Validation

```http
POST /validateprompt
```

Uses the optional Mistral + LoRA validation module.

---

## Logo Generation

```http
POST /generate
```

Generates multiple logo variations from a prompt.

---

## Complete Pipeline

```http
POST /full_pipeline2/
```

This endpoint executes the complete workflow:

```text
Text
 ↓
NER
 ↓
Relation Extraction
 ↓
JSON Block
 ↓
Prompt Generation
 ↓
Stable Diffusion + LoRA
 ↓
4 Logos
 ↓
2×2 Grid
```

---

# 📥 Example Input

```json
{
  "text": "Un logo moderne pour une marque de café avec une tasse noire, un style minimaliste et une typographie élégante."
}
```

---

# 📤 Example Output

The API returns:

```json
{
  "entities": [],
  "relations": [],
  "block": {},
  "prompt_used": "...",
  "logos_count": 4,
  "logos": [],
  "grid_logo": "..."
}
```

The actual values depend on the input description and model predictions.

---

# 🧪 Example Use Case

### Input

```text
Créer un logo moderne pour une marque de café.
Le logo contient une tasse noire avec une typographie élégante.
```

### Processing

```text
Text
 ↓
NER
 ↓
Objets = tasse
Couleurs = noire
Style = moderne
Typographie = élégante
 ↓
Relation Extraction
 ↓
Structured JSON
 ↓
Prompt Builder
 ↓
Stable Diffusion + LoRA
```

### Output

```text
Logo 1
Logo 2
Logo 3
Logo 4

        ┌─────────┬─────────┐
        │ Logo 1  │ Logo 2  │
        ├─────────┼─────────┤
        │ Logo 3  │ Logo 4  │
        └─────────┴─────────┘
```

---

# ☁️ Execution Environment

The project was developed and tested using **Google Colab** with GPU acceleration.

The models used in the project are computationally intensive, especially the Stable Diffusion and large language model components.

The API can be exposed publicly during experimentation using Ngrok.

Architecture:

```text
Google Colab
     │
     ├── Python
     ├── PyTorch
     ├── Transformers
     ├── Stable Diffusion
     └── FastAPI
            │
            ▼
          Ngrok
            │
            ▼
     Public API Endpoint
```

---

# 📦 Installation

Clone the repository:

```bash
git clone https://github.com/amal5598/text-to-logo-ai.git
```

Enter the project:

```bash
cd text-to-logo-ai
```

Install dependencies:

```bash
pip install -r requirements.txt
```

---

# ⚠️ Models and Checkpoints

The trained models and checkpoints are not included directly in the repository because of their large size.

The project requires access to:

```text
CamemBERT NER model
CamemBERT Relation Extraction model
Stable Diffusion v1.5
LoRA checkpoint
```

The paths used during development can be configured according to the local or Google Drive environment.

Example:

```python
MODEL_DIR = "/path/to/model"
CHECKPOINT_PATH = "/path/to/lora/checkpoint"
```

---

# 🔐 Security Note

API keys and authentication tokens must **never be committed to GitHub**.

For example, Ngrok authentication tokens should be stored as environment variables or secrets.

```python
import os

NGROK_TOKEN = os.getenv("NGROK_TOKEN")
```

Do not place private tokens directly inside source files.

---

# 📊 Model Architecture

## NER Model

```text
Input Text
     │
     ▼
CamemBERT Tokenizer
     │
     ▼
Fine-Tuned CamemBERT
     │
     ▼
Token Classification
     │
     ▼
Entity Aggregation
     │
     ▼
Structured Entities
```

---

## Relation Extraction Model

```text
Description
     │
     ▼
Entity Pair Construction
     │
     ▼
CamemBERT Tokenizer
     │
     ▼
Fine-Tuned CamemBERT
     │
     ▼
Sequence Classification
     │
     ▼
Relation + Confidence
```

---

## Generative Model

```text
Generated Prompt
      │
      ▼
Stable Diffusion v1.5
      │
      +
      │
     LoRA
      │
      ▼
Image Generation
      │
      ▼
4 Logo Variations
```

---

# 📈 Advantages

The proposed system provides several advantages:

### Structured Understanding

The system does not directly send the raw description to the image generator.

Instead, it first extracts and structures semantic information.

### Semantic Relationships

Relation extraction allows the system to understand relationships between entities.

### Automatic Prompt Engineering

Prompts are automatically generated from the extracted information.

### Multiple Results

Four different seeds provide several visual alternatives.

### Modular Architecture

Each component can be independently improved:

```text
NER
 ↓
Relation Extraction
 ↓
Prompt Builder
 ↓
Image Generation
```

---

# 🔬 Future Improvements

Several improvements can be considered for future versions.

## Front-End Interface

Develop a dedicated web interface allowing users to:

- Enter descriptions
- Preview extracted entities
- Visualize relations
- Edit generated prompts
- Generate logos
- Download results

---

## Model Improvements

Possible improvements include:

- Better NER training
- More relation classes
- Larger logo datasets
- Improved LoRA fine-tuning
- More specialized diffusion models
- Automatic logo quality evaluation

---

## Prompt Validation

The optional Mistral + LoRA module can be integrated as an additional validation layer:

```text
Generated Prompt
       │
       ▼
Mistral + LoRA
       │
       ▼
Validated Prompt
       │
       ▼
Stable Diffusion
```

---

## Deployment

The system can later be deployed using:

- Docker
- Cloud GPU
- Hugging Face Spaces
- AWS
- Azure
- Google Cloud

---

# 📚 Research Contribution

The project combines several AI techniques into a unified pipeline:

```text
Natural Language Processing
          +
Named Entity Recognition
          +
Relation Extraction
          +
Prompt Engineering
          +
Large Language Models
          +
Generative AI
          +
Diffusion Models
          +
LoRA Fine-Tuning
```

This combination enables a structured transformation:

```text
Natural Language
       ↓
Semantic Representation
       ↓
Structured Prompt
       ↓
Generated Visual Concept
```

---

# 👩‍💻 Author

**Amal Boubakri**

Master's Degree in Data Science

Interests:

- Data Science
- Artificial Intelligence
- NLP
- Generative AI
- Large Language Models
- Computer Vision
- Data Engineering

GitHub:

https://github.com/amal5598

---

# ⭐ Project

If you find this project interesting, feel free to explore the repository and follow the development of the project.

**Text-to-Logo AI — From Natural Language to Generative Logo Design.**
