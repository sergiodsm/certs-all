# Azure AI Cloud Developer Associate: Speech AI

## Topics checklist
- [ ] Speech-to-text (batch vs real-time concepts)
- [ ] Speaker/language handling concepts (when relevant to the solution)
- [ ] Text-to-speech (neural voices, SSML basics)
- [ ] Error handling and latency/throughput considerations
- [ ] Integrating speech features into an app (streaming handling, retries, UX timeouts)

## Exam-style practice (with answers)
### Question 1
You’re building a live call transcription feature. Which mode is typically the better fit?

**Answer (model):**
**Real-time** transcription (low-latency streaming) rather than batch transcription, because the user needs partial results as the audio is spoken.

### Question 2
You want to control pronunciation, emphasis, or speaking style in generated speech. What should you use?

**Answer (model):**
Use **SSML** (and the related speech synthesis options) to control prosody/pronunciation/emphasis so the voice renders the text the way you intend.

