# 🤖 Text-to-Logo AI

An AI-powered system that transforms natural language descriptions into logo concepts using NLP, relation extraction, prompt engineering, and generative AI.

## 🚀 Overview

Text-to-Logo AI is an intelligent pipeline designed to automatically transform a textual logo description into structured visual specifications and generate multiple logo concepts.

The system combines Natural Language Processing, Transformer-based models, relation extraction, automatic prompt construction, and Stable Diffusion with LoRA.

## 🧠 Pipeline

```text
Natural Language Description
            ↓
      CamemBERT NER
            ↓
     Entity Extraction
            ↓
    Relation Extraction
            ↓
      Structured JSON
            ↓
   Automatic Prompt Construction
            ↓
     Prompt Optimization
            ↓
   Stable Diffusion + LoRA
            ↓
      Generated Logos
```

## ✨ Main Features

- 📝 Natural language logo description processing
- 🔍 Named Entity Recognition (NER)
- 🔗 Relation extraction between entities
- 🧩 Automatic construction of structured JSON specifications
- ✍️ Automatic prompt generation
- 🤖 Transformer-based NLP models
- 🎨 Stable Diffusion for logo generation
- 🧠 LoRA fine-tuning
- ⚡ FastAPI REST API
- 🖼️ Multiple logo generation using different seeds

## 🛠️ Technologies

### NLP & AI

- Python
- PyTorch
- Hugging Face Transformers
- CamemBERT
- Mistral 7B
- LoRA / PEFT

### Generative AI

- Stable Diffusion
- Hugging Face Diffusers
- Prompt Engineering

### Backend

- FastAPI
- Uvicorn
- Pydantic

### Data Processing

- Pandas
- NumPy
- JSON

## 📁 Project Structure

```text
text-to-logo-ai/
│
├── api/
│   ├── app.py
│   ├── constructionpromptautomatiquement.py
│   ├── model_validator.py
│   └── relation_extractor.py
│
└── README.md
```

## 🔍 Components

### 1. Named Entity Recognition

CamemBERT is used to identify important elements from the logo description, such as:

- Objects
- Colors
- Styles
- Typography
- Text content
- Brand names
- Layout / disposition

### 2. Relation Extraction

The system identifies relationships between extracted entities.

Examples:

```text
Object → Color
Object → Style
Text → Typography
Object → Layout
```

The extracted relations are then transformed into a structured representation.

### 3. Automatic Prompt Construction

The extracted entities and relations are combined to create a structured JSON block.

This information is then transformed into a detailed French prompt adapted for image generation.

### 4. Generative AI

Stable Diffusion combined with LoRA is used to generate logo concepts from the final prompt.

Multiple seeds are used to generate different visual variations.

## ⚡ API

The backend is implemented using FastAPI.

Main endpoints include:

```text
POST /predict_entities/
POST /relation
POST /build_prompts/
POST /validateprompt
POST /generate
POST /full_pipeline/
```

## 💡 Example

### Input

```text
Créer un logo moderne pour une marque de café,
avec une tasse noire, des couleurs marron et beige,
et le nom "Coffee House" en typographie élégante.
```

### Processing

```text
Entities
    ↓
Objects
Colors
Typography
Text
Style
    ↓
Relations
    ↓
Structured JSON
    ↓
Generated Prompt
    ↓
Stable Diffusion
```

### Output

The system generates multiple logo variations from the same description using different random seeds.

## 🎯 Objective

The objective of this project is to demonstrate how NLP and Generative AI can be combined to build an end-to-end intelligent system capable of understanding natural language and transforming it into visual content.

## 👩‍💻 Author

**Amal Boubakri**

Data Science & AI

GitHub: https://github.com/amal5598
