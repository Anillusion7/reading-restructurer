---
name: reading-restructurer
description: Reconstruct dense long-form reading into a clearer, better-segmented, lower-friction version while preserving the author’s argument chain, definitions, evidence, and qualifications.
---

# reading-restructurer

## 1) Purpose and product boundary
This skill restructures dense reading materials (books, chapters, essays, reflective prose, long-form argument) into a clearer and less fatiguing version **without distorting meaning**.

It is **not** a plain summary tool. It must preserve the reasoning chain, not only conclusions.

## 2) Trigger boundaries

### SHOULD trigger
Use this skill when the user asks to:
- Rewrite a chapter/excerpt into a more readable but faithful version.
- Reduce verbosity, indirect exposition, repetitive buildup, or structural messiness.
- Reach the main point faster without losing logic.
- Add internal sub-structure/headings to dense passages.
- Do argument-preserving compression rather than short summarization.

### SHOULD NOT trigger
Do **not** use this skill when the user only wants:
- A short summary.
- Translation only (no restructuring).
- Literary appreciation/commentary only.
- Analysis without reconstruction.
- Stylistic imitation or parody.
- Exact source-text reproduction.

Also do not trigger if source text is unavailable and cannot be reliably/lawfully obtained for the requested rewrite.

## 3) Input expectations
Support four input situations:

- **Case A: User provides passage text (preferred).**
  - Treat user text as source of truth.
  - Process directly; do not replace with a web version.

- **Case B: User provides title + author + chapter/section.**
  - Resolve work identity and locate reliable, lawful source.
  - If uncertain, ask for excerpt instead of guessing.

- **Case C: User provides vague or partial memory.**
  - Attempt careful identity resolution.
  - If ambiguity remains, request clearer identifiers.

- **Case D: User requests full-book processing.**
  - Do not process full book in a single pass by default.
  - Switch to chapter/excerpt chunking and recomposition workflow.

## 4) Source handling policy
1. Prefer user-provided text first.
2. If user text exists, do not overwrite with external versions.
3. If only metadata is provided, use reliable/lawful sources only.
4. If copyright/lawful access is unclear, do not produce substitute full-text rewrite from uncertain sourcing.
5. In restricted cases, offer fallback options:
   - structure guide,
   - excerpt-based restructuring workflow,
   - reading plan requiring user-supplied excerpts.
6. Distinguish source types explicitly:
   - original-language edition,
   - translated edition,
   - abridged edition,
   - commentary/study guide/summary (not source text).
7. If source reliability is uncertain, state uncertainty explicitly.

## 5) Source discovery and language resolution policy
When user supplies only title/author/chapter metadata, resolve in order:
1. Canonical work identity.
2. Author identity.
3. Original language (if known).
4. Whether user likely needs original or translated text.

Rules:
- If user specifies language, search that language first.
- If user does not specify language, check title variants/translations before deciding.
- Prefer original-language source for argument-preserving reconstruction when feasible.
- If original language is impractical and user is clearly reading Chinese, a reliable Chinese translation may be used, but this must be declared.
- Before rewriting, explicitly state source language and edition type.
- If identity remains uncertain, ask for exact edition/chapter/excerpt.

## 6) Output language policy (default)
Unless user explicitly requests otherwise:
- Explanations and analysis scaffolding are in **Simplified Chinese**:
  - 章节导读
  - 结构拆解
  - 关键论证链
  - 压缩说明
  - warnings / source reliability notes
- Reconstructed main text defaults to the **source text’s original language**.
- If user explicitly requests Chinese reading version, produce reconstructed main text in Simplified Chinese.
- If task involves both restructuring + translation, warn that interpretation risk is higher and preserve key terms carefully.

## 7) Terminology policy
- Preserve precise names and technical/philosophical/historical/school-specific/book-specific terms in original language when precision matters.
- On first mention, optionally add concise Simplified Chinese gloss if useful.
- Do not replace precision terms with loose colloquial paraphrases.

## 8) Reading modes
- **fidelity_mode**: high fidelity to original sequencing/rhetorical feel; compress only clearly redundant material.
- **standard_mode (default)**: balanced readability and faithfulness.
- **efficiency_mode**: stronger compression of setup/repetition; reaches main point faster while preserving core reasoning.

## 9) Compression levels
- **light**: mild cleanup; mostly preserve structure; remove obvious redundancy.
- **medium (default)**: tighten transitions, reduce repeated setup, improve segmentation, retain full reasoning chain.
- **high**: substantial compression of rhetorical padding and repeated restatement while preserving an honest argument chain; must not collapse into shallow summary.

## 10) Genre sensitivity rule
For argumentative/explanatory/philosophical/historical/analytical/essayistic writing:
- Prioritize clarity, structure, and information density.
- Compress aggressively when safe.

For literary/narrative writing:
- Be conservative.
- Preserve scene function, pacing, atmosphere, characterization, and tonal buildup when they carry meaning.
- Do not treat all atmosphere as redundant setup.

When compression may damage intended effect, warn user and default to conservative mode.

## 11) Required execution workflow
Follow this sequence exactly:

1. **Classify source situation**: user text / reliable external / uncertain / unavailable.
2. **Resolve work identity + source language** when needed.
3. **Check lawful and practical feasibility** for requested operation.
4. **Set operating parameters**:
   - reading mode,
   - compression level,
   - source edition type,
   - output language mode.
5. **Read passage intent**: identify topic and authorial goal.
6. **Segment by rhetorical function**.
7. **Tag content roles**:
   - essential,
   - compressible,
   - repeated,
   - definitional,
   - evidentiary,
   - transitional,
   - cautionary/qualifying.
8. **Reconstruct**:
   - improve structure,
   - reduce friction,
   - compress redundancy,
   - keep argument integrity,
   - add internal subheadings.
9. **Produce output contract exactly**.
10. **If blocked/unsafe**: execute fallback path explicitly; do not pretend completion.

## 12) Output contract (must match exactly)
Return output in this exact structure and order:

1. **章节导读**
   - 3–5句简体中文。
   - 覆盖：主题、核心命题/统摄观点、论证展开路径。

2. **结构拆解**
   - 对每个内部小节给出：
     - 小节标题
     - 功能标签
     - 一句话概括

3. **重构后的正文**
   - 要求：更清晰、更结构化、带内部标题、比原文更紧凑、保留关键论证链。
   - 语言默认源文本原语言；如用户明确要求中文则输出简体中文重构版。

4. **关键论证链**
   - 简体中文列出：
     - 核心命题
     - 主要支撑理由
     - 关键例子或证据
     - 重要限定、反驳或保留意见

5. **压缩说明**
   - 简体中文说明：
     - 压缩了什么
     - 为什么可以安全压缩
     - 哪些部分必须完整保留及原因

## 13) Failure and fallback behavior
When failure risk appears, respond explicitly:

1. **source not found**
   - State source cannot be reliably identified.
   - Request title/author/chapter/excerpt details.

2. **source found but not reliable enough**
   - Explain uncertainty and risk.
   - Do not proceed as if certain.

3. **likely copyrighted + no lawful full-text access**
   - Do not output substitute full-text reconstruction.
   - Offer excerpt-based restructuring workflow.

4. **text too long**
   - Process by chunks.
   - Preserve inter-chunk logic with cross-chunk map.
   - Recompose into chapter-level final output.

5. **literary text with atmosphere-sensitive effect**
   - Warn user compression may damage effect.
   - Default to conservative mode (fidelity_mode + light or medium compression).

## 14) Non-negotiable fidelity rules
- Never distort author meaning.
- Never turn tentative claims into absolute conclusions.
- Never remove necessary definitions, transitions, rebuttals, or qualifications.
- Never collapse into shallow summary.
- Never add unsupported interpretations or fabricated evidence.
- Never claim certainty when source identity is uncertain.
- Never overwrite user-provided text with another version.
- Never obscure whether source is original-language, translation, abridgment, or commentary-derived.

## 15) Operational response template (internal checklist)
Before finalizing output, verify:
- [ ] Source status declared.
- [ ] Language + edition type declared.
- [ ] Mode + compression level declared (explicit or inferred default).
- [ ] Rhetorical segmentation completed.
- [ ] Output has all 5 required sections in exact order.
- [ ] Compression explanation distinguishes removed vs preserved material.
- [ ] No unsupported inference introduced.
