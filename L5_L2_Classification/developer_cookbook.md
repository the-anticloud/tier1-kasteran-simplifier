# Developer Cookbook — KASTERAN_SIMPLIFIER
**Stack:** Python 3.11, radon, pylint, AST, PAX 27B

## Analyze project complexity
```python
from kasteran_simplifier import KasteranAnalyzer
analyzer = KasteranAnalyzer()
report = analyzer.analyze_directory("E:/fenta/Downloads/The Anticloud/TIER_4_INFERENCE_AGENTS/K_SGLANG")
print(f"Avg CC: {report.avg_cyclomatic_complexity:.1f}")
print(f"High CC functions: {len(report.high_complexity_functions)}")
```

## Auto-simplify
```python
simplified = analyzer.simplify(file_path="./engine.py",
                                pax_model="./pax-27b-q4.gguf", max_cc=10)
simplified.write_patched()
```

## Find dead code
```python
dead = analyzer.find_dead_code("./inference_pipeline.py")
for fn in dead.unused_functions:
    print(f"Unused: {fn.name} at line {fn.line}")
```

## CI check
```bash
python -m kasteran_simplifier check --max-cc 15 --fail-on-violation
```

## AIOSS append for refactor event
```python
before_hash = hashlib.sha3_256(open("engine.py","rb").read()).hexdigest()
simplified.write_patched()
after_hash = hashlib.sha3_256(open("engine.py","rb").read()).hexdigest()
record = json.dumps({"before": before_hash, "after": after_hash, "cc_delta": -4}).encode()
aioss_append("./simplifier.aioss", record, "KASTERAN_SIMPLIFIER")
```

## Performance
Run radon/pylint first; only invoke PAX for CC > 10. Batch: `analyzer.batch_simplify(files)`.
