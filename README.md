# Multi-Document & Multi-Agent RAG System

This project implements a sophisticated Retrieval-Augmented Generation (RAG) system using multiple agents to process and query financial reports. The system is built using LlamaIndex and integrates with OpenAI's models for enhanced performance.

## Project Overview

The system is designed to:

- Process multiple types of financial reports (annual reports and balance of banks)
- Clean and preprocess Markdown files for better chunking
- Implement a hierarchical multi-agent system with:
  - Low-level agents specialized in specific report types
  - A top-level agent that routes queries to appropriate specialized agents
- Support bilingual queries and responses (Arabic and English)

## Setup

### Prerequisites

- Python 3.x
- OpenAI API key

### Installation

1. Clone the repository:

```bash
git clone [repository-url]
cd [repository-name]
```

2. Install required packages:

```python
pip install llama-index openai
```

3. Set up your OpenAI API key:

```python
import os
os.environ["OPENAI_API_KEY"] = "your-api-key-here"
```

## Project Structure

```
.
├── Data/
│   ├── التقارير السنوية/      # Annual Reports
│   └── ميزان المدفوعات/       # Balance of Banks Reports
├── Multi_Agent_RAG.ipynb       # Main implementation notebook
└── README.md
```

## Features

### 1. Preprocessing Tools

- `sanitize_name()`: Cleans file names for compatibility
- `merge_consecutive_headers()`: Improves document chunking by merging consecutive headers
- `clean_markdown_files()`: Processes markdown files for better indexing

### 2. Model Configuration

- Uses OpenAI's GPT-4 for LLM capabilities
- Implements OpenAI's text-embedding-3-large for embeddings

### 3. Agent Architecture

#### Low-Level Agents

- Specialized in specific report types
- Built using file-level vector indices
- Each file has its own query engine

#### Top-Level Agent

- Routes queries to appropriate specialized agents
- Uses semantic search to find relevant tools
- Supports complex queries spanning multiple report types

### 4. Query Processing

Two main query processing approaches:

1. Direct Top-Level Agent:

   - Simple query routing
   - Single-step response generation

2. Agent Runner with Worker:
   - Supports loop reasoning
   - Better for complex queries requiring multiple steps

## Usage Examples

### Basic Query

```python
response = top_agent.query("ماهي نسبة البطالة في التقارير السنوية لعام 2010؟")
```

### Complex Multi-Document Query

```python
response = agent.query("في عام 2008, ماهي نسبة البطالة في امريكا وماهي قيمة الحساب الجاري في ليبيا؟")
```

### Comparative Analysis

```python
response = agent.query("قارن بين معدلات التضخم في التقارير السنوية لعام 2013 وعام 2014")
```

## Best Practices

1. **Data Preparation**

   - Always clean markdown files before indexing
   - Use the cleaned files for vector store creation

2. **Query Formation**

   - Be specific with date ranges and metrics
   - Use Arabic for optimal results with financial reports

3. **System Usage**
   - Use the Agent Runner for complex queries
   - Use the direct top-level agent for simple queries

## Limitations

- Maximum context window limitations from OpenAI models
- Processing time depends on the number of documents
- Requires proper markdown formatting for optimal results

## Contributing

Feel free to contribute to this project by:

1. Forking the repository
2. Creating a feature branch
3. Submitting a pull request

## License

[Specify your license here]
