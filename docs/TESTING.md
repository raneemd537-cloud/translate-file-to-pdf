# Testing Guide

## 1. Purpose

This document describes how to test the Translate File to PDF skill.

The goal is to verify full and faithful translation (not summarization), content completeness, preservation of tables and technical details, Arabic RTL formatting, structure preservation, and PDF quality.

**Important:** A test must only be marked as PASS after it has actually been performed. Do not mark tests as passed based on instructions alone.

## 2. Core Requirements Under Test

The improved skill must satisfy:

- Complete translation of all readable content (no silent omission or summarization).
- Preservation of original order of sections, pages, and slides.
- Exact preservation of tables (rows, columns, headers, values, relationships).
- No merging of separate columns or entries.
- Exact preservation of code blocks and technical names.
- Correct handling of Arabic RTL and mixed Arabic-English text.
- Mandatory completeness verification before delivery.
- Honest reporting of unreadable or unprocessed content.

## 3. Regression Test Cases (Based on Real Failures)

These cases come from a real test of an English lecture PDF on data preprocessing (missing values) that was translated into Arabic. The original contained 14 presentation slides. The previous version produced omissions and structural errors. These tests exist to prevent the same mistakes from recurring.

### Regression Test R1: Full translation without summarization

**Context:** Original slide explained multiple imputation alternatives in detail, including:
- Creating an `age_missing` indicator column
- Using `KNNImputer`
- Using `IterativeImputer`
- Using `ffill`, `bfill`, and `interpolate` for time-series data

**Previous failure:** The Arabic output reduced these to a general summary and omitted practical details.

**Expected result:**
- All listed techniques and explanations are present in the translation.
- No detailed technical content is replaced by a short general statement.
- The translation is complete, not summarized.

**Status:** Not tested (requires the original lecture PDF and a full run of the skill).

### Regression Test R2: No merging of separate dataset columns

**Context:** Original document contained separate columns:
- `Sex`
- `Age`
- `SibSp`

**Previous failure:** The translated version combined them into one row and described their type as `mixed`.

**Expected result:**
- The three columns remain separate.
- Headers and values stay associated correctly.
- No artificial "mixed" grouping is introduced.

**Status:** Not tested (requires the original lecture PDF and a full run of the skill).

### Regression Test R3: Preservation of technical names and code

**Context:** Original contained exact technical identifiers and code-related terms such as:
- `KNNImputer`
- `IterativeImputer`
- `ffill`
- `bfill`
- `interpolate`
- `age_missing`

**Previous failure:** Some code lines and explanations were compressed or rearranged, reducing clarity.

**Expected result:**
- All listed technical names appear unchanged.
- Code blocks retain their original form and meaning.
- Surrounding explanations are translated without altering the code or identifiers.

**Status:** Not tested (requires the original lecture PDF and a full run of the skill).

### Regression Test R4: Slide / page content coverage

**Context:** Original document had 14 slides. Output had 4 portrait pages.

**Previous concern:** Content loss due to page reduction or reorganization.

**Expected result:**
- All content from every original slide is present.
- Slide titles and logical order are preserved or clearly mapped.
- Combining slides onto fewer pages is allowed only if no information is lost and sections remain distinguishable.

**Status:** Not tested (requires the original lecture PDF and a full run of the skill).

## 4. Standard Test Cases

### Test 1: TXT File Translation

**Input:** A simple TXT document (see `examples/sample_input.txt`).

**Steps:**
1. Upload the file.
2. Request translation into a target language (e.g., Arabic).
3. Request a full translation and PDF.

**Expected Result:**
- All text is translated.
- Original meaning is preserved.
- No paragraphs are missing or repeated.
- Output is a readable PDF.

**Status:** Not tested.

### Test 2: DOCX File Translation

**Input:** A DOCX document containing headings, paragraphs, lists, and at least one table.

**Expected Result:**
- Content is extracted in the correct order.
- Headings and lists remain organized.
- Tables keep their structure.
- Important information is preserved.

**Status:** Not tested.

### Test 3: Text-Based PDF Translation

**Input:** A PDF containing selectable text (multi-page preferred).

**Expected Result:**
- Text is extracted correctly.
- Page or section order is preserved.
- No important sections are missing.
- Tables and lists (if present) are preserved.

**Status:** Not tested.

### Test 4: Scanned PDF and OCR

**Input:** A scanned PDF or image-based document.

**Expected Result:**
- OCR is used only when available.
- Extracted text is reviewed for recognition errors.
- Unclear or unreadable content is reported to the user.
- No invented text is presented as accurate.

**Status:** Not tested.

### Test 5: Arabic Translation and RTL Formatting

**Input:** An English document translated into Arabic.

**Expected Result:**
- Arabic letters are connected correctly.
- Text direction is right-to-left (not merely right-aligned).
- Numbers and English technical terms remain readable and correctly ordered.
- No overlapping, reversed, or disconnected text appears.
- Mixed Arabic-English paragraphs are logical.

**Status:** Not tested.

### Test 6: Long Document / Multi-Slide Translation

**Input:** A document or presentation containing multiple pages or slides.

**Expected Result:**
- All sections or slides are processed.
- No paragraphs or slides are skipped or repeated.
- Original content order is preserved.
- Completeness verification is performed.

**Status:** Not tested.

### Test 7: Table Preservation

**Input:** A document containing one or more tables with multiple columns and rows.

**Expected Result:**
- All rows and columns are present.
- Headers match the correct values.
- Separate columns are not merged.
- Empty cells with structural meaning are preserved when possible.

**Status:** Not tested.

### Test 8: Code and Technical Content Preservation

**Input:** A technical document containing code blocks, function names, and numerical examples.

**Expected Result:**
- Code is preserved exactly.
- Technical identifiers are not translated.
- Numerical values and formulas remain correct.
- Explanatory text is translated without altering the technical content.

**Status:** Not tested.

### Test 9: PDF Output Quality

**Input:** A successfully translated document.

**Expected Result:**
- A PDF file is generated successfully.
- The file can be opened.
- Text is readable.
- Formatting is consistent.
- Tables and code blocks are fully visible.
- No sections are cut off.

**Status:** Not tested.

### Test 10: Completeness Verification Behavior

**Input:** Any document processed by the skill.

**Expected Result:**
- The skill performs (or explicitly reports the inability to perform) the completeness checks listed in SKILL.md Section 11.
- Missing or unreadable content is reported rather than silently omitted.
- The skill does not claim completeness without evidence.

**Status:** Not tested.

### Test 11: Unsupported Tools or File Types

**Input:** A file that cannot be processed with the available tools, or a request that requires unavailable OCR/PDF capabilities.

**Expected Result:**
- The limitation is explained clearly.
- The assistant does not claim that the file was fully processed.
- An alternative is suggested when possible (e.g., translated text in another format).

**Status:** Not tested.

### Test 12: Explicit Summary Request

**Input:** A document with an explicit user request for a summary rather than full translation.

**Expected Result:**
- The skill produces a summary as requested.
- It does not silently switch to full translation or vice versa.

**Status:** Not tested.

## 5. Test Results Summary

Record results only after actual execution.

| Test | Status | Notes |
|------|--------|-------|
| R1 Full translation (no summarization) | Not tested | Requires original Titanic/missing-values lecture PDF |
| R2 Separate columns (Sex, Age, SibSp) | Not tested | Requires original lecture PDF |
| R3 Technical names (KNNImputer, etc.) | Not tested | Requires original lecture PDF |
| R4 Slide/page coverage | Not tested | Requires original lecture PDF |
| 1 TXT Translation | Not tested | |
| 2 DOCX Translation | Not tested | |
| 3 Text-Based PDF | Not tested | |
| 4 Scanned PDF / OCR | Not tested | |
| 5 Arabic RTL | Not tested | |
| 6 Long / Multi-Slide | Not tested | |
| 7 Table Preservation | Not tested | |
| 8 Code & Technical | Not tested | |
| 9 PDF Output Quality | Not tested | |
| 10 Completeness Verification | Not tested | |
| 11 Unsupported Cases | Not tested | |
| 12 Explicit Summary | Not tested | |

## 6. Notes on Real-World Testing

The original and previously generated Arabic PDF files mentioned in the improvement request (`Ch02 part(1)- Data Preprocessing - Missing Values.pdf` and the corresponding Arabic output) were not present in the working environment at the time of this update. Therefore, the regression tests (R1–R4) are documented but marked "Not tested".

When those files (or equivalent technical lecture slides) become available, they should be used as the primary regression suite. The skill instructions have been strengthened specifically to prevent the previously observed failures:

- Omission / summarization of imputation techniques
- Merging of separate columns (`Sex`, `Age`, `SibSp`)
- Loss or compression of technical identifiers and code
- Incomplete slide coverage

## 7. Final Evaluation Criteria

The skill can be considered improved and ready for use when:

1. The instructions in `SKILL.md` clearly mandate full translation and completeness verification.
2. Regression cases for the known failures are documented.
3. At least the core tests (full translation, table preservation, technical name preservation, Arabic RTL, and completeness checks) have been executed on real documents and the results recorded honestly.

Do not report successful results without actual testing.
