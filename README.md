# Synthetic Data Generation Project

This project focuses on generating high-quality synthetic data for machine learning applications using state-of-the-art language models for Docker commands. The project leverages Llama-3.1-405b for content generation and Nemotron-4-340b-reward for quality assessment.

## Project Structure

```
.
├── create_dataset.ipynb      # Main notebook for dataset creation
├── synthetic_data.jsonl      # Raw synthetic data
└── synthetic_data_filtered.jsonl  # Filtered synthetic data
```

## Detailed Project Workflow

```
┌─────────────────────────────────────────────────────────────────────────┐
│                        Topic Processing Phase                            │
│  ┌─────────────┐    ┌─────────────┐    ┌─────────────┐                 │
│  │ Main Topic  │───▶│ Subtopics   │───▶│ Questions   │                 │
│  │ Input       │    │ Generation  │    │ Generation  │                 │
│  │             │    │ (Llama-3.1) │    │ (Llama-3.1) │                 │
│  └─────────────┘    └─────────────┘    └─────────────┘                 │
└───────────────────────────────┬─────────────────────────────────────────┘
                                ▼
┌─────────────────────────────────────────────────────────────────────────┐
│                        Response Generation Phase                         │
│  ┌─────────────┐    ┌─────────────┐    ┌─────────────┐                 │
│  │ Question    │───▶│ Response    │───▶│ Quality     │                 │
│  │ Processing  │    │ Generation  │    │ Assessment  │                 │
│  │ (Llama-3.1) │    │ (Llama-3.1) │    │ (Nemotron-4)│                 │
│  └─────────────┘    └─────────────┘    └─────────────┘                 │
└───────────────────────────────┬─────────────────────────────────────────┘
                                ▼
┌─────────────────────────────────────────────────────────────────────────┐
│                        Quality Control Phase                             │
│  ┌─────────────┐    ┌─────────────┐    ┌─────────────┐                 │
│  │ Response    │───▶│ Quality     │───▶│ Dataset     │                 │
│  │ Evaluation  │    │ Filtering   │    │ Creation    │                 │
│  │ (Nemotron-4)│    │ (Threshold) │    │ (JSONL)     │                 │
│  └─────────────┘    └─────────────┘    └─────────────┘                 │
└─────────────────────────────────────────────────────────────────────────┘
```

## Data Generation Process

The data generation process involves:
1. Taking a main topic as input
2. Using Llama-3.1-405b-instruct to generate relevant subtopics
3. Creating questions for each subtopic using Llama-3.1-405b-instruct
4. Generating detailed responses using Llama-3.1-405b-instruct
5. Assessing response quality using Nemotron-4-340b-reward
6. Filtering and saving high-quality responses

### Quality Assessment

The quality assessment process includes:
- Using Nemotron-4-340b-reward to evaluate response quality
- Setting quality thresholds for filtering
- Removing low-quality or irrelevant responses
- Ensuring response coherence and relevance

## Data Files

- `synthetic_data.jsonl`: Contains the raw synthetic data including all generated responses
- `synthetic_data_filtered.jsonl`: Contains only the high-quality responses that passed the quality assessment

## Models Used

- **llama-3.1-405b-instruct**: Used for generating subtopics, questions, and responses
- **nemotron-4-340b-reward**: Used for quality assessment and filtering