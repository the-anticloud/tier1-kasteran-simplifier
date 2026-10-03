# Deploy Guide — KASTERAN_SIMPLIFIER
## Prerequisites
- Python 3.11+, radon 6.0+, pylint 3.1+, ast (stdlib), PAX 27B for AI refactoring

## Environment
- CPU-only for static analysis. GPU for PAX-assisted refactoring. 8GB RAM.

## Install
```bash
pip install anticloud-kasteran radon pylint
```

## Run as pre-commit hook
```bash
python -m kasteran_simplifier install-hook --max-cc 15
```

## Air-Gap
Static analysis (radon/pylint/ast) has no network requirements. PAX weights needed for AI refactoring.

## AIOSS Integration
```bash
aioss init --module KASTERAN_SIMPLIFIER --output ./simplifier.aioss
```

## Verification
```bash
python -m kasteran_simplifier check --max-cc 15 --path ./TIER_4_INFERENCE_AGENTS/K_NANOVLLM
```
