# L5 Narrow / L2 General Classification — KASTERAN_SIMPLIFIER
**Platform:** Anticloud | **PAX:** 27B | **IP:** USPTO pending 2026, Anticloud FZ LLE

## L5 Narrow
KASTERAN_SIMPLIFIER specializes in cyclomatic complexity reduction and dead-code elimination for
Python/Rust AI inference pipelines. Not JS, not frontend, not infra YAML. Scoped to the patterns
found in Anticloud's 123 projects: async inference loops, AIOSS chain calls, PAX harness wiring.

## L2 General
Any developer runs KASTERAN_SIMPLIFIER on any tier project without configuration. It understands
Anticloud-specific patterns across all tiers.

## PAX Integration
PAX 27B handles AI-assisted refactoring. Static analysis (radon/pylint) identifies targets;
PAX generates refactored versions; AST equivalence validation confirms correctness.

## AIOSS Audit Relevance
Each simplification event is chained: before-AST hash, after-AST hash, complexity delta.
Complete audit trail of every AI-assisted refactor in the codebase.

## Regulatory
NIST SSDF PW.1.1 (secure design), ISO 25010 (software quality — maintainability sub-characteristic)
