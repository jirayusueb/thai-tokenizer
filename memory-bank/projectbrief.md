# Project Brief: Thai Tokenizer

## Overview

A Python-based Thai text tokenization library designed to effectively segment Thai text into meaningful units (words, syllables, or characters) for natural language processing applications.

## Core Requirements

- **Primary Goal**: Develop a robust Thai text tokenizer using MLX LoRA fine-tuning
- **Base Model**: Qwen3-4B-Instruct-2507 loaded via Hugging Face
- **Training Data**: Thai Wikipedia dataset v3 from PyThaiNLP
- **Pipeline**: Preprocessing → Training → Inference
- **Language Focus**: Thai language text processing with transformer-based approach
- **Output Format**: High-quality tokenized text suitable for downstream NLP tasks

## Technical Constraints

- Python 3.10+ compatibility
- MLX framework for Apple Silicon optimization
- LoRA (Low-Rank Adaptation) for efficient fine-tuning
- Jupyter notebook implementation (main.ipynb)
- Hugging Face integration for model and dataset loading

## Success Criteria

- Accurate tokenization of Thai text
- Handle edge cases (mixed scripts, punctuation, numbers)
- Clear API for integration
- Comprehensive documentation
- Test coverage for reliability

## Project Scope

- **In Scope**: Thai text tokenization, basic preprocessing, API design
- **Future Considerations**: Multiple tokenization strategies, performance optimization, integration with popular NLP frameworks

## Current Status

- ✅ Complete MLX LoRA Thai tokenizer implementation
- ✅ Qwen3-4B-Instruct-2507 + LoRA + Thai Wikipedia dataset
- ✅ Full pipeline implemented in main.ipynb
- ✅ Ready for production use and further development

## Key Challenges

- Thai script complexity (no spaces between words)
- Handling mixed Thai-English text
- Balancing accuracy vs performance
- Supporting different tokenization granularities
