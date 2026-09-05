# Section 3 — Implement computer vision solutions (10–15%)

> **Exam:** AI-103 · Developing AI Apps and Agents on Azure  
> **Mapped skills:** 3.1–3.3 · [Official study guide](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/ai-103)  
> **Mock test:** [`../practice/domain-3-questions.md`](../practice/domain-3-questions.md)

## In one sentence

You generate and edit images/videos, understand visual content with multimodal models and Content Understanding, and apply responsible AI controls to multimodal media.

## Why it matters on the exam

Smaller weight but dense. Distinguish **generation** vs **understanding**, captioning vs visual Q&A, and classic vision filters vs **indirect prompt injection** via text-in-image.

## Mental model

```text
                 ┌── Generation / editing ──► images & videos
  Visual task ───┤
                 └── Understanding ──► captions, VQA, objects, video insights
                              │
                              ▼
                     Content Understanding / multimodal models
                              │
                              ▼
                     RAI: filters, injection defense, brand/policy rules
```

## Topics checklist

### 3.1 Image- and video-generation

- [ ] Text-to-image and reference-media conditioning
- [ ] Text-to-video and reference-media video generation
- [ ] Image editing: inpainting, mask-based edits, prompt-driven edits
- [ ] Edit generated videos
- [ ] Apply platform generation/editing controls (size, seed, strength, safety, etc.)

### 3.2 Multimodal understanding

- [ ] Analyze visual context with multimodal models
- [ ] Concise vs detailed captions (single/multi image)
- [ ] Visual question-answering grounded in evidence
- [ ] Alt-text and extended descriptions for accessibility
- [ ] Azure **Content Understanding** for visual characteristics
- [ ] Video segment analysis workflows
- [ ] Single-task vs **pro-mode** Content Understanding pipelines
- [ ] Object / component / region identification

### 3.3 Responsible AI for multimodal content

- [ ] Classify unsafe/disallowed visual content
- [ ] Detect/mitigate **indirect prompt injection** from embedded text in images
- [ ] Enforce visual policies: watermarks, prohibited symbols, brand rules, inappropriate content

---

## Key concepts

### Generation vs understanding

| Goal | Approach |
|------|----------|
| Create new media | Image/video generation models + controls |
| Modify existing media | Inpainting, masks, prompt edits, video edit workflows |
| Describe or answer about media | Multimodal understanding / Content Understanding |
| Accessibility | Alt-text (short) + extended descriptions |

### Image editing patterns

- **Inpainting:** replace a masked region while keeping the rest.
- **Mask-based edits:** explicit region control for precision.
- **Prompt-driven modifications:** natural-language edit instructions over the whole or part of an image.
- Controls typically include guidance strength, seed reproducibility, resolution, and safety settings.

### Content Understanding pipelines

| Mode | Typical use |
|------|-------------|
| Single-task | Focused extraction (e.g., one schema or one visual task) |
| Pro-mode | Richer / multi-step understanding pipelines for complex docs or media |

Use Content Understanding to extract structured visual characteristics and produce grounded representations for agents/RAG — not only free-form captions.

### Video workflows

- Segment video → analyze frames/segments → summarize or answer questions.
- Combine generation (create clips) with understanding (index/search what happened).

### Multimodal RAI

```text
  Image/video in
       │
       ├── Content safety classification (NSFW, violence, etc.)
       ├── OCR / text extraction → scan for injected instructions
       └── Policy checks (brand, watermark, prohibited symbols)
```

⚠️ **Exam trap:** Treating a malicious instruction *printed in an image* as ordinary user text — that’s **indirect prompt injection**; mitigate by detecting embedded text and not blindly following it as system instructions.

## Common mistakes

- Using generation models for object detection / field extraction tasks.
- Confusing short alt-text with detailed captioning or VQA.
- Skipping safety filters on generated or user-uploaded media.
- Ignoring brand/watermark requirements in enterprise image pipelines.

## Study focus order

1. Generation vs editing controls (3.1)  
2. Understanding tasks: caption, VQA, objects, Content Understanding (3.2)  
3. Multimodal RAI and prompt injection (3.3)

## Check your understanding

A retail app must generate product hero images, allow background replacement, and block competitor logos. Which capabilities map to generation, editing, and RAI?
