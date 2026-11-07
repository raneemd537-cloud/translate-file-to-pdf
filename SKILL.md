---
name: translate-file-to-pdf
description: Translate any uploaded file (PDF, DOCX, TXT, images with text, etc.) into a clean well-structured PDF in the target language while preserving the original order of sections, headings, paragraphs and lists. Use when the user asks to translate a file and return PDF, or says translate this document to PDF, or invokes this skill for batch or repeated file translations.
---

# Translate File to PDF

## Overview

Handle end-to-end translation of user-provided files into a high-quality PDF. Extract content while respecting document structure, translate accurately, and regenerate a readable PDF that keeps the same logical order and hierarchy as the source.

## When to use

- User uploads or references a file and asks for translation + PDF output.
- User says "ترجم الملف" / "translate this file to PDF" / "translate and give me PDF".
- User wants a reusable workflow for translating multiple documents the same way.

## Instructions

1. **Identify source file and target language**
   - Accept PDF, DOCX, TXT, Markdown, or image files containing text.
   - If target language is not specified, default to Arabic (العربية). Ask only if truly ambiguous.
   - Confirm the source language if detection is uncertain.

2. **Extract content with structure**
   - For PDF: use `pdfplumber` (prefer) or `pdftotext -layout` to get text page by page. Capture headings, paragraphs, lists and tables as separate blocks in order.
   - For DOCX: use the `docx` skill to extract paragraphs and runs while noting style (Heading 1/2, Normal, List).
   - For plain text / Markdown: keep paragraph and heading markers.
   - For scanned / image PDFs: rasterize with `pdf2image` then OCR with `pytesseract` (Arabic + English support if needed).
   - Never flatten everything into one continuous string. Keep a list of ordered blocks: `{type: heading|paragraph|list_item|table_row, level: int, text: str}`.

3. **Translate**
   - Translate each block independently while preserving meaning, tone and technical terms.
   - Keep original numbers, dates, names, and code-like tokens untranslated unless the user asks otherwise.
   - Maintain the same block order and hierarchy after translation.
   - For tables: translate cell by cell and keep the grid structure.

4. **Generate the output PDF**
   - Use the `pdf` skill (`reportlab` + Platypus preferred for flowing documents).
   - Create a clean professional layout:
     - Title page or header with original filename + "ترجمة" / "Translation" + target language.
     - Headings use larger bold fonts and proper spacing.
     - Body text uses readable size (11–12 pt) with good leading.
     - Lists keep bullets/numbers.
     - Page numbers in footer.
   - Right-to-left support: when target is Arabic (or other RTL languages), set the PDF to RTL layout where possible (reportlab canvas direction or paragraph alignment).
   - Output file name: `translated_<original_basename>.pdf` or `<original>_ar.pdf`.

5. **Quality checks before delivery**
   - Verify every major section from the source appears in the same order in the PDF.
   - Spot-check a few paragraphs for translation accuracy.
   - If the source had many pages, produce a multi-page PDF; do not force everything onto one page.
   - Deliver the PDF via the render_file component and also give a short summary of what was translated (page count, language pair, any notes).

6. **Edge cases**
   - Very long documents: process page-by-page or section-by-section to stay within context limits; still produce one final PDF.
   - Mixed-language source: translate only the parts that are not already in the target language.
   - Forms or heavily designed PDFs: extract the readable text content and produce a clean textual PDF (do not attempt pixel-perfect visual recreation unless the user explicitly asks).
   - If extraction fails completely, tell the user clearly and offer alternatives (paste text, convert to DOCX first, etc.).

## Example triggers

- "ترجم هذا الملف وأعطني PDF"
- "Translate the attached PDF to Arabic and keep the structure"
- "Use the translate-file-to-pdf skill on this document"
- "I have several files to translate the same way"

## Notes for the agent

- Always prefer structured extraction over raw text dump.
- The final deliverable must be a real .pdf file the user can download.
- This skill is designed so the user can invoke it repeatedly without re-explaining the workflow.
