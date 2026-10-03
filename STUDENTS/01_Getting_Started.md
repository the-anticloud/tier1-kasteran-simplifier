# KASTERAN_SIMPLIFIER — Student Getting Started

## What You'll Build
A text simplification pipeline that rewrites complex documents into plain language, running entirely locally with Ollama.

## Prerequisites
- Python 3.10+
- Ollama with llama3:8b installed

## Install
```bash
ollama pull llama3:8b
pip install kasteran-simplifier
```

## First Working Example
```python
from kasteran import Simplifier

simplifier = Simplifier(model="ollama/llama3:8b", target_grade=6)

complex_text = """The implementation leverages asynchronous I/O multiplexing
to facilitate concurrent request processing while maintaining deterministic
throughput guarantees under variable load conditions."""

result = simplifier.simplify(complex_text)
print("Original:")
print(complex_text)
print("\nSimplified:")
print(result.simplified_text)
print(f"Readability: grade {result.original_grade:.1f} -> {result.simplified_grade:.1f}")
```

## Batch Simplification
```python
from kasteran import Simplifier

simplifier = Simplifier(model="ollama/llama3:8b", target_grade=8)

texts = open("technical_doc.txt").readlines()
for i, text in enumerate(texts[:5]):
    result = simplifier.simplify(text)
    print(f"Paragraph {i}: {result.simplified_text}\n")
```

## On Kaggle (loiskleinner account, T4 GPU)
```python
!pip install kasteran-simplifier
!curl -fsSL https://ollama.ai/install.sh | sh
!ollama serve &
import time; time.sleep(5)
!ollama pull llama3:8b
```

## What's Next
- Try different `target_grade` values (4, 8, 12) and compare outputs
- Compute SARI scores by comparing to human-simplified reference texts
- Integrate with KAMELOT_SEARCH to simplify indexed documents on the fly
