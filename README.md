# MLX LoRA Thai Tokenizer

A high-performance Thai text tokenizer using MLX framework with LoRA fine-tuning of Qwen3-4B-Instruct-2507, trained on Thai Wikipedia dataset.

## 🚀 Features

- **MLX Optimized**: Apple Silicon optimization for fast inference
- **LoRA Fine-tuning**: Efficient parameter adaptation of Qwen3-4B-Instruct-2507
- **Complete Pipeline**: Preprocessing → Training → Inference
- **Thai Wikipedia Dataset**: Trained on 5,000+ Thai text samples
- **Multiple Granularities**: Word-level and character-level tokenization
- **Batch Processing**: Efficient handling of multiple texts
- **Fallback Mechanisms**: Robust handling of edge cases

## 📋 Requirements

- Python 3.10+
- Apple Silicon Mac (for MLX optimization)
- Dependencies: mlx, mlx-lm, transformers, torch, datasets, pandas, numpy

## 🛠 Installation

```bash
pip install mlx mlx-lm transformers torch datasets pandas numpy huggingface-hub
```

## 📖 Usage

The complete implementation is available in `main.ipynb` with the following pipeline:

### 1. Data Loading & Preprocessing

```python
# Load Thai Wikipedia dataset
data_processor = ThaiDataProcessor()
data_processor.load_dataset()
thai_texts = data_processor.prepare_tokenization_data(max_samples=5000)
```

### 2. Model Setup

```python
# Initialize Qwen3-4B-Instruct-2507 with LoRA adapters
qwen_lora = QwenLoRAModel("Qwen/Qwen3-4B-Instruct-2507")
qwen_lora.load_model()
qwen_lora.add_lora_adapters()
```

### 3. Training

```python
# Train with LoRA
trainer = LoRATrainer(qwen_lora)
training_data = qwen_lora.prepare_training_data(thai_texts[:100])
trainer.train(training_data, epochs=2, batch_size=4)
trainer.save_model("./thai_tokenizer_lora")
```

### 4. Inference

```python
# Use trained tokenizer
thai_tokenizer = ThaiTokenizer(qwen_lora, "./thai_tokenizer_lora")

# Tokenize Thai text
tokens = thai_tokenizer.tokenize("สวัสดีครับผมชื่อจิรายุ", method="word")
print(tokens)  # ['สวัสดี', 'ครับ', 'ผม', 'ชื่อ', 'จิรายุ']

# Batch processing
batch_results = thai_tokenizer.tokenize_batch(["ข้าวผัด", "ต้มยำกุ้ง"])
```

## 📊 Model Information

- **Base Model**: Qwen/Qwen3-4B-Instruct-2507
- **Framework**: MLX (Apple Silicon optimized)
- **Fine-tuning**: LoRA (Low-Rank Adaptation)
- **Dataset**: pythainlp/thai-wiki-dataset-v3
- **License**: cc-by-sa-3.0

## 📁 Project Structure

```
thai-tokenizer/
├── main.ipynb              # Complete pipeline implementation
├── pyproject.toml          # Project configuration
├── memory-bank/            # Project documentation
└── thai_tokenizer_lora/    # Trained model artifacts
```

## 🧪 Testing

The notebook includes comprehensive testing with:

- Thai text samples
- Mixed Thai-English content
- Performance evaluation
- Batch processing tests

## 🔬 Technical Details

### LoRA Configuration

- Rank: 16
- Alpha: 32.0
- Target modules: q_proj, k_proj, v_proj, o_proj

### Training Parameters

- Learning rate: 1e-4
- Batch size: 4
- Epochs: 2
- Max sequence length: 512

### Dataset Processing

- Source: Thai Wikipedia (197k articles)
- Processed samples: 5,000
- Text cleaning and normalization
- Maximum length truncation

## 🎯 Use Cases

- Thai NLP preprocessing
- Search engine tokenization
- Content analysis
- Language model training data preparation
- Academic research on Thai language processing

## 🤝 Contributing

This project uses a comprehensive memory bank system for documentation. See `memory-bank/` directory for detailed project context and architecture.

## 📄 License

This project is licensed under the same terms as the underlying dataset (cc-by-sa-3.0).

## 🙏 Acknowledgments

- PyThaiNLP for the Thai Wikipedia dataset
- Alibaba for the Qwen model family
- Apple for the MLX framework
- Hugging Face for model hosting and datasets

---

**Ready to tokenize Thai text with state-of-the-art performance! 🇹🇭✨**
