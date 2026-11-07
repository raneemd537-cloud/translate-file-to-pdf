---
name: translate-file-to-pdf
description: Translate document files into another language and create a well-formatted PDF while fully preserving the original content, structure, technical details, tables, code, and meaning. Performs complete translation (not summarization) by default, with mandatory completeness verification before delivery. Supports document extraction, faithful translation, structure preservation, Arabic RTL, and PDF generation when the required tools are available.
---

# Translate File to PDF

## 1. Purpose

This skill helps users translate documents into another language and create a readable PDF version of the translated document.

**Core principle: Full and faithful translation, not summarization.**

The main goals are:

- Translate the complete readable content of the source document.
- Preserve the original order of sections, pages, slides, headings, and paragraphs.
- Preserve every table row, column, heading, value, and relationship.
- Preserve code blocks, formulas, technical names, numbers, and examples exactly.
- Never summarize, shorten, skip, or remove content unless the user explicitly requests a summary.
- Create a clean, readable PDF with correct language direction (including Arabic RTL).
- Perform a mandatory completeness verification before claiming the translation is complete.

Accuracy and completeness always come before appearance or page-count reduction.

## 2. Understand the User's Request

Before starting:

1. Identify the uploaded file and its type.
2. Determine the target language. If unclear, ask the user.
3. Default to full translation of the entire document. Only summarize if the user explicitly asks for a summary or abbreviated version.
4. Note any special requests (e.g., "keep the tables", "do not remove any details", formal tone).
5. Explain important limitations of the current environment before processing when relevant.

Short requests such as the following should be understood without unnecessary questions:

- "Translate this file into Arabic and make it a PDF."
- "Translate this document into English."
- "Convert this file into an Arabic PDF and keep the tables."
- "Translate this lecture without removing any details."

If the request is already clear, proceed. Ask only when essential information is missing.

## 3. Check Available Tools

Before processing any file:

- Check which file-reading, text-extraction, OCR, and PDF-generation tools are actually available in the current environment.
- Use only tools and libraries that are present.
- Do not assume a particular library, command, or external skill is installed.
- Do not invent tool names or pretend that a tool was used.
- If a required capability is unavailable, explain the limitation honestly and offer a practical alternative (for example, provide the translated text in Markdown or another supported format).

This skill provides structured instructions. It does not contain its own translation engine, OCR engine, or PDF-generation library. Actual processing depends on the AI platform and available tools.

## 4. Supported File Types

Support the following formats only when the available tools can process them:

### PDF
- Extract text while preserving page or slide order.
- Identify headings, paragraphs, lists, tables, and code when possible.
- Check whether the PDF contains selectable text.
- If it is scanned or image-based, use OCR only if an appropriate OCR tool is available.
- For presentation-style PDFs (slides), treat each slide as a logical unit and preserve all content from every slide.

### DOCX
- Extract paragraphs, headings, lists, and tables.
- Preserve the logical order of the content.
- Keep important document structure whenever possible.

### TXT and Markdown
- Read the text directly.
- Preserve headings, paragraphs, lists, and other basic formatting.

### Images and Scanned Documents
- Use OCR only when an appropriate tool is available.
- Check the extracted text for obvious recognition errors.
- Preserve the order of text and its relationship with any tables or images.
- Do not invent text that cannot be read.
- Mark unclear or unreadable content for user review.
- Report which pages could not be processed reliably.
- Do not claim OCR support if the required capability is unavailable.

Do not claim support for a format that cannot actually be processed.

## 5. Extract and Organize the Content

Before translating:

1. Extract all readable content from the document.
2. Keep the original page, slide, or section order.
3. Identify headings, subheadings, paragraphs, bullet points, numbered lists, notes, captions, footnotes, tables, code blocks, formulas, and examples.
4. Preserve numbers, percentages, dates, measurements, statistical results, names, links, and technical terms exactly.
5. Identify unclear or unreadable sections and mark them.
6. Never silently remove content because of space, formatting difficulty, or length.

For long documents or multi-slide presentations, process content in manageable sections while keeping a clear inventory of what has been extracted so nothing is missed or duplicated.

**Presentation / slide-based PDFs:**
- Preserve slide titles and slide order.
- Preserve all content from each slide.
- Do not omit a slide simply because it contains little text.
- If multiple original slides are placed on one output page, all their content must remain present and clearly distinguishable.

**Ordinary documents:**
- Preserve headings, subheadings, paragraphs, tables, lists, and page order.

The skill does not have to reproduce the exact original visual design in every case. However, it must preserve the original information and logical structure. If the original layout cannot be reproduced, prioritize content completeness and readability.

## 6. Translation Rules — Full and Faithful Translation

**Translation means transferring the complete original content into another language.**
**Summarization means reducing or shortening the original content.**

This skill performs translation by default. It must not summarize unless the user explicitly requests a summary.

### Mandatory rules

1. Translate all readable content from the source document.
2. Preserve the original order of sections, pages, slides, headings, and paragraphs.
3. Never summarize, shorten, skip, or remove content unless the user explicitly requests a summary.
4. Never silently omit content because of space or formatting limitations.
5. Preserve all bullet points, numbered lists, notes, captions, examples, explanations, and footnotes.
6. Preserve every table, including its rows, columns, headers, values, and relationships.
7. Keep separate items separate. Do not merge columns, rows, or concepts that are separate in the original.
8. Preserve all numbers, percentages, dates, measurements, and statistical results exactly.
9. Preserve technical terminology, programming terms, dataset column names, function names, library names, and variable names.
10. Preserve mathematical formulas and their meaning.
11. Translate explanatory text without changing its original meaning.
12. Do not add new explanations or information that does not exist in the original document unless the user explicitly asks for additional explanations.

If a sentence or section is unclear, do not guess its meaning. Note the uncertainty when necessary.

## 7. Special Rules for Code and Technical Content

When the document contains code, technical examples, or programming-related material:

- Preserve code exactly as it appears in the original.
- Never translate programming keywords, variable names, function names, library names, class names, method names, or commands.
- Preserve code indentation and formatting whenever possible.
- Preserve formulas and mathematical notation.
- Translate only the explanatory text around the code; leave the code itself unchanged.
- Preserve technical examples and their outputs.
- Avoid changing the meaning of technical terms.
- Never replace a detailed technical example with a short general explanation.

Examples of terms that must remain unchanged (illustrative, not exhaustive):

- `KNNImputer`
- `IterativeImputer`
- `ffill`
- `bfill`
- `interpolate`
- `age_missing`
- Dataset column names such as `Sex`, `Age`, `SibSp`
- Library and function names in general

The surrounding explanations may be translated into the target language.

## 8. Special Rules for Tables and Structured Data

Handle tables with particular care:

- Preserve the original number of columns and rows whenever possible.
- Preserve column headers and their relationships with the values under them.
- Do not combine separate columns.
- Do not move values into unrelated rows.
- Do not replace detailed tables with general descriptions.
- Preserve empty cells when they have structural meaning.
- Maintain the distinction between numerical values, percentages, categories, and text.
- If a table is too wide for the output page, use a suitable layout or carefully split it while preserving all information and making the relationship between parts clear.

Before finalizing the PDF, compare the translated tables with the original tables to confirm that rows, columns, and values match.

**Regression example (must not be repeated):**
In a data-preprocessing lecture, the columns `Sex`, `Age`, and `SibSp` were separate. Combining them into one row labeled "mixed" is incorrect and must be avoided.

## 9. Arabic and Right-to-Left Support

When the target language is Arabic (or another right-to-left language):

- Use correct right-to-left text direction (not merely right alignment).
- Ensure Arabic letters are properly connected and shaped.
- Keep punctuation in appropriate positions.
- Preserve the logical order of mixed Arabic and English text.
- Display English technical terms correctly inside Arabic paragraphs.
- Avoid reversing code, formulas, numbers, or English technical expressions.
- Use fonts that support Arabic characters.
- Make tables readable and correctly aligned for RTL.
- Ensure that headings, paragraphs, lists, and page numbers are positioned consistently.

Do not sacrifice translation accuracy or completeness to achieve a visually attractive layout.

If the available PDF-generation tools cannot correctly handle Arabic shaping and bidirectional text, explain this limitation instead of presenting an incorrectly formatted document as complete.

## 10. Create the PDF

After translation and before final delivery:

1. Confirm that all translated sections are present.
2. Organize headings, paragraphs, lists, tables, and code blocks clearly.
3. Use a consistent font system and readable font sizes.
4. Maintain appropriate spacing and margins; avoid crowded pages.
5. Keep tables and code blocks organized and fully visible.
6. Use page numbers when appropriate.
7. Support the correct writing direction for the target language.
8. Adapt the layout to the document type when helpful:
   - Presentation slides may use a presentation-style layout.
   - Academic documents may use a formal document layout.
   - Technical documents should make code and tables easy to read.

Do not force every document into the same page size or visual template.

Create the PDF only with an available and suitable tool. Do not claim that a PDF has been created unless an actual PDF file has been generated successfully.

Prioritize content accuracy and completeness over reducing the number of pages. Changing page dimensions or combining content is acceptable only when no information is lost and the result remains readable.

## 11. Mandatory Completeness Verification Stage

**This stage is required before generating or delivering the final PDF.**

Do not claim that the translation is complete unless these checks have actually been performed. If a page, image, table, or text section cannot be read or extracted, clearly report it instead of silently skipping it. If full verification is not technically possible, explain the limitation honestly.

### Content completeness
- Are all original sections included?
- Are all pages or slides accounted for?
- Are all headings translated?
- Are all paragraphs and bullet points included?
- Are all examples, notes, captions, and footnotes preserved?

### Tables
- Are all table rows included?
- Are all table columns included?
- Are values associated with the correct headers?
- Were separate columns or rows accidentally merged?

### Technical accuracy
- Are code blocks preserved exactly?
- Are function names, variable names, library names, and dataset column names unchanged?
- Are numerical values and percentages correct?
- Are formulas and technical examples complete?

### Translation accuracy
- Does the translation preserve the original meaning?
- Has any information been added without permission?
- Has any information been shortened or omitted?
- Are technical terms handled consistently?

### PDF quality
- Is the text readable?
- Is Arabic (if applicable) displayed correctly with proper shaping and direction?
- Are there overlapping elements?
- Are tables and code blocks fully visible?
- Are any sections cut off or missing?

Only after these checks pass (or limitations are clearly reported) should the final PDF be delivered.

## 12. Deliver the Result

When the PDF is successfully created and verified:

- Provide the generated PDF file.
- State the source and target languages.
- Briefly describe any formatting or extraction limitations.
- Mention any sections, pages, or elements that could not be extracted or translated accurately.

If PDF creation fails, explain what happened and offer the translated text or another available output format.

Never provide a fake download link or claim that an unavailable file exists.

## 13. User Experience

Keep the process simple and clear.

- Ask only necessary questions.
- Give short progress updates during long tasks when helpful.
- Inform the user about important limitations early.
- Do not overwhelm the user with unnecessary technical details.
- Let the user know when the translation and PDF are ready.

If a limitation prevents completing the task, explain it clearly and offer a practical alternative.

## 14. Core Principles

1. **Full translation by default.** Never summarize unless explicitly requested.
2. **Completeness over appearance.** Do not omit content to fit a nicer layout or fewer pages.
3. **Structure and technical fidelity.** Preserve tables, code, formulas, numbers, and separate items exactly.
4. **Honest reporting.** Never claim completeness or success that was not actually achieved. Report unreadable or unprocessed parts.
5. **Accuracy before beauty.** A well-formatted PDF is not successful if its translation is incomplete, its meaning is altered, or its text cannot be read.

Always be honest about the tools used, the work completed, and the limitations encountered.
