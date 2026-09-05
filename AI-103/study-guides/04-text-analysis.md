# Section 4 — Implement text analysis solutions (10–15%)

> **Exam:** AI-103 · Developing AI Apps and Agents on Azure  
> **Mapped skills:** 4.1–4.2 · [Official study guide](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/ai-103)  
> **Mock test:** [`../practice/domain-4-questions.md`](../practice/domain-4-questions.md)

## In one sentence

You analyze and transform text with language models and Foundry Tools, and you add speech (STT/TTS/translation) as a modality for agent interactions.

## Why it matters on the exam

Expect chooser questions: **Foundry Tools** (Translator, Language, Speech) vs **LLM prompting** for extraction/summarization; also when to use custom speech models.

## Mental model

```text
  Text path:  input text → extract / sentiment / translate / summarize → structured output
  Speech path: audio ⇄ text (STT/TTS) → same language pipeline → optional translation
  Agent path:  speech as modality + custom speech + multimodal reasoning from audio
```

## Topics checklist

### 4.1 Language model text analysis

- [ ] Extract entities, topics, summaries, structured **JSON** (prompting + Foundry Tools)
- [ ] Detect sentiment, tone, safety issues, sensitive content
- [ ] Translate with **Azure Translator** or LLM-powered flows
- [ ] Customize outputs for domain tasks (compliance summarization, domain extraction)

### 4.2 Speech solutions

- [ ] Speech-to-text and text-to-speech for agents
- [ ] Speech as an agent modality; **custom speech** models
- [ ] Multimodal reasoning from audio inputs
- [ ] Speech translation via language models and Foundry Tools

---

## Key concepts

### Tools vs LLM prompting

| Task | Prefer Foundry Tools when… | Prefer LLM prompting when… |
|------|----------------------------|----------------------------|
| Translation | High volume, many languages, deterministic MT | Nuanced rewrite + translate, style control |
| Sentiment / PII / safety | Dedicated detectors, policy features | Tone + nuanced judgment in one pass |
| Entities / topics | Built-in NER / topic APIs fit the domain | Custom schema, nested JSON, rare domains |
| Summarization | Standard abstractive needs with control | Compliance framing, multi-doc synthesis |

### Structured outputs

- Ask for **JSON schema**-aligned responses for downstream systems.
- Validate schema before using fields in agents or workflows.
- Combine Tools (reliable detectors) with LLM (flexible structuring) when needed.

### Domain customization

- Compliance summarization: constrain length, cite clauses, flag risk language.
- Domain extraction: industry glossaries, few-shot examples, controlled vocabularies.
- Prefer grounded prompts over unconstrained free text when outputs feed systems of record.

### Speech in agentic systems

```text
  User speaks → STT (+ custom model if accents/domain terms)
             → agent reasoning (text + optional audio multimodal)
             → TTS reply (voice, locale)
             → optional speech translation
```

- **Custom speech** improves accuracy for jargon, accents, noisy environments.
- Agents treat speech as another input/output channel, not a separate product silo.
- Multimodal reasoning from audio can use transcript + audio features depending on model capabilities.

⚠️ **Exam trap:** Using a general STT model when the scenario stresses specialized vocabulary — answer is often **custom speech**.

## Common mistakes

- Using a full agent stack for “detect sentiment and return JSON.”
- Forgetting sensitive-content / PII detection before logging or storing text.
- Translating with an LLM when Azure Translator is the cheaper, clearer fit (or vice versa for creative localization).
- Ignoring locale/voice selection in TTS for multilingual agents.

## Study focus order

1. Extraction, sentiment/safety, translation choosers (4.1)  
2. Structured JSON and domain customization (4.1)  
3. STT/TTS, custom speech, speech translation (4.2)

## Check your understanding

A call-center agent must transcribe domain jargon, summarize for compliance, and reply in the caller’s language. Outline STT, analysis, and TTS/translation choices.
