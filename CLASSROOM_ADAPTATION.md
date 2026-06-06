# 🎓 Classroom Demo Adaptation Plan

> **Source:** Forked from [akucharsk/CompressionVis](https://github.com/akucharsk/CompressionVis)  
> **Purpose:** Adapt this compression visualization tool into a classroom-ready teaching demo for media format transitions, codec comparison, and video compression concepts.

---

## 📊 Project Architecture Snapshot

| Layer | Language | Files | Notes |
|-------|----------|-------|-------|
| **Frontend** | JavaScript (React) | ~91 | Components, pages, contexts, hooks, utils |
| **Frontend** | CSS | ~30 | Page & component styles |
| **Frontend** | HTML | 1 | `index.html` entry point |
| **Backend** | Python (Django) | ~29 core | Views, models, serializers, tasks, extractors |
| **Backend** | Python (migrations) | ~20 | Auto-generated Django migrations |
| **Infra** | Docker/YAML | ~3 | `docker-compose.yml`, Dockerfiles |

**Front-end → Back-end file ratio:**  
- **Including migrations:** 122 frontend / 49 backend ≈ **2.5 : 1**  
- **Excluding migrations:** 122 frontend / 29 backend ≈ **4.2 : 1**  

This is heavily front-end weighted — ideal since most pedagogical changes will be UI-layer additions (annotations, walkthroughs, tooltips).

---

## 📋 Required Changes

### 1. 🔴 Step-by-Step Walkthrough Mode (P0)
- Add a guided tour / wizard mode that walks students through the app one concept at a time:
  - **Step 1:** Pick a video
  - **Step 2:** Choose a codec & encoding parameters
  - **Step 3:** Inspect frame types (I / P / B)
  - **Step 4:** Compare quality metrics side-by-side
  - **Step 5:** Analyze macroblocks & motion vectors
- Implement "Next / Back" navigation within each visualization page.
- Persist walkthrough progress in `localStorage` so students can resume later.

### 2. 🔴 Explanatory Annotations & Tooltips (P0)
- Add contextual info panels / popovers on every major UI element:
  - **Frame Distribution view:** Explain I-frames, P-frames, B-frames and their roles.
  - **Comparison view:** Explain PSNR, SSIM, VMAF in plain language.
  - **Charts view:** Explain bitrate ladders, CRF vs. quality trade-offs.
  - **Macroblock view:** Explain motion vectors and macroblock partitioning.
- Include "Why does this matter?" callout boxes connecting visualizations to real-world implications (streaming bandwidth, storage costs, perceptual quality).

### 3. 🟠 Glossary / Reference Panel (P1)
- Add a collapsible sidebar or modal glossary defining all technical terms: codec, container, bitrate, CRF, GOP, PSNR, SSIM, VMAF, macroblock, motion vector, chroma subsampling, etc.
- Link glossary terms inline so clicking "PSNR" in any view opens its glossary entry.

### 4. 🟠 Pre-Loaded Demo Content — Remove 16 GB Dependency (P1)
- Bundle or auto-fetch a small set of lightweight sample videos (short clips, ≤30 s, low resolution) so the demo works without the 16 GB Google Drive download.
- Provide a "quick-start" Docker profile that pre-populates the database with sample compression results, eliminating the need for students to wait for encoding tasks.

### 5. 🟡 Simplified Landing / Menu Page (P2)
- Redesign the Menu page for a classroom context:
  - Replace the current card layout with a **lesson-oriented flow**: "Lesson 1: Understanding Frame Types", "Lesson 2: Codec Quality Comparison", "Lesson 3: Compression Artifacts", etc.
  - Add estimated time per lesson.
  - Show completion checkmarks for finished lessons.

### 6. 🟡 Quiz Enhancements for Formative Assessment (P2)
- Add explanatory feedback after each quiz answer — explain *why* the correct answer is right, not just right/wrong.
- Allow instructors to create custom quizzes through a simpler UI (current admin requires Django superuser).
- Add a "review mode" where students can revisit questions and see explanations without retaking.

### 7. 🟢 Visual Codec Transition Demonstrator — New Feature (P3)
- Build a new page/module showing a side-by-side animated transition of the same video encoded with different codecs (H.264 vs. VP9 vs. AV1) at the same bitrate.
- Overlay real-time metric graphs (PSNR/SSIM per frame) that animate as the video plays.
- Add a slider to scrub between codec outputs for direct visual comparison.

### 8. 🟢 Instructor Dashboard (P3)
- Add a lightweight instructor view showing aggregated student quiz results and walkthrough progress.
- Provide a "Reset Demo" button to clear all student progress for a new class.

### 9. 🟢 Accessibility & UX Polish (P3)
- Ensure keyboard-navigable walkthrough (Tab / Enter to advance steps).
- Add high-contrast mode for projector-friendly classroom display.
- Include a "Print Handout" mode that exports key visualizations and explanations as a PDF-friendly layout.

### 10. 🟢 Documentation for Educators (P3)
- Add a `TEACHING_GUIDE.md` with:
  - Suggested lesson plans (30 min, 60 min, 90 min formats).
  - Learning objectives mapped to each visualization page.
  - Discussion prompts and follow-up exercises.
  - Simplified setup instructions for non-technical instructors.

---

## 🏗️ Implementation Priority Summary

| Priority | Item | Effort | Front-end? | Back-end? |
|----------|------|--------|------------|-----------|
| 🔴 P0 | Walkthrough Mode | Medium | ✅ | Minor |
| 🔴 P0 | Explanatory Annotations | Medium | ✅ | — |
| 🟠 P1 | Pre-Loaded Demo Content | Medium | Minor | ✅ |
| 🟠 P1 | Glossary Panel | Low | ✅ | — |
| 🟡 P2 | Simplified Landing Page | Low | ✅ | — |
| 🟡 P2 | Quiz Feedback | Medium | ✅ | Minor |
| 🟢 P3 | Codec Transition Demonstrator | High | ✅ | ✅ |
| 🟢 P3 | Instructor Dashboard | High | ✅ | ✅ |
| 🟢 P3 | Accessibility | Medium | ✅ | — |
| 🟢 P3 | Teaching Guide | Low | — | — |

---

## 🚀 Quick Start for Classroom Use

1. **Enable Issues** on this fork (Settings → Features → Issues) to track progress on each item above.
2. **Create a branch** `classroom-demo` from `master` for all adaptation work.
3. **Start with P0 items** — walkthrough mode and annotations will have the biggest impact on student learning.
4. **Test with sample content** before class — the 16 GB download can be avoided by using the quick-start profile once implemented.

---

*This document serves as the master plan for classroom adaptation. Convert each section into individual GitHub Issues once the Issues feature is enabled on this fork.*
