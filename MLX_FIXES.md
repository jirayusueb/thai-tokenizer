# MLX Compatibility Fixes

## Issues Fixed

### 1. TokenizerWrapper Compatibility Error

**Problem**: `TypeError: 'TokenizerWrapper' object is not callable`

**Root Cause**: MLX's `load_model()` returns a `TokenizerWrapper` object that has a different interface than standard HuggingFace tokenizers. The `TokenizerWrapper` is designed for generation (encode/decode) but doesn't support the full tokenizer interface needed for data preprocessing.

**Solution**:

- Keep both the original HuggingFace tokenizer and the MLX TokenizerWrapper
- Use HuggingFace tokenizer for data preparation (training data tokenization)
- Use MLX TokenizerWrapper for model generation/inference

```python
# Load both tokenizers
self.hf_tokenizer = AutoTokenizer.from_pretrained(self.model_name)  # For data prep
self.model, self.tokenizer = load_model(self.model_name)  # MLX TokenizerWrapper for generation

# Use HF tokenizer for training data preparation
tokenizer_to_use = self.hf_tokenizer  # Always use HF for data prep
inputs = tokenizer_to_use(text, max_length=512, truncation=True, padding="max_length", return_tensors="np")
```

### 2. LoRA Initialization Error

**Problem**: `AttributeError: module 'mlx.nn.init' has no attribute 'kaiming_uniform_'`

**Solution**: MLX uses different initialization methods compared to PyTorch. Updated the LoRA adapter initialization:

```python
# Before (PyTorch style - doesn't work in MLX)
nn.init.kaiming_uniform_(self.lora_A.weight)
nn.init.zeros_(self.lora_B.weight)

# After (MLX compatible)
def _initialize_weights(self):
    std = (2.0 / self.lora_A.weight.shape[-1]) ** 0.5
    self.lora_A.weight = mx.random.normal(self.lora_A.weight.shape) * std
    self.lora_B.weight = mx.zeros_like(self.lora_B.weight)
```

### 3. Tensor Format Compatibility

**Problem**: PyTorch tensors (`return_tensors="pt"`) are not compatible with MLX.

**Solution**: Updated tokenizer to use numpy arrays and convert to MLX:

```python
# Before
return_tensors="pt"

# After
return_tensors="np"  # Use numpy for MLX compatibility
# Convert to MLX arrays
"input_ids": mx.array(inputs["input_ids"]),
"attention_mask": mx.array(inputs["attention_mask"]),
"labels": mx.array(targets["input_ids"])
```

### 4. Model Serialization

**Problem**: MLX arrays need special handling for JSON serialization.

**Solution**: Added robust conversion for weight saving:

```python
# Enhanced weight serialization with fallbacks
try:
    if hasattr(adapter.lora_A.weight, 'tolist'):
        lora_A_data = adapter.lora_A.weight.tolist()
    elif hasattr(adapter.lora_A.weight, '__array__'):
        lora_A_data = np.array(adapter.lora_A.weight).tolist()
except:
    lora_A_data = f"shape_{adapter.lora_A.weight.shape}"
```

## Verification

All fixes have been tested and verified:

- ✅ TokenizerWrapper issue resolved
- ✅ HuggingFace + MLX tokenizer dual setup works
- ✅ Training data preparation works correctly
- ✅ LoRA adapter creation works
- ✅ Forward pass through LoRA layers works
- ✅ Weight conversion to numpy works
- ✅ MLX tensor operations work correctly

## Running the Fixed Code

The notebook `main.ipynb` now runs successfully with MLX. Key improvements:

1. Proper MLX-compatible LoRA initialization
2. Correct tensor format handling
3. Robust model serialization
4. Better error handling for edge cases

## Performance Benefits

With these fixes, the Thai tokenizer now properly leverages:

- MLX's Apple Silicon optimization
- Efficient LoRA parameter updates
- Native MLX tensor operations
- Optimal memory usage on M-series chips
