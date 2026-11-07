# Translate File to PDF

**Translate documents into another language and prepare a clean, readable PDF — with full content preservation by default.**

Translate File to PDF is an AI Skill that guides an assistant to translate document content while preserving its original meaning, structure, tables, code, and technical details as completely as possible.

It focuses on faithful translation (not summarization), document organization, Arabic RTL support, and readable PDF output.

## The Problem

Translating documents is not always easy.

Users may face problems such as:

- Losing the original document structure.
- Incorrect translations of technical terms.
- Missing paragraphs, bullet points, or technical details (silent summarization).
- Merged or distorted tables.
- Poor formatting in the final PDF.
- Incorrect Arabic text direction and letter shaping.

## Our Solution

Translate File to PDF provides a structured workflow that guides an AI assistant through:

1. Document extraction
2. Full and faithful translation
3. Structure and technical detail preservation
4. Mandatory completeness verification
5. PDF generation and quality checking

The default behavior is complete translation of the source document. Summarization occurs only when the user explicitly requests it.

## Key Features

### 1. Document Content Extraction
Extracts text and organizes the content while preserving its original order and structure when possible. Handles multi-page documents and presentation slides.

### 2. Full and Faithful Translation (Not Summarization)
Translates all readable content. Preserves meaning, names, numbers, dates, technical terms, code, formulas, and examples. Does not silently omit or shorten content.

### 3. Structure and Table Preservation
Keeps headings, paragraphs, lists, and tables organized. Preserves every table row, column, header, and value relationship. Does not merge separate columns or entries.

### 4. Technical Content Rules
Preserves code blocks, function names, variable names, library names, dataset column names, and mathematical formulas exactly. Translates only the surrounding explanatory text.

### 5. Arabic and RTL Support
Includes specific instructions for correct right-to-left direction, Arabic letter shaping, mixed Arabic-English text, and readable tables in RTL layouts.

### 6. Mandatory Completeness Verification
Before delivering the final PDF, the skill requires systematic checks for content completeness, table integrity, technical accuracy, translation fidelity, and PDF quality. Unreadable or missing sections must be reported.

### 7. PDF Generation
Guides the AI assistant to create a readable PDF using available tools, with consistent fonts, spacing, and layout adapted to the document type.

## Supported File Types

The skill is designed to work with:

- PDF files (text-based and, when OCR is available, scanned)
- DOCX files
- TXT files
- Markdown files
- Scanned documents and images when OCR is available

Actual support depends on the tools available in the execution environment.

## How It Works

1. The user uploads a document and requests a translation (target language + optional preferences).
2. The AI assistant identifies the file type and available tools.
3. The document content is extracted while preserving order and structure.
4. The content is translated fully into the requested language (default: no summarization).
5. Tables, code, and technical identifiers are checked for fidelity.
6. A completeness verification is performed.
7. A PDF is generated using available tools.
8. The result is checked and delivered, with any limitations reported honestly.

## Important Limitations

This repository contains AI skill instructions, not a standalone translation application.

- It does **not** include its own translation engine, OCR engine, or PDF-generation software.
- The skill depends on the capabilities and tools available in the AI environment where it is used.
- Arabic PDF output requires suitable fonts and proper text-shaping / bidirectional text support.
- Not every AI platform supports all file-processing operations. The skill instructs the assistant to check availability and report limitations rather than claim capabilities it does not have.

## Project Structure

```text
translate-file-to-pdf/
├── README.md
├── SKILL.md
├── docs/
│   └── TESTING.md
└── examples/
    └── sample_input.txt
```

## Testing

A testing guide is available in `docs/TESTING.md`.

It includes:

- Standard test cases for different document types
- Regression tests based on real failures observed with a data-preprocessing lecture (omitted technical details, merged columns, incomplete slide coverage)
- Explicit rules that tests may only be marked PASS after actual execution

## Project Goal

The goal of this project is to make document translation more reliable by enforcing complete, structure-preserving translation and honest verification, rather than treating translation as a summarization task.

---

**Project:** Translate File to PDF  
**Type:** AI Skill (instruction-based)  
**Platform:** Designed for an AI environment with the required document-processing tools
