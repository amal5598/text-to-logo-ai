# 🧠 TEXT2LOGO AI

> End-to-end Artificial Intelligence system for transforming natural-language logo descriptions into structured design information, optimized prompts, and generated logo concepts.

---

## 📌 Overview

TEXT2LOGO AI is an intelligent generative AI system designed to transform a natural-language description of a logo into one or more generated logo concepts.

The system combines:

- Natural Language Processing
- Named Entity Recognition
- Semantic Relation Extraction
- Prompt Engineering
- Large Language Models
- LoRA Fine-Tuning
- Stable Diffusion
- FastAPI

The complete pipeline is:

```text
Natural Language Description
            ↓
       Entity Extraction
            ↓
    Relation Extraction
            ↓
   Structured JSON Block
            ↓
   Automatic Prompt Building
            ↓
     Prompt Validation
            ↓
 Stable Diffusion + LoRA
            ↓
   Multiple Logo Candidates

### 🎯 Project Objective

The main objective of TEXT2LOGO AI is to understand a textual description of a logo and transform its semantic information into a visual representation.

The system is designed to preserve:

Objects
Colors
Styles
Typography
Textual content
Brand names
Spatial relationships
Layout
Composition

Example:

Créer un logo moderne pour une marque de café appelée CaféNova,
avec une tasse noire, une typographie élégante et le texte placé
sous la tasse.

The system extracts the relevant information, constructs a structured representation, generates a prompt, validates it, and finally generates several logo candidates.

✨ Main Features
🧠 Natural Language Understanding

The system analyzes the input description using a fine-tuned CamemBERT model.

It identifies entities related to logo design.

Supported entity categories include:

Objets
Couleurs
Styles
Typographies
Contenu_textuel
Marque
disposition
Categories
🔗 Semantic Relation Extraction

The system identifies semantic relationships between extracted entities.

Supported relations:

A_COMME_COULEUR
A_COMME_DISPOSITION
A_COMME_STYLE
A_COMME_TYPOGRAPHIE

Example:

tasse → A_COMME_COULEUR → noire


tasse → A_COMME_STYLE → moderne


CaféNova → A_COMME_TYPOGRAPHIE → élégante
🧩 Structured Semantic Representation

The extracted information is transformed into a structured JSON block.

Example:

{
  "Marque": ["CaféNova"],
  "Contenu_textuel": [],
  "Objets": ["tasse"],
  "Couleurs": [
    {
      "cible": "tasse",
      "couleur": "noire"
    }
  ],
  "Styles": [
    {
      "cible": "tasse",
      "style": "moderne"
    }
  ],
  "Typographies": [
    {
      "cible": "CaféNova",
      "typo": "élégante"
    }
  ],
  "Dispositions": [],
  "Dispositions_props": [],
  "Categories": []
}
✍️ Automatic Prompt Construction

The module:

constructionpromptautomatiquement.py

is responsible for transforming the structured information into a natural-language prompt.

The system uses a hybrid strategy combining:

Extracted entities
Semantic relations
Rule-based processing
Text normalization
Deduplication
Garbage filtering
French normalization
Semantic retargeting

Example generated prompt:

Logo vectoriel pour CaféNova mettant en scène une tasse
dans un style moderne avec une palette noire et une typographie
élégante et le texte présent : CaféNova. Fond neutre, lisible, net.
🤖 Prompt Validation

A Mistral-7B-Instruct-v0.3 model combined with LoRA fine-tuning was used for prompt validation.

The validator receives:

Description originale
        +
Structured JSON Block
        +
Generated Prompt

The model is instructed to:

Never invent new elements
Preserve existing information
Restore missing information when necessary
Preserve the intended composition
Avoid unnecessary modifications
Return one final sentence
🎨 Logo Generation

The image generation module uses:

Stable Diffusion 1.5
+
LoRA Fine-Tuning

Configuration:

Image Size       : 512 × 512
Inference Steps  : 50
Guidance Scale   : 8.0
Seeds            : 7, 21, 42, 87

Four different seeds are used to generate four visual alternatives.

The system also creates a 2×2 grid containing the four generated logos.

🏗️ System Architecture
                         TEXT2LOGO AI
                              │
                              ▼
                  ┌──────────────────────┐
                  │ Natural Language      │
                  │ Logo Description      │
                  └──────────┬───────────┘
                             │
                             ▼
                  ┌──────────────────────┐
                  │     CamemBERT NER    │
                  │  Entity Recognition  │
                  └──────────┬───────────┘
                             │
                             ▼
                  ┌──────────────────────┐
                  │ Extracted Entities    │
                  └──────────┬───────────┘
                             │
                             ▼
                  ┌──────────────────────┐
                  │ CamemBERT Relation   │
                  │ Classification       │
                  └──────────┬───────────┘
                             │
                             ▼
                  ┌──────────────────────┐
                  │ Semantic Relations    │
                  └──────────┬───────────┘
                             │
                             ▼
                  ┌──────────────────────┐
                  │ Hybrid Semantic Block │
                  │ JSON Representation   │
                  └──────────┬───────────┘
                             │
                             ▼
                  ┌──────────────────────┐
                  │ Automatic Prompt      │
                  │ Construction           │
                  └──────────┬───────────┘
                             │
                             ▼
                  ┌──────────────────────┐
                  │ Mistral-7B + LoRA     │
                  │ Prompt Validation     │
                  └──────────┬───────────┘
                             │
                             ▼
                  ┌──────────────────────┐
                  │ Final Generation      │
                  │ Prompt                │
                  └──────────┬───────────┘
                             │
                             ▼
                  ┌──────────────────────┐
                  │ Stable Diffusion 1.5 │
                  │ + LoRA                │
                  └──────────┬───────────┘
                             │
                             ▼
                  ┌──────────────────────┐
                  │ 4 Logo Candidates     │
                  │ + 2×2 Grid            │
                  └──────────────────────┘
🔄 Complete AI Pipeline
Input Description
       ↓
NER CamemBERT
       ↓
Entity Extraction
       ↓
Relation Extraction
       ↓
Hybrid Semantic Representation
       ↓
Automatic Prompt Construction
       ↓
Mistral + LoRA Prompt Validation
       ↓
Stable Diffusion + LoRA
       ↓
4 Generated Logos
       ↓
2×2 Visualization
🛠️ Technologies
Programming Language
Python
NLP
Hugging Face Transformers
CamemBERT
Token Classification
Sequence Classification
Large Language Models
Mistral-7B-Instruct-v0.3
LoRA
PEFT
BitsAndBytes
4-bit Quantization
Generative AI
Stable Diffusion 1.5
Diffusers
LoRA
Prompt Engineering
Deep Learning
PyTorch
API
FastAPI
Uvicorn
Pydantic
CORS
Data Processing
Pandas
NumPy
JSON
Regex
Development Environment
Google Colab
Google Drive
Ngrok
📂 Project Structure
text-to-logo-ai/
│
├── api/
│   ├── app.py
│   ├── constructionpromptautomatiquement.py
│   ├── model_validator.py
│   └── relation_extractor.py
│
├── README.md
│
└── models/
    ├── NER/
    ├── relation_model/
    ├── mistral_lora/
    └── stable_diffusion_lora/
📄 API Modules
app.py

Main FastAPI application.

Responsibilities:

API configuration
Model loading
Request validation
Complete pipeline execution
Logo generation
Image encoding
Image saving
API endpoints
relation_extractor.py

Responsible for:

Entity pair extraction
Relation input construction
CamemBERT relation prediction
Confidence calculation
Relation output formatting
constructionpromptautomatiquement.py

Responsible for:

Entity normalization
Relation normalization
Structured JSON construction
Hybrid merging
Cleaning
Deduplication
French normalization
Prompt construction
model_validator.py

Responsible for:

Loading Mistral
Loading LoRA adapters
Prompt validation
Prompt correction
Final prompt generation
🤖 Model Architecture
Component	Model	Task
NER	CamemBERT	Entity Recognition
Relation Extraction	CamemBERT	Relation Classification
Prompt Validation	Mistral-7B-Instruct-v0.3 + LoRA	Prompt Correction
Image Generation	Stable Diffusion 1.5 + LoRA	Logo Generation
🧠 NER Module

The NER model is fine-tuned specifically for the TEXT2LOGO domain.

The model identifies:

Objets
Couleurs
Styles
Typographies
Contenu_textuel
Marque
disposition
Categories

Example:

Input:
Un logo moderne avec une tasse noire et le texte CaféNova
en typographie élégante.


Entities:


tasse       → Objets
moderne     → Styles
noire       → Couleurs
CaféNova    → Contenu_textuel
élégante    → Typographies
🔗 Relation Extraction

The relation classifier identifies semantic dependencies between entities.

Example:

tasse
   │
   ├── A_COMME_COULEUR ──> noire
   │
   └── A_COMME_STYLE ──> moderne


CaféNova
   │
   └── A_COMME_TYPOGRAPHIE ──> élégante

This information is used to build a structured representation.

🧩 Hybrid Strategy

The prompt builder supports three modes:

entities
relations
hybrid
Entities

Uses only extracted entities.

Relations

Uses only semantic relations.

Hybrid

Combines both.

The final system uses the hybrid mode:

Entities
    +
Relations
    ↓
Hybrid Semantic Block
    ↓
Prompt

The hybrid approach provides a richer representation of the original description.

🧹 Data Cleaning

The system applies several cleaning operations:

Text normalization
Label normalization
Relation normalization
Duplicate removal
Invalid token removal
Empty value filtering
French normalization
Entity retargeting

Invalid tokens such as:

nan
none
null
-
—
?

are filtered before prompt construction.

✍️ Prompt Generation

The prompt generator creates a rich French prompt.

The generated prompt can contain:

Brand
Category
Objects
Style
Colors
Typography
Composition
Text
Background

Example:

Logo vectoriel pour CaféNova mettant en scène une tasse
dans un style moderne avec une palette noire et une typographie
élégante. Fond neutre, lisible, net.
🤖 Mistral + LoRA

The prompt validation model uses:

Base Model:
mistralai/Mistral-7B-Instruct-v0.3

with:

LoRA
PEFT
4-bit Quantization
BitsAndBytes

The use of quantization reduces memory requirements and makes the model more suitable for GPU environments such as Google Colab.

🎨 Stable Diffusion + LoRA

The image generation module uses:

runwayml/stable-diffusion-v1-5

with a LoRA adapter trained for the logo generation domain.

Generation parameters:

Steps       = 50
Guidance    = 8.0
Resolution  = 512 × 512


Seeds:
7
21
42
87
🚀 FastAPI

The entire pipeline is exposed through a REST API.

The API allows the different modules to be tested independently or executed as a complete pipeline.

🔌 API Endpoints
GET /

Returns the API status.

{
  "message": "Bienvenue sur l'API TEXT2LOGO"
}
POST /predict_entities/

Extracts entities from a text.

Request
{
  "text": "Logo moderne avec une tasse noire et CaféNova."
}
Response
{
  "entities": [
    {
      "text": "tasse",
      "label": "Objets"
    },
    {
      "text": "noire",
      "label": "Couleurs"
    }
  ]
}
POST /relation

Predicts semantic relations.

POST /build_prompts/

Builds the structured JSON representation and generates the prompt.

POST /validateprompt

Validates a generated prompt using Mistral + LoRA.

POST /generate

Generates multiple logo candidates.

POST /full_pipeline/

Executes the complete system.

Input
 ↓
NER
 ↓
Relations
 ↓
Structured Block
 ↓
Prompt Construction
 ↓
Prompt Validation
 ↓
Stable Diffusion
 ↓
4 Logo Candidates
GET /grid.png

Returns the generated 2×2 grid.

GET /logo/{seed}

Returns a specific generated logo.

Example:

/logo/42
📊 Evaluation

The evaluation was conducted at multiple levels:

Entity Recognition
Semantic Relation Extraction
Prompt Generation
Image Generation
Human Evaluation
📈 Entity Recognition Evaluation

Two models were evaluated:

CamemBERT
Multilingual BERT

The models were trained for 10 epochs.

Training Loss, Validation Loss, Precision, Recall and F1-score were monitored.

Results
Model	Epoch	Train Loss	Validation Loss	Precision	Recall	F1-score
CamemBERT	1	0.3619	0.3613	0.8900	0.8920	0.8706
CamemBERT	5	0.3623	0.3541	0.8520	0.8536	—
Multilingual BERT	1	0.3726	0.3681	0.8927	0.8681	0.8724
Multilingual BERT	5	0.3588	0.3618	0.8941	0.8693	0.8810

Both models demonstrate strong performance for entity recognition in the TEXT2LOGO domain.

🔗 Relation Extraction Evaluation

The CamemBERT relation model was evaluated on four semantic relations.

Relation	Precision	Recall	F1-score	Support
A_COMME_COULEUR	1.00	1.00	1.00	673
A_COMME_DISPOSITION	1.00	1.00	1.00	357
A_COMME_STYLE	1.00	1.00	1.00	842
A_COMME_TYPOGRAPHIE	0.99	0.98	0.99	130
Macro Average	1.00	1.00	0.996	2002

The relation model achieves a macro F1-score of approximately:

0.996

indicating very strong classification performance on the evaluated relation classes.

📝 Prompt Generation Evaluation

Two models were compared:

Gemma-2B-it
Mistral

The evaluation used:

BLEU
ROUGE-L
SBERT Similarity
BERTScore Precision
BERTScore Recall
BERTScore F1
Input-Human Similarity
Results
Metric	Gemma-2B-it	Mistral
BLEU	0.582	0.742
ROUGE-L	0.865	0.856
SBERT Similarity	0.771	0.880
BERTScore Precision	0.585	0.771
BERTScore Recall	0.747	0.844
BERTScore F1	0.656	0.805
Input-Human Similarity	0.615	0.615
📌 Prompt Evaluation Analysis
Lexical and Structural Evaluation

Mistral achieves a higher BLEU score:

Mistral       = 0.742
Gemma-2B-it   = 0.582

This indicates that Mistral reproduces the lexical structure of human-corrected prompts more effectively.

The ROUGE-L scores are relatively close:

Gemma-2B-it   = 0.865
Mistral       = 0.856

This shows that both models provide good content coverage.

🧠 Semantic and Coherence Evaluation

Mistral performs better on the semantic metrics.

SBERT Similarity:

Gemma-2B-it = 0.771
Mistral     = 0.880

BERTScore F1:

Gemma-2B-it = 0.656
Mistral     = 0.805

Mistral therefore generates prompts that are semantically closer to the human-corrected references.

👤 Human Reference Similarity

The similarity between the original prompt and the human-corrected prompt is:

0.615

for both models.

The SBERT similarity between generated prompts and human references is:

Gemma-2B-it = 0.771
Mistral     = 0.880

This confirms the better semantic fidelity of Mistral.

🏆 Prompt Model Conclusion

Based on the evaluation results, Mistral-7B-Instruct-v0.3 provides the strongest overall performance.

Mistral generates prompts that are:

More coherent
More semantically faithful
More precise
Better structured
Closer to human corrections

Therefore, Mistral + LoRA was selected for prompt validation.

🖼️ Image Generation Evaluation

The generated images were evaluated using automatic and human-based metrics.

The automatic evaluation considers:

CLIP
SSIM
LPIPS
Text-Image Similarity

A global score was calculated using:

Score_global = (Score_auto + Score_humain) / 2

Where:

Score_auto
=
Normalized automatic score


Score_humain
=
Average human evaluation score
🎨 Stable Diffusion Evaluation

Two models were compared:

Stable Diffusion 1.5 pre-trained
Stable Diffusion 1.5 + LoRA
Results
Model	CLIP	SSIM	LPIPS	Text-Image	Human Score
Stable Diffusion 1.5 + LoRA	0.677	0.404	0.668	0.292	3.472
Stable Diffusion 1.5	0.634	0.332	0.752	0.296	1.224

The LoRA fine-tuned model obtains:

CLIP = 0.677

compared with:

CLIP = 0.634

for the pre-trained Stable Diffusion model.

The human evaluation is also significantly higher:

LoRA = 3.472
SD 1.5 = 1.224

These results indicate that domain-specific LoRA fine-tuning improves the generation of logo concepts.

🏆 Overall Evaluation

The evaluation confirms the effectiveness of the different components of the TEXT2LOGO pipeline.

NER

CamemBERT demonstrates strong entity recognition performance.

Relations

CamemBERT achieves a macro F1-score of approximately 0.996.

Prompt Generation

Mistral performs better than Gemma-2B-it on the main semantic metrics.

Image Generation

Stable Diffusion + LoRA achieves better results than the pre-trained Stable Diffusion 1.5 model, particularly according to human evaluation.

🔬 End-to-End Example
Input
Créer un logo moderne pour une marque de café appelée CaféNova,
avec une tasse noire, une typographie élégante et le texte placé
sous la tasse.
Step 1 — Entity Extraction
CaféNova    → Marque
tasse       → Objets
noire       → Couleurs
moderne     → Styles
élégante    → Typographies
Step 2 — Relation Extraction
tasse → A_COMME_COULEUR → noire


tasse → A_COMME_STYLE → moderne


CaféNova → A_COMME_TYPOGRAPHIE → élégante
Step 3 — Structured Block
{
  "Marque": ["CaféNova"],
  "Contenu_textuel": [],
  "Objets": ["tasse"],
  "Couleurs": [
    {
      "cible": "tasse",
      "couleur": "noire"
    }
  ],
  "Styles": [
    {
      "cible": "tasse",
      "style": "moderne"
    }
  ],
  "Typographies": [
    {
      "cible": "CaféNova",
      "typo": "élégante"
    }
  ],
  "Dispositions": [],
  "Dispositions_props": [],
  "Categories": []
}
Step 4 — Prompt Construction
Logo vectoriel pour CaféNova mettant en scène une tasse
dans un style moderne avec une palette noire et une typographie
élégante. Fond neutre, lisible, net.
Step 5 — Prompt Validation

Mistral + LoRA validates the generated prompt against the original description.

Step 6 — Image Generation

Stable Diffusion + LoRA generates:

Seed 7
Seed 21
Seed 42
Seed 87

The four results are returned individually and as a 2×2 grid.

☁️ Development Environment

The project was developed and tested using Google Colab with GPU acceleration.

Google Colab was used because the pipeline requires significant computational resources for:

Mistral-7B
Stable Diffusion
LoRA inference
CamemBERT
GPU-based image generation

Models were stored and loaded from Google Drive during experimentation.

📦 Installation

Clone the repository:

git clone https://github.com/amal5598/text-to-logo-ai.git
cd text-to-logo-ai

Install the required packages:

pip install -r requirements.txt

Main dependencies:

fastapi
uvicorn
nest-asyncio
pyngrok
transformers
torch
seqeval
bitsandbytes
accelerate
peft
diffusers
safetensors
xformers
pandas
numpy
Pillow
▶️ Running the API

Start the FastAPI server:

uvicorn app:app --host 0.0.0.0 --port 8000

For Google Colab, Ngrok can be used to expose the API:

from pyngrok import ngrok


public_url = ngrok.connect(8000)


print("Public URL:", public_url)
🔐 Security Note

API tokens and authentication credentials must never be committed to the repository.

Use environment variables or secret management systems for:

NGROK_AUTH_TOKEN
API_KEYS
MODEL_KEYS

Example:

import os


NGROK_AUTH_TOKEN = os.getenv("NGROK_AUTH_TOKEN")
📊 End-to-End Output

For a single description, the system can return:

Entities
Relations
Structured JSON
Generated Prompt
Validated Prompt
4 Generated Logos
2×2 Logo Grid

Example response structure:

{
  "entities": [],
  "relations": [],
  "block": {},
  "prompt_used": "...",
  "logos_count": 4,
  "logos": [],
  "grid_logo": "..."
}
🚀 Main Contributions
1. Domain-Specific NER

Development of an entity recognition model adapted to logo descriptions.

2. Semantic Relation Extraction

Identification of semantic relationships between logo components.

3. Hybrid Semantic Representation

Combination of entity and relation information.

4. Automatic Prompt Engineering

Transformation of structured information into generation-ready prompts.

5. LLM-Based Prompt Validation

Use of Mistral + LoRA to improve prompt fidelity.

6. Domain-Specific Image Generation

Fine-tuning Stable Diffusion 1.5 using LoRA.

7. End-to-End AI Pipeline

Integration of NLP, LLM and Generative AI.

8. FastAPI Integration

Deployment of the complete pipeline as a REST API.

🔮 Future Improvements

Possible future improvements include:

Complete web interface
Authentication
User accounts
Database integration
Cloud GPU deployment
Logo download
Automatic logo ranking
Human feedback integration
Better typography rendering
Better text rendering inside logos
More logo categories
Multilingual support
Larger language models
Improved relation extraction
Improved LoRA datasets
Faster inference
Continuous evaluation
Automatic quality scoring
📚 Final Architecture
                         TEXT2LOGO AI
                              │
                              ▼
                  ┌──────────────────────┐
                  │ Natural Language      │
                  │ Description           │
                  └──────────┬───────────┘
                             │
                             ▼
                  ┌──────────────────────┐
                  │ CamemBERT NER         │
                  │ Entity Extraction     │
                  └──────────┬───────────┘
                             │
                             ▼
                  ┌──────────────────────┐
                  │ Semantic Relations    │
                  │ CamemBERT             │
                  └──────────┬───────────┘
                             │
                             ▼
                  ┌──────────────────────┐
                  │ Hybrid JSON Block     │
                  └──────────┬───────────┘
                             │
                             ▼
                  ┌──────────────────────┐
                  │ Prompt Construction   │
                  └──────────┬───────────┘
                             │
                             ▼
                  ┌──────────────────────┐
                  │ Mistral + LoRA        │
                  │ Prompt Validation     │
                  └──────────┬───────────┘
                             │
                             ▼
                  ┌──────────────────────┐
                  │ Final Prompt          │
                  └──────────┬───────────┘
                             │
                             ▼
                  ┌──────────────────────┐
                  │ Stable Diffusion 1.5 │
                  │ + LoRA                │
                  └──────────┬───────────┘
                             │
                             ▼
                  ┌──────────────────────┐
                  │ Multiple Logos        │
                  │ + 2×2 Grid            │
                  └──────────────────────┘
👩‍💻 Author

Amal Boubakri

Data Science & Artificial Intelligence

GitHub:

https://github.com/amal5598

Repository:

https://github.com/amal5598/text-to-logo-ai
