# KASTERAN_SIMPLIFIER — Educator's Teaching Guide

## Course Fit: NLP, text simplification, accessibility engineering, LLM fine-tuning

## 3-Week Module: Text Simplification Systems for Accessible AI

### Week 1: What Is Text Simplification?
**Lecture Topics:**
- Lexical vs. syntactic simplification
- Readability metrics: Flesch-Kincaid, SMOG, ARI
- Why KASTERAN_SIMPLIFIER uses local models (privacy for legal/medical text)
- Training data for simplification: Simple English Wikipedia, Newsela

**Lab Exercise:**
```python
from kasteran import Simplifier
simplifier = Simplifier(model="ollama/llama3:8b", target_grade=6)
complex_text = """The mitigation of anthropogenic greenhouse gas emissions
requires multisectoral coordination across energy, transport, and industrial
sectors."""
result = simplifier.simplify(complex_text)
print(f"Original FK grade: {result.original_grade:.1f}")
print(f"Simplified FK grade: {result.simplified_grade:.1f}")
print(result.simplified_text)
```

### Week 2: Fine-Tuning for Domain-Specific Simplification
**Lecture Topics:**
- When zero-shot simplification fails (legal contracts, medical records)
- Instruction-tuning a LoRA adapter for simplification
- Evaluation: SARI score, BERTScore, human evaluation
- Preserving factual accuracy during simplification

**Lab Exercise:**
```python
from kasteran import SimplifierTrainer
from datasets import load_dataset
dataset = load_dataset("json", data_files="legal_simplification_pairs.jsonl")
trainer = SimplifierTrainer(
    base_model="meta-llama/Llama-3.2-3B",  # download locally
    lora_rank=16,
    target_grade=8
)
trainer.train(dataset["train"], epochs=3, output_dir="./kasteran_legal_adapter")
```

### Week 3: Integrating KASTERAN in the Anticloud System
**Lecture Topics:**
- KASTERAN as a preprocessing step in KAMELOT_SEARCH pipelines
- Simplification in MIIRAI_CHAT for accessibility modes
- AIOSS format for audit trails of simplification decisions
- Batch processing with PAX_SCHEDULER

**Lab Exercise:**
```python
from kasteran import Simplifier
from kamelot import SearchIndex
simplifier = Simplifier(model="ollama/llama3:8b")
index = SearchIndex(backend="local")
for doc in index.iter_documents():
    simplified = simplifier.simplify(doc.text)
    index.update(doc.id, metadata={"simplified": simplified.simplified_text})
```

## Exam Questions
1. What does the SARI score measure? Why is it preferred over BLEU for evaluating text simplification?
2. Explain why preserving factual accuracy is harder in simplification than in summarization. How would you detect factual drift in a simplification pipeline?
3. Describe a use case in the Anticloud ecosystem where KASTERAN_SIMPLIFIER integration with KAMELOT_SEARCH provides measurable value.
