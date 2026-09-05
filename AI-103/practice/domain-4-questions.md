# Domain 4 practice — Implement text analysis solutions

**Exam:** AI-103 · Developing AI Apps and Agents on Azure  
**Weight:** 10–15% · Skills measured as of **April 16, 2026**  
**Coverage:** Study guide [`../study-guides/04-text-analysis.md`](../study-guides/04-text-analysis.md)

**How to use:** Cover the **Correct / Why** blocks and answer closed-book first. Unofficial study aids — not Microsoft exam dumps.

---

### Q1. Structured extraction
A workflow must return entities and topics as validated JSON for a CRM. Which approach aligns with the exam skills?

- A. Extract entities/topics/summaries into structured JSON using generative prompting and/or Foundry Tools
- B. Return only unstructured free text with no schema
- C. Generate videos of the CRM screens
- D. Disable all parsing and store screenshots

**Correct:** A  
**Why correct:** Entity/topic extraction with structured JSON is an explicit skill.  
**Why distractors fail:** B/C/D don’t produce reliable structured outputs.  
**Mapped skill:** 4.1 Extract entities, topics, summaries, structured JSON  

---

### Q2. Sentiment and safety
Before publishing customer comments to a public dashboard, you must detect negative tone and sensitive content. What should you configure?

- A. Detection of sentiment/tone, safety issues, and sensitive content
- B. Only image inpainting
- C. Only vector index rebuilds with no text analysis
- D. Only increasing TTS volume

**Correct:** A  
**Why correct:** Sentiment, tone, safety, and sensitive content detection are in scope.  
**Why distractors fail:** B/C/D don’t analyze comment risk.  
**Mapped skill:** 4.1 Detect sentiment, tone, safety, sensitive content  

---

### Q3. Translation chooser
You need high-volume, predictable translation of product UI strings into 20 languages. Which option is the best default?

- A. Azure Translator in Foundry Tools
- B. A video-generation model
- C. Manual retyping by the model with no Translator and no evaluation
- D. Disabling language codes in the request

**Correct:** A  
**Why correct:** Azure Translator is built for scalable, consistent MT workloads.  
**Why distractors fail:** B wrong modality; C/D unreliable.  
**Mapped skill:** 4.1 Translate text using Azure Translator or LLM flows  

---

### Q4. LLM translation nuance
Marketing wants translations that also rewrite tone to match brand voice. What may be appropriate?

- A. LLM-powered translation/localization flows with style instructions
- B. Only binary file copy across regions
- C. Only OCR without language output
- D. Only deleting source strings

**Correct:** A  
**Why correct:** LLM flows help when translation + stylistic rewrite is required.  
**Why distractors fail:** B/C/D don’t produce localized brand copy.  
**Mapped skill:** 4.1 LLM-powered translation flows  

---

### Q5. Domain customization
Legal needs summaries that highlight compliance obligations and extract clause types unique to your contracts. What should you do?

- A. Customize language model outputs for domain tasks (compliance summarization / domain extraction)
- B. Use a generic captioning model for photos of the office
- C. Ignore domain vocabulary
- D. Replace contracts with random text

**Correct:** A  
**Why correct:** Domain customization for compliance summarization/extraction is listed.  
**Why distractors fail:** B/C/D miss the legal domain requirement.  
**Mapped skill:** 4.1 Customize outputs for domain tasks  

---

### Q6. Speech for agents (multi-select)
**Select 2.** Which capabilities enable voice-based agent interactions?

- A. Speech-to-text for user utterances
- B. Text-to-speech for agent replies
- C. Only PDF layout analysis with no audio
- D. Only watermark detection on images

**Correct:** A, B  
**Why correct:** STT and TTS are the speech modalities for agentic interactions.  
**Why distractors fail:** C/D are other domains.  
**Mapped skill:** 4.2 Speech-to-text and text-to-speech for agents  

---

### Q7. Custom speech
Call-center audio includes rare medical device names and strong regional accents; generic STT accuracy is poor. What should you implement?

- A. Custom speech models tailored to the domain/accents
- B. Lower the image generation resolution
- C. Remove punctuation from CRM IDs only
- D. Disable STT and require Morse code

**Correct:** A  
**Why correct:** Custom speech improves recognition for specialized vocabulary and accents.  
**Why distractors fail:** B/C/D don’t fix speech accuracy.  
**Mapped skill:** 4.2 Integrate speech including custom speech models  

---

### Q8. Multimodal audio reasoning
An agent must reason over a voicemail’s content (not only a rough transcript). Which capability is in scope?

- A. Enable multimodal reasoning from audio inputs
- B. Only translate filenames
- C. Only generate unrelated product images
- D. Only rebuild a search index of empty documents

**Correct:** A  
**Why correct:** Multimodal reasoning from audio is an explicit speech skill.  
**Why distractors fail:** B/C/D ignore audio understanding.  
**Mapped skill:** 4.2 Multimodal reasoning from audio inputs  

---

### Q9. Speech translation
A global support line must take speech in one language and respond in another. What should you build?

- A. Translate speech using language models and/or Foundry Tools speech/translation capabilities
- B. Only store audio blobs with no transcription
- C. Only apply image brand watermarks
- D. Only increase embedding dimensions

**Correct:** A  
**Why correct:** Speech translation via models/Foundry Tools matches the outline.  
**Why distractors fail:** B/C/D don’t deliver cross-language voice support.  
**Mapped skill:** 4.2 Translate speech into other languages  

---

### Q10. Tool vs agent scope
Requirement: “Detect PII in support tickets and return a JSON flag.” Smallest sufficient solution?

- A. Text analysis with Foundry Tools / prompting for sensitive content + structured output
- B. A multi-agent swarm with video generation and no PII detection
- C. Unrestricted autonomous database deletion agents
- D. Only hybrid search with no text classifiers

**Correct:** A  
**Why correct:** Targeted text analysis/safety detection with structured output is enough.  
**Why distractors fail:** B/C overbuild or wrong risk; D doesn’t detect PII.  
**Mapped skill:** 4.1 Sensitive content detection + structured outputs  

---

## Answer key

| Q | Answer |
|---|--------|
| 1 | A |
| 2 | A |
| 3 | A |
| 4 | A |
| 5 | A |
| 6 | A, B |
| 7 | A |
| 8 | A |
| 9 | A |
| 10 | A |

**Readiness:** Aim ≥8/10. Review [`../study-guides/04-text-analysis.md`](../study-guides/04-text-analysis.md) for misses.
