# Azure AI Cloud Developer Associate: Computer Vision & Document Intelligence

## Topics checklist
### Computer vision
- [ ] Image classification and object detection concepts
- [ ] OCR / text extraction concepts for images
- [ ] Bounding boxes, confidence scores, and interpreting vision outputs
- [ ] Quality considerations (thresholding, domain shift, failure modes)
- [ ] Integrating vision outputs into an app (data models for labels, boxes, and OCR text)

### Document Intelligence / form processing
- [ ] Document extraction fundamentals (forms, receipts, IDs, tables/layout)
- [ ] Handling layouts (structured vs unstructured fields)
- [ ] Model selection vs custom training (when you need a custom model)
- [ ] Preprocessing and postprocessing patterns (validation, normalization)
- [ ] Evaluating accuracy (field-level and document-level)

## Exam-style practice (with answers)
### Question 1
You need to identify where products appear in an image (and return bounding boxes). What class of vision problem is this?

**Answer (model):**
It’s an **object detection / detection** problem (not plain classification), because you need locations (bounding boxes) plus labels.

### Question 2
Your documents vary by customer and the prebuilt extraction isn’t accurate enough. When should you switch to custom training (vs continuing with only preprocessing)?

**Answer (model):**
When the gaps are primarily **domain-specific layout/field variations** (not just noise/rotation/lighting), and you need consistently higher extraction quality, you generally move toward **custom model training** and/or a tailored extraction approach. Preprocessing is useful, but it won’t replace the ability to learn the domain-specific structure.

