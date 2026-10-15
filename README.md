# NLP Project

# NLP Project To-Do: Translate→Simplify vs Simplify→Translate

**Deadline:** Friday 6 November 2026, 23:59 (ACL format, max 8 pages excl. references/appendix)

## Week 1 (12–18 Oct): Setup and data

- [x] Set up repo and environment
  - [x] Pin model versions (opus-mt-nl-en, bart-base-wikilarge-simplification, ul2-base-dutch-simplification)
  - [x] Pin library versions (`trhansformers`, `sentencepiece`, `easse`)
  - [x] Fix random seeds
- [x] Load the Amsterdam dataset
  - [x] Compute stats: documents, sentence pairs, words, avg sentence length (complex vs simple)
- [x] Load the SimPA dataset - 6e0c011d0166c1a8b571760c87bfd3779f3cce49
  - [x] Compute the same stats for a side-by-side table
- [x] Document the human-eval sentence selection rule (eligibility filters + sampling seed/cap) — complexity itself comes from the dataset's Complex/Simple pairing, not a threshold we define: eligible `Complex` sentences need ≥12 whitespace tokens, must end in `. ? !`, and have no leftover anonymization artifacts (stray punctuation gaps, `[` placeholders); rows where `Complex == Simple` or duplicate `Complex` text are dropped. From the eligible pool, 60 sentences are drawn with `SEED = 42`, capped at 3 per document for diversity (see `project.ipynb`).
- [x] Draw the 60-sentence human-eval sample

## Week 2 (19–25 Oct): Experiments

### Simplifier evaluation (controls)
- [x] Dutch UL2 model on Amsterdam → SARI against Dutch references (SARI = 40.10, n=1310)
- [x] English BART model on SimPA → SARI against the 3 references (main English test) (SARI = 34.84, 876/1100 rows had all 3 refs)
- [x] English BART model on MT-translated Amsterdam → SARI (secondary test; note MT noise in references) (SARI = 35.61, pseudo-refs)
- [ ] (Optional) English BART model on ASSET or TurkCorpus (in-domain comparison)

### Baselines
- [x] Translation only (opus-mt-nl-en, no simplification)
- [x] Identity (copy the source) — unprocessed Dutch, rock-bottom floor reference

### Pipelines
- [x] Run Pipeline 1 (translate → simplify) on the full Amsterdam input
- [x] Run Pipeline 2 (simplify → translate) on the full Amsterdam input
- [x] Translate the Dutch simple references to English (pseudo-references)

### Automatic pipeline metrics
- [x] SARI (both pipelines + translation-only baseline) — Translation-only 23.18, Pipeline 1 (translate→simplify) 35.61, Pipeline 2 (simplify→translate) 41.73
- [x] FKGL (readability) — Translation-only 9.63, Pipeline 1 8.77, Pipeline 2 8.43 (lower = simpler; vowel-group syllable heuristic, approximate)
- [x] BERTScore against translation-only output (meaning preservation) — Pipeline 1 F1 = 0.965, Pipeline 2 F1 = 0.922 (Pipeline 2 drifts further from the translation-only meaning, consistent with simplifying before translation compounding more change)
- [x] Regex check: do numbers, dates and names survive? — Pipeline 1: 86.2% numbers / 95.7% dates / 88.2% capitalized-words kept; Pipeline 2: 80.9% / 73.9% / 73.0% (capitalized-words is a cheap proxy for names, not real NER; see `project.ipynb`)

### Evaluation website
- [x] Show Dutch source + outputs A/B in random order — live at https://nlp-project.hnat-dev.com/, all 60 sentences loaded with real pipeline outputs
- [x] Two 1–5 ratings per output (ease of understanding, key info retained)
- [x] Preference choice — A / equally good / B, ties kept rather than forced
- [x] Log the A/B → pipeline mapping server-side only — verified: no pipeline names in client-side code/storage, mapping only in the judgments export
- [ ] Test the site on one person
- [ ] Start the paper outline in Overleaf (ACL template)

## Week 3 (26 Oct – 1 Nov): Human evaluation and analysis

- [ ] Send the website out early in the week (target: 20 participants × 10 sentences)
- [ ] Follow up with people who haven't finished
- [ ] Analyse human results
  - [ ] Mean ratings per pipeline + Wilcoxon signed-rank test
  - [ ] Preference win rate + sign/binomial test
  - [ ] Inter-annotator agreement (Krippendorff's alpha)
- [ ] Error analysis
  - [ ] Select ~10 sentences where pipelines differ most
  - [ ] Categorise failures (dropped date/amount, hallucination, MT error propagation, no simplification, …)
  - [ ] Pick 2–3 example sentences for the paper

## Week 4 (2–6 Nov): Write the paper

- [ ] Title + names and student numbers
- [ ] Introduction: letter problem, RQ, findings summary
- [ ] Related work: Vlantis et al. 2024, Xu et al. 2016, Scarton et al. 2018, + 1–2 on cascaded MT / Dutch simplification
- [ ] Data: Amsterdam + SimPA stats table, licences, how references were made, sampling rule
- [ ] Method: pipeline diagram, models, decoding settings, preprocessing
- [ ] Experimental setup: simplifier controls, baselines, metrics (and why), human eval design
- [ ] Results: SARI table, pipeline metrics table, human eval table with significance, example outputs
- [ ] Discussion & conclusion
  - [ ] Answer the RQ
  - [ ] Confound: different simplifiers, and how far the controls address it
  - [ ] MT noise in pseudo-references
  - [ ] Small, friend-based sample (not representative of real non-Dutch speakers)
  - [ ] Sentence-level vs whole letters
  - [ ] Ethics: harm from wrong simplification of tax/DUO letters; flag uncertainty, link to original
  - [ ] GenAI use statement
- [ ] Abstract (150–250 words, written last)
- [ ] References: check every one resolves

## Submission

- [ ] Check page count (≤ 8 pages)
- [ ] Export and submit the PDF
- [ ] Attach anonymised human-evaluation data
- [ ] (Optional) Attach code
