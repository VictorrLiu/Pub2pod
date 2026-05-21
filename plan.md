# Pub2pod Planning (No Build Yet)

## Scope acknowledgement
- This phase is planning-only.
- No pipeline implementation is started in this document.
- Requested model preference captured: **Claude Opus 4.7**.

## What is still unclear / ambiguous
1. **Provider stack**: exact LLM provider/API + fallback policy are unspecified.
2. **TTS stack**: provider, voice inventory, and licensing constraints are unspecified.
3. **Rights/access policy**: behavior for paywalled or unavailable full text is unspecified.
4. **Grounding/citation rules**: required citation format and claim traceability in outputs are unspecified.
5. **Novelty method**: retrieval scope and criteria for “better/different from prior work” are unspecified.
6. **Length targets**: desired summary size and podcast runtime are unspecified.
7. **Narration style controls**: speaker persona and pacing controls are unspecified.
8. **Windows runtime constraints**: packaging and local dependency expectations are unspecified.
9. **Caching strategy**: cache keying, invalidation TTL, and offline reuse policy are unspecified.
10. **Failure semantics**: retry limits, partial-output policy, and exit codes are unspecified.
11. **Config surface**: precedence between config file vs CLI flags vs env vars is unspecified.
12. **Data/privacy posture**: whether paper text can be sent to external APIs is unspecified.

## Clarifying questions (small batch 1)
Please answer this first batch before we draft batch 2.

1. **LLM provider/model**: Should we lock to Claude Opus 4.7 only, or allow provider/model config with Opus 4.7 as default?
2. **TTS provider**: Which provider should be primary (and do you want an offline fallback)?
3. **Paywalled papers**: If full text is inaccessible, should output be:
   - metadata+abstract-only summary/podcast,
   - hard fail with actionable message, or
   - user-prompted override?
4. **Output length target**: What is your default target for:
   - summary note length,
   - single-narrator runtime,
   - two-host runtime?
5. **Config strategy**: Prefer primarily a `config.toml/yaml` file with optional CLI overrides, or CLI-first with minimal config file?

## Technical risks / decisions to resolve early
- **Hallucination risk** in methods/novelty claims without citation-backed grounding.
- **Licensing/compliance risk** for TTS voice usage and redistribution of generated audio.
- **Access fragility** across DOI/PubMed/PDF sources and publisher rate limits.
- **Cost risk** from multi-stage LLM + TTS calls without strict token/audio budgeting.
- **Reproducibility risk** if model/provider output drift is not bounded by deterministic prompts/settings.
- **Latency risk** for long papers if no chunking + staged summarization strategy.
- **Quality risk** if script generation is not constrained by speaking-rate/pacing targets.

## Draft execution plan (to finalize after Q&A)
- [ ] Confirm provider, model, and TTS decisions
- [ ] Finalize error-handling + paywall policy
- [ ] Finalize config schema and CLI precedence
- [ ] Finalize retrieval/grounding and novelty-analysis criteria
- [ ] Freeze architecture and module contracts
- [ ] Define acceptance criteria and test plan
- [ ] Begin implementation only after plan sign-off
