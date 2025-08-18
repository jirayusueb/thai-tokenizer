# Folder Structure: Thai Tokenizer

## Current Structure

```
thai-tokenizer/
├── main.ipynb                    # Development and experimentation notebook
├── pyproject.toml               # Project configuration and dependencies
├── README.md                    # Project documentation (empty)
├── .gitignore                   # Git ignore patterns
├── .python-version              # Python version specification
└── memory-bank/                 # Project memory and documentation
    ├── projectbrief.md          # Foundation project requirements
    ├── product-context.md       # Product vision and user experience
    ├── active-context.md        # Current work focus and decisions
    ├── system-patterns.md       # Architecture and design patterns
    ├── tech-context.md          # Technology stack and constraints
    ├── progress.md              # Current status and milestones
    └── folder-structure.md      # This file
```

## Planned Structure (Post-Implementation)

```
thai-tokenizer/
├── src/
│   └── thai_tokenizer/
│       ├── __init__.py          # Package initialization
│       ├── core.py              # Main tokenizer classes
│       ├── algorithms/
│       │   ├── __init__.py
│       │   ├── rule_based.py    # Rule-based tokenization
│       │   ├── dictionary.py    # Dictionary-based tokenization
│       │   └── ml_based.py      # Machine learning tokenization
│       ├── preprocessing/
│       │   ├── __init__.py
│       │   ├── normalizer.py    # Text normalization
│       │   └── cleaner.py       # Text cleaning utilities
│       ├── utils/
│       │   ├── __init__.py
│       │   ├── text_utils.py    # Text processing utilities
│       │   └── io_utils.py      # Input/output utilities
│       └── data/
│           ├── dictionaries/    # Word dictionaries
│           └── models/          # Pre-trained models
├── tests/
│   ├── __init__.py
│   ├── test_core.py             # Core functionality tests
│   ├── test_algorithms/
│   │   ├── test_rule_based.py
│   │   ├── test_dictionary.py
│   │   └── test_ml_based.py
│   ├── test_preprocessing/
│   ├── test_utils/
│   └── fixtures/
│       └── sample_texts.py      # Test data
├── docs/
│   ├── api/                     # API documentation
│   ├── user-guide/              # User documentation
│   ├── examples/                # Usage examples
│   └── development/             # Development documentation
├── benchmarks/
│   ├── accuracy/                # Accuracy evaluation
│   ├── performance/             # Speed benchmarks
│   └── datasets/                # Evaluation datasets
├── examples/
│   ├── basic_usage.py           # Simple usage examples
│   ├── advanced_features.py     # Advanced usage examples
│   └── integration_examples/    # Framework integration examples
├── scripts/
│   ├── setup_dev.py             # Development setup
│   ├── run_benchmarks.py        # Benchmark execution
│   └── build_package.py         # Package building
├── main.ipynb                   # Development notebook
├── pyproject.toml               # Project configuration
├── README.md                    # Project documentation
├── CHANGELOG.md                 # Version history
├── CONTRIBUTING.md              # Contribution guidelines
├── LICENSE                      # Project license
├── .gitignore                   # Git ignore patterns
├── .python-version              # Python version
└── memory-bank/                 # Project memory (current structure)
```

## Directory Purposes

### Source Code (`src/thai_tokenizer/`)

- **Core Module**: Main tokenizer implementation
- **Algorithms**: Different tokenization strategies
- **Preprocessing**: Text cleaning and normalization
- **Utils**: Helper functions and utilities
- **Data**: Dictionaries, models, and language resources

### Testing (`tests/`)

- **Unit Tests**: Individual component testing
- **Integration Tests**: Full workflow testing
- **Fixtures**: Test data and sample texts
- **Test Organization**: Mirror source structure

### Documentation (`docs/`)

- **API Documentation**: Auto-generated from code
- **User Guide**: Tutorials and examples
- **Development**: Contributing and architecture docs

### Benchmarking (`benchmarks/`)

- **Accuracy**: Evaluation against gold standards
- **Performance**: Speed and memory benchmarks
- **Datasets**: Standard evaluation datasets

### Examples (`examples/`)

- **Basic Usage**: Simple tokenization examples
- **Advanced Features**: Complex use cases
- **Integrations**: Framework-specific examples

### Utilities (`scripts/`)

- **Development**: Setup and maintenance scripts
- **Build Process**: Package building and distribution
- **Automation**: CI/CD and testing scripts

## File Naming Conventions

- **Python Files**: snake_case naming
- **Classes**: PascalCase naming
- **Functions/Methods**: snake_case naming
- **Constants**: UPPER_SNAKE_CASE
- **Test Files**: `test_` prefix
- **Documentation**: kebab-case for markdown files

## Organization Principles

- **Modular Design**: Clear separation of concerns
- **Testable Structure**: Easy to unit test components
- **Discoverable**: Intuitive navigation and imports
- **Extensible**: Easy to add new algorithms and features
- **Standard Layout**: Follow Python packaging conventions
