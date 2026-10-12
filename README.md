# NLP Project

# NLP Project To-Do: Translate→Simplify vs Simplify→Translate

**Deadline:** Friday 6 November 2026, 23:59 (ACL format, max 8 pages excl. references/appendix)

## Week 1 (12–18 Oct): Setup and data

- [ ] Reply to the teacher
  - [ ] Clarify: no back-translation to Dutch; both sides of the Amsterdam pairs are translated to English
  - [ ] Say we'll add SimPA (Scarton et al., 2018) as a clean English test set
  - [ ] Confirm we're going ahead
- [ ] Set up repo and environment
  - [ ] Pin model versions (opus-mt-nl-en, bart-base-wikilarge-simplification, ul2-base-dutch-simplification)
  - [ ] Pin library versions (`transformers`, `sentencepiece`, `easse`)
  - [ ] Fix random seeds
- [ ] Load the Amsterdam dataset
  - [ ] Compute stats: documents, sentence pairs, words, avg sentence length (complex vs simple)
- [ ] Load the SimPA dataset
  - [ ] Compute the same stats for a side-by-side table
- [ ] Define the "complex sentence" sampling rule (length or readability threshold + seed) and write it down
- [ ] Draw the 60-sentence human-eval sample
- [ ] Check ethics requirements
  - [ ] Check whether the UT faculty (BMS) requires ethics review for the human evaluation
  - [ ] Write the consent text
  - [ ] Make responses anonymous (participant ID only, no names)

## Week 2 (19–25 Oct): Experiments

### Simplifier evaluation (controls)
- [ ] Dutch UL2 model on Amsterdam → SARI against Dutch references
- [ ] English BART model on SimPA → SARI against the 3 references (main English test)
- [ ] English BART model on MT-translated Amsterdam → SARI (secondary test; note MT noise in references)
- [ ] (Optional) English BART model on ASSET or TurkCorpus (in-domain comparison)

### Baselines
- [ ] Translation only (opus-mt-nl-en, no simplification)
- [ ] Identity (copy the source)

### Pipelines
- [ ] Run Pipeline 1 (translate → simplify) on the full Amsterdam input
- [ ] Run Pipeline 2 (simplify → translate) on the full Amsterdam input
- [ ] Translate the Dutch simple references to English (pseudo-references)

### Automatic pipeline metrics
- [ ] SARI (both pipelines + translation-only baseline)
- [ ] FKGL (readability)
- [ ] BERTScore against translation-only output (meaning preservation)
- [ ] Regex check: do numbers, dates and names survive?

### Evaluation website
- [ ] Show Dutch source + outputs A/B in random order
- [ ] Two 1–5 ratings per output (ease of understanding, key info retained)
- [ ] Preference choice
- [ ] Log the A/B → pipeline mapping server-side only
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
