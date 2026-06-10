# Can Offline AI Pass JEE and NEET?

Testing small, locally-run language models on real competitive exam questions. No internet, no cloud, just raw model intelligence.

---

## Background

This started as a simple question: how well do small, free, offline AI models actually perform on JEE Main and NEET UG questions? Not GPT-4, not Gemini. Models that run entirely on a laptop, with no API calls and no internet access during inference.

The motivation is practical. Millions of JEE and NEET aspirants study across India, many without reliable internet access. Cloud-based AI tutors are effectively out of reach for them. If a small model running on a mid-range laptop could meaningfully help with exam prep, that changes things.

Three open-source models were tested using [LM Studio](https://lmstudio.ai), a free application that runs quantized AI models locally. The questions came from real NEET UG papers (2019, 2022, 2025) and JEE Main 2025 papers (Jan 22, Jan 24, Apr 06 shifts). 36 questions per model, 108 total inferences, five subjects.

---

## Models

| Model | Made By | Parameters | VRAM |
|---|---|---|---|
| Gemma 4 12B QAT | Google DeepMind | 12B | 7.31 GB |
| Qwen 3.5 9B | Alibaba Cloud | 9B | 7.21 GB |
| Ministral 3 3B | Mistral AI | 3B | 3.23 GB |

All three run in GGUF quantized format, meaning they fit on consumer hardware. No GPU workstation required.

---

## Results

### Overall (36 questions each)

| Model | Correct | Accuracy |
|---|---|---|
| Gemma 4 12B QAT | 17/36 | 47% |
| Ministral 3 3B | 14/36 | 39% |
| Qwen 3.5 9B | 12/36 | 33% |

### NEET vs JEE

| Exam | Gemma | Qwen | Ministral |
|---|---|---|---|
| NEET (18 questions) | 10/18 | 8/18 | 11/18 |
| JEE (18 questions) | 6/18 | 5/18 | 4/18 |

Every model performed noticeably better on NEET than JEE. The gap is consistent across all three.

### Subject Breakdown

| Subject | Gemma | Qwen | Ministral |
|---|---|---|---|
| Biology | 4/4 | 3/4 | 4/4 |
| Physics | 7/14 | 4/14 | 7/14 |
| Chemistry | 5/12 | 3/12 | 1/12 |
| Maths (JEE only) | 1/6 | 2/6 | 2/6 |

---

## What the Data Shows

**Biology was surprisingly strong.** All three models handled NEET Biology questions well. Fact-based, concept-heavy questions with clear text answers are well-suited to language models. This is actually useful for exam prep since Biology has a large share of marks in NEET.

**JEE Maths was the hardest section by far.** Multi-step calculations involving area under curves, coordinate geometry, and limits failed across all models. This is the clearest hard ceiling in the dataset.

**Chemistry calculations were a consistent weak point.** Questions involving Ksp from pH, Carius method percentages, and ionic equilibrium tripped up all three models. Conceptual chemistry MCQs fared better.

**Diagram-based questions caused errors across the board.** The models are working from text descriptions of circuits and diagrams, not the actual images. That is a structural disadvantage that better prompting alone cannot fix.

**Questions all three got wrong simultaneously:**
- NEET 2019: Q62 Chemistry (Ksp of Ca(OH)2 from pH)
- NEET 2025: Q46 Physics, Q48 Chemistry
- JEE Apr 06: Q18 Maths, Q2 Maths, Q6 Physics, Q7 Chemistry
- JEE Jan 22: Q3 Physics, Q17 Physics, Q24 Chemistry
- JEE Jan 24: Q3 Chemistry

These represent a consistent floor where small models simply do not have enough reasoning capacity for the required steps.

**One important caveat on Gemma:** It was tested with a 2000-token context window, far below the 8192 tokens given to Qwen and Ministral, and a fraction of its actual maximum (262,144 tokens). This likely hurt its performance on multi-part questions. Its 47% accuracy despite this is notable.

---

## Takeaway

These models are not ready to replace a textbook or a teacher for serious JEE/NEET prep. They are too unreliable on calculations and too blind to diagrams to be trusted on the question types that decide ranks.

That said, the Biology and conceptual MCQ results suggest a real, if narrow, use case. For concept revision, quick factual checks, and understanding definitions, a small offline model running on a basic laptop is genuinely functional. That is not nothing, especially for students without reliable internet.

The more interesting question is what happens when these models are given better context: longer windows, retrieval from textbooks, or fine-tuning on Indian curriculum data. This study is a baseline.

---

## Setup

- Tool: LM Studio (lmstudio.ai), free and no-code
- Hardware: Consumer GPU, 3 to 8 GB VRAM depending on model
- Question sources: Official NEET papers, eSaral.com for JEE 2025 papers

Full question-by-question results are in the report included in this repo.

*Research by Diya Arora, June 2026*
