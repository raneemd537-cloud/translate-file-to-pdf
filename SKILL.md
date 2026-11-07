
---
name: translate-file-to-pdf
description: Translate document files into another language and create a well-formatted PDF while preserving the original content, structure, and meaning as much as the available tools allow. Supports document extraction, translation, and PDF generation when the required tools are available.
---

# Translate File to PDF

## 1. Purpose

This skill helps users translate documents into another language and create a readable PDF version of the translated document.

The main goals are:

- Preserve the meaning of the original content.
- Keep the document structure organized.
- Maintain important details such as names, numbers, dates, and technical terms.
- Create a clean and readable PDF.
- Support right-to-left languages, especially Arabic, when the available tools allow it.

## 2. Understand the User's Request

Before starting:

1. Identify the uploaded file.
2. Ask the user for the target language if it is not specified.
3. Ask whether the user wants a full translation or selected sections.
4. Identify any special preferences, such as formal or simple language.
5. Explain important limitations before processing the file.

If the user does not specify a translation style, use clear and natural language while preserving the original meaning.

## 3. Check Available Tools

Before processing any file:

- Check which file-reading, text-extraction, OCR, translation, and PDF-generation tools are actually available.
- Use only tools and libraries that are available in the current environment.
- Do not assume that a particular library, command, or external skill is installed.
- Do not invent tool names or pretend that a tool was used.
- If a required capability is unavailable, explain the limitation and offer a practical alternative.

## 4. Supported File Types

Support the following formats only when the available tools can process them:

### PDF
- Extract text while preserving page order.
- Identify headings, paragraphs, lists, and tables when possible.
- Check whether the PDF contains selectable text.
- If it is scanned or image-based, use OCR only if an OCR tool is available.

### DOCX
- Extract paragraphs, headings, and tables.
- Preserve the logical order of the content.
- Keep important document structure whenever possible.

### TXT and Markdown
- Read the text directly.
- Preserve headings, paragraphs, lists, and other basic formatting.

### Images and Scanned Documents
- Use OCR only when an appropriate tool is available.
- Check the extracted text for missing or incorrectly recognized words.
- Inform the user if the image quality affects accuracy.

Do not claim support for a format that cannot actually be processed.

## 5. Extract and Organize the Content

Before translating:

1. Extract the document content.
2. Keep the original page order.
3. Identify headings, paragraphs, lists, and tables.
4. Preserve numbers, dates, names, links, and important technical terms.
5. Identify unclear or unreadable sections.
6. Avoid silently removing content.

For long documents, process the content in manageable sections.

Keep track of completed sections to avoid missing or repeating content.

## 6. Translation Rules

Translate the meaning, not just individual words.

Follow these rules:

- Preserve the original meaning and context.
- Use natural language in the target language.
- Keep names, dates, numbers, and measurements accurate.
- Translate technical terms consistently.
- Avoid adding information that does not exist in the original.
- Do not summarize unless the user requests a summary.
- Do not remove paragraphs or sections.
- Preserve tables and lists as much as possible.

If a sentence is unclear, do not guess its meaning. Explain the uncertainty when necessary.

## 7. Arabic and Right-to-Left Support

When the target language is Arabic or another right-to-left language:

- Use a font that supports the required characters.
- Ensure Arabic letters are connected and shaped correctly.
- Apply bidirectional text handling so Arabic and English text appear in the correct order.
- Set the correct text direction, not only right alignment.
- Keep numbers, punctuation, and mixed-language expressions readable.
- Check headings, paragraphs, and tables.
- Verify that text is not reversed, disconnected, or overlapping.

Important:

Right alignment alone does not provide correct Arabic support.

If the available PDF-generation tools cannot correctly handle Arabic shaping and bidirectional text, explain this limitation instead of presenting an incorrectly formatted document as complete.

## 8. Create the PDF

After translation:

1. Check that all translated sections are included.
2. Organize headings, paragraphs, and lists.
3. Use readable fonts and suitable font sizes.
4. Maintain consistent spacing and margins.
5. Keep tables readable.
6. Use page breaks when needed.
7. Support the correct writing direction for the target language.

Create the PDF only with an available and suitable tool.

Do not claim that a PDF has been created unless an actual PDF file has been generated successfully.

## 9. Quality Check

Before delivering the result, check the following:

### Translation
- Is the full content translated?
- Is the original meaning preserved?
- Are names, numbers, and dates correct?
- Are any sections missing or repeated?

### Formatting
- Are headings and paragraphs organized?
- Are tables readable?
- Are pages in the correct order?
- Is the font readable?

### Arabic Support
- Are letters connected correctly?
- Is the text direction correct?
- Are mixed Arabic and English sentences readable?
- Is there any overlapping or reversed text?

### File
- Was the PDF actually created?
- Can the generated file be opened?
- Is the output file available to the user?

Do not report a test as passed unless it was actually performed.

## 10. Deliver the Result

When the PDF is successfully created:

- Provide the generated PDF file.
- State the source and target languages.
- Briefly describe any formatting limitations.
- Mention any sections that could not be extracted or translated accurately.

If PDF creation fails, explain what happened and offer the translated text or another available output format.

Never provide a fake download link or claim that an unavailable file exists.

## 11. User Experience

Keep the process simple and clear.

- Ask only necessary questions.
- Give short progress updates during long tasks.
- Inform the user about important limitations.
- Do not overwhelm the user with technical details.
- Let the user know when the translation and PDF are ready.

## 12. Core Principle

Accuracy comes before appearance.

A well-formatted PDF is not successful if its translation is incomplete, its meaning is incorrect, or its text cannot be read.

Always be honest about the tools used, the work completed, and the limitations encountered.
