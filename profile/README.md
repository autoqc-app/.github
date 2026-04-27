# AutoQC

**Automated video quality control — AI-powered subtitle QA, brand detection, and 13 signal checks. Zero manual frame scrubbing.**

AutoQC is a web-based SaaS platform that automatically detects visual, audio, and encoding issues in video files before delivery or broadcast. Built for content creators, post-production teams, broadcasters, and MCN agencies.

🌐 **[autoqc.app](https://www.autoqc.app)** · [Features](https://www.autoqc.app/features) · [Pricing](https://www.autoqc.app/pricing) · [What's New](https://www.autoqc.app/resource/whats-new)

---

## What AutoQC detects

### AI Visual Detection
- **PlanD OCR** — GPU-accelerated OCR + LLM semantic analysis pipeline, **OCR Recall 96.9%**, 109 languages
  - Typo & spelling error detection, safe zone check, subtitle extraction
- **Logo & Brand Detection** — Grounding DINO v1 zero-shot detector, 4-stage aggregation pipeline, no brand sample upload required
  - Logo copyright risk (amber markers) + branded product risk (orange markers) with dynamic bounding box tracking

### Video Quality (8 checks)
- Black frames, flash frames, bad edits — single-pass detection (VideoArtifact v4.0, **F1 Score 103.7%**, Precision 100%)
- Freeze frames — 3-stage cascade with motion-vector entropy analysis (**100% pass rate, zero false positives**)
- Blur, brightness, borders, aspect ratio

### Audio Quality (5 checks)
- Audio loudness compliance, audio clipping (true-peak), background noise, silence, speech clarity
- All 5 audio checks share a single Silero VAD timeline — **Audio Module 75% faster** vs. independent per-check analysis

### Platform Compliance
- YouTube · TikTok · Instagram · Broadcast TV · Custom presets

---

## Detection accuracy

| Module | Precision | Recall | F1 Score | Test set |
|--------|-----------|--------|----------|----------|
| VideoArtifact (black frames, flash, bad edit) | **100%** | 107.7% | **103.7%** | BE_01–05 (5 scene types) |
| FreezeFrame | 100% | 100% | **100%** | Case 1–7 (7 scene types) |
| PlanD OCR (subtitle extraction) | — | **96.9%** | — | 15-video batch test |

> VideoArtifact Recall 107.7% means the detector found real artifacts not covered by the test set annotations. Precision 100% = zero false positives.

---

## Architecture highlights

- **Hybrid approach**: FFmpeg/DSP for signal-level checks + AI deep learning for semantic checks
- **Single-pass efficiency**: FFmpeg calls reduced **from 7 to 2 (−70%)** via UnifiedVideoWrapper + UnifiedAudioWrapper
- **Queue system**: Bull Queue + Redis, async processing, 30-min timeout protection
- **AI inference**: Silero VAD (ONNX Runtime) + Grounding DINO v1 + GPU-accelerated OCR pipeline (serverless inference)
- **Stack**: Next.js 16 · React 19 · Node.js 22 · Prisma · PostgreSQL · Docker

---

## Links

- Product: [autoqc.app](https://www.autoqc.app)
- Product Hunt: [producthunt.com/products/autoqc](https://www.producthunt.com/products/autoqc/launches/autoqc)
- G2 Reviews: [g2.com/products/autoqc](https://www.g2.com/products/autoqc/reviews)
- Release notes: [autoqc.app/resource/whats-new](https://www.autoqc.app/resource/whats-new)
