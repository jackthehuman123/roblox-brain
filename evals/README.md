# Evals (HUMAN-OWNED, agents read-only)

- **Scoring is done by the harness, never by an agent's self-report.** Run notes paste the harness output verbatim.
- The harness scripts live in each game repo, not here. TODO: humans build them.
- `tasks/train/`: tasks used during training batches. Agents may see them.
- `tasks/holdout/`: tasks only used to compare a candidate against the current card. Never train on them and never quote them in lessons.
- Agents must never edit anything here. If a test or baseline looks wrong, write a note in `inbox/`.
- Baselines: [[evals/baselines]] (server-scripter), [[evals/assets/baselines]] (asset-builder). Task template: [[evals/tasks/_task-template]].
