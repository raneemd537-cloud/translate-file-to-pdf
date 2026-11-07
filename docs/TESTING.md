# Testing Guide

## 1. Purpose

This document describes how to test the Translate File to PDF skill.

The goal is to check translation quality, content accuracy, document formatting, and PDF generation.

**Important:** A test must only be marked as PASS after it has actually been performed.

## 2. Test Cases

### Test 1: TXT File Translation

**Input:** A simple TXT document.

**Steps:**
1. Upload the file.
2. Select a target language.
3. Request a full translation.
4. Review the translated content.

**Expected Result:**
- All text is translated.
- The original meaning is preserved.
- No paragraphs are missing or repeated.

**Status:** Not tested.

### Test 2: DOCX File Translation

**Input:** A DOCX document containing headings, paragraphs, and lists.

**Expected Result:**
- Content is extracted in the correct order.
- Headings and lists remain organized.
- Important information is preserved.

**Status:** Not tested.

### Test 3: Text-Based PDF Translation

**Input:** A PDF containing selectable text.

**Expected Result:**
- Text is extracted correctly.
- Page order is preserved.
- No important sections are missing.

**Status:** Not tested.

### Test 4: Scanned PDF and OCR

**Input:** A scanned PDF or image-based document.

**Expected Result:**
- OCR is used only when available.
- Extracted text is reviewed for recognition errors.
- Unclear content is reported to the user.

**Status:** Not tested.

### Test 5: Arabic Translation and RTL Formatting

**Input:** An English document translated into Arabic.

**Expected Result:**
- Arabic letters are connected correctly.
- Text direction is right-to-left.
- Numbers and English terms remain readable.
- No overlapping or reversed text appears.

**Status:** Not tested.

### Test 6: Long Document Translation

**Input:** A document containing multiple pages.

**Expected Result:**
- All sections are processed.
- No paragraphs are skipped or repeated.
- The original content order is preserved.

**Status:** Not tested.

### Test 7: PDF Output

**Input:** A successfully translated document.

**Expected Result:**
- A PDF file is generated successfully.
- The file can be opened.
- Text is readable.
- Formatting is consistent.

**Status:** Not tested.

### Test 8: Unsupported Tools or File Types

**Input:** A file that cannot be processed with the available tools.

**Expected Result:**
- The limitation is explained clearly.
- The assistant does not claim that the file was processed.
- An alternative is suggested when possible.

**Status:** Not tested.

## 3. Test Results

Record the results after performing each test.

| Test | Status | Notes |
|---|---|---|
| TXT Translation | Not tested | |
| DOCX Translation | Not tested | |
| PDF Extraction | Not tested | |
| OCR | Not tested | |
| Arabic RTL | Not tested | |
| Long Documents | Not tested | |
| PDF Generation | Not tested | |
| Unsupported Files | Not tested | |

## 4. Final Evaluation

The skill should be considered ready only after the main test cases have been performed and important issues have been addressed.

Do not report successful results without actual testing.
