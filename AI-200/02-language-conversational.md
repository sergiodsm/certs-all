# Azure AI Cloud Developer Associate: Natural Language & Conversational AI

## Topics checklist
### Natural language (NLP)
- [ ] Language detection and text preprocessing basics
- [ ] Text translation (translation pipelines, throughput considerations)
- [ ] Text analytics capabilities (sentiment, key phrases, entities / NER)
- [ ] Document/PII-related NLP considerations (redaction/classification patterns)
- [ ] Integrating NLP calls into an application (schemas, retries, and safe logging of inputs/outputs)

### Conversational AI
- [ ] Intent and entity modeling (concepts and why they matter)
- [ ] Designing dialog flows (context, turn-taking, error handling)
- [ ] Integrating a conversational layer with downstream AI services
- [ ] Testing conversational flows (edge cases, fallback behavior)

## Exam-style practice (with answers)
### Question 1
A user asks: “Translate this text to Spanish, and also tell me the sentiment.” Which capability goes with which task?

**Answer (model):**
Use **translation** for the language conversion step, and **sentiment analysis** as the NLP step that labels tone/polarity. In a typical design, the translation output is either analyzed directly (if you analyze the translated text) or you analyze sentiment on the original text—either way you should keep the intent clear and consistent.

### Question 2
Your bot sometimes fails when the user input is ambiguous. What’s the best dialog-flow behavior?

**Answer (model):**
Implement an explicit **fallback/repair path**: when confidence is low, ask a clarifying question (or route to a safe default), preserve conversation context, and avoid committing side effects until the intent/entity is reliably determined.

